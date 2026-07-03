# Using the `pass` Password Manager on macOS

A step-by-step guide to installing, configuring, and managing passwords with `pass` (the standard Unix password manager) on macOS.

## Table of Contents
- [Prerequisites & Installation](#prerequisites--installation)
- [Initial Setup](#initial-setup)
  - [1. Generate a GPG Key](#1-generate-a-gpg-key)
  - [2. Initialize the Password Store](#2-initialize-the-password-store)
- [Managing Passwords](#managing-passwords)
  - [Storing a Password](#storing-a-password)
  - [Retrieving a Password](#retrieving-a-password)
  - [Removing a Password](#removing-a-password)

---

## [Prerequisites & Installation](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

`pass` stores password files encrypted using GnuPG (GPG). Install both utilities using Homebrew:

```bash
brew install pass gnupg
```

---

## [Initial Setup](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

### [1. Generate a GPG Key](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

If you do not have a GPG key, generate one to encrypt and decrypt your passwords:

1. Run the generation command:
   ```bash
   gpg --full-generate-key
   ```
2. Follow the interactive prompts:
   - Select the default key type (usually **RSA and RSA**).
   - Choose a key size (e.g., **3072** or **4096** bits).
   - Set the expiration (choose **0** for no expiration).
   - Enter your name and email address.
   - Set a strong **passphrase** (remember this passphrase, as it unlocks your password store).

3. Retrieve your GPG Key ID by listing your secret keys:
   ```bash
   gpg --list-secret-keys --keyid-format=long
   ```
   Look for the hexadecimal ID following the key length (e.g., in `sec rsa3072/3AA5C34371567BD2`, the Key ID is `3AA5C34371567BD2`).

### [2. Initialize the Password Store](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

Initialize `pass` using your GPG Key ID:

```bash
pass init <YOUR_GPG_KEY_ID>
```

This creates a hidden directory at `~/.password-store` where your encrypted password files will reside.

---

## [Managing Passwords](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

`pass` supports folder hierarchy to keep your passwords organized (e.g., `email/gmail`, `social/twitter`).

### [Storing a Password](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

#### [Option A: Manually input a password](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)
To enter a password manually:
```bash
pass insert <path/to/password>
```
*Example:*
```bash
pass insert email/gmail
```
*Type and verify the password when prompted.*

#### [Option B: Generate a random password](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)
To generate and store a secure random password of a specific length (e.g., 20 characters):
```bash
pass generate <path/to/password> <length>
```
*Example:*
```bash
pass generate social/twitter 20
```

---

### [Retrieving a Password](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

- **Display the password in the terminal:**
  ```bash
  pass <path/to/password>
  ```
- **Copy the password directly to your clipboard** (clears automatically after 45 seconds):
  ```bash
  pass -c <path/to/password>
  ```

---

### [Removing a Password](https://github.com/c4arl0s/pass#using-the-pass-password-manager-on-macos)

- **Delete a specific password** (asks for confirmation):
  ```bash
  pass rm <path/to/password>
  ```
- **Delete a password without confirmation** (force delete):
  ```bash
  pass rm -f <path/to/password>
  ```
- **Recursively delete a directory** (deletes all passwords inside a folder):
  ```bash
  pass rm -r <directory_name>
  ```
