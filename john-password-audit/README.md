# John the Ripper Password Hash Auditing Lab

## Overview

This project explores password hash auditing using John the Ripper in a controlled Kali Linux environment.

The lab demonstrates wordlist attacks and incremental numeric attacks, comparing the practical differences between MD5 and bcrypt password hashing.

All passwords and hashes used in this project were created for educational testing. No real user credentials or third-party password hashes were used.

## Objectives

* Understand password hashing and password auditing.
* Perform wordlist-based password recovery.
* Perform incremental numeric password recovery.
* Compare the observed performance of MD5 and bcrypt.
* Identify password security risks and recommend mitigations.

## Tools and Environment

* Kali Linux
* John the Ripper
* Python 3
* Python bcrypt library
* OpenSSL
* Linux command-line utilities

## Project Structure

```text
john-password-audit/
├── README.md
├── .gitignore
├── hashes/
│   ├── md5_hash.txt
│   └── bcrypt_hash.txt
├── wordlists/
│   └── test_words.txt
└── brute-force-lab/
    ├── numeric_hash.txt
    ├── six_digit_md5.txt
    └── six_digit_bcrypt.txt
```

Screenshots and local evidence are intentionally excluded from the public repository.

## Experiments and Results

### 1. MD5 Wordlist Attack

A sample password, `football123`, was hashed using MD5.

The hash was audited using a custom wordlist containing five candidate passwords.

**Result:** John the Ripper successfully recovered the password.

### 2. bcrypt Wordlist Attack

The same sample password was hashed using bcrypt and tested against the custom wordlist.

**Result:** John the Ripper successfully recovered the password.

### 3. Four-Digit Numeric Password Recovery

A four-digit numeric password, `4827`, was hashed using MD5.

John the Ripper's incremental digits mode was configured to test four-digit numeric candidates.

**Result:** The password was recovered successfully.

### 4. Six-Digit Numeric MD5 Attack

A six-digit numeric password, `583104`, was hashed using MD5.

John the Ripper's incremental digits mode was restricted to six-digit candidates.

**Result:** The password was recovered successfully.

### 5. Six-Digit Numeric bcrypt Attack

The same six-digit password, `583104`, was hashed using bcrypt with a cost factor of 12.

The attack used incremental numeric mode with the candidate length restricted to six digits.

**Result:** John the Ripper eventually recovered the password. The observed runtime was approximately 15 hours and 2 minutes.

The recovery was confirmed using John the Ripper's `--show` option.

This runtime reflects the specific test environment and attack configuration. It is not a universal estimate of bcrypt cracking time.

## Results Summary

| Experiment      | Hash Algorithm | Attack Method       | Result                  |
| --------------- | -------------- | ------------------- | ----------------------- |
| Wordlist test   | MD5            | Wordlist            | `football123` recovered |
| Wordlist test   | bcrypt         | Wordlist            | `football123` recovered |
| Four-digit test | MD5            | Incremental numeric | `4827` recovered        |
| Six-digit test  | MD5            | Incremental numeric | `583104` recovered      |
| Six-digit test  | bcrypt         | Incremental numeric | `583104` recovered      |

## Key Findings

### MD5

MD5 is a fast general-purpose hash function and is unsuitable for modern password storage. Its speed allows attackers to test password guesses comparatively quickly.

### bcrypt

bcrypt is designed for password hashing and makes each guess more computationally expensive than a fast general-purpose hash such as MD5.

Its configurable cost factor increases the computational work required for password guessing. However, bcrypt cannot compensate fully for short or predictable passwords.

### Wordlist Attacks

Wordlist attacks test candidate passwords from a prepared list. Their effectiveness depends on whether the correct password is included among the candidates.

### Incremental Attacks

Incremental attacks generate password candidates according to a configured character set and length range.

The experiments demonstrated that even short numeric passwords can be recovered through systematic guessing.

## Security Recommendations

* Avoid MD5 for password storage.
* Use a password-hashing algorithm such as Argon2id, scrypt, or appropriately configured bcrypt.
* Choose long, unique, unpredictable passwords or passphrases.
* Consider using a password manager.
* Configure password-hashing parameters according to current security guidance.
* Protect stored password hashes against unauthorized access.
* Enable multifactor authentication where available.

## Limitations

* The experiments used a small set of synthetic passwords and hashes.
* The custom wordlist contained only five candidate passwords.
* Numeric attacks were restricted to particular password lengths and a digits-only character set.
* The observed bcrypt runtime applies only to this experiment and its environment.
* These results do not establish universal password-cracking times or prove that any password-hashing configuration is secure in every situation.

## Disclaimer

This project is intended for educational purposes and authorized password-auditing practice only.

All test passwords and hashes were created for this lab. Do not attempt to access or audit password hashes without explicit authorization.

## Author

A hands-on cybersecurity learning project focused on password auditing, password-hashing security, and the practical differences between fast general-purpose hashes and password-hashing algorithms.
