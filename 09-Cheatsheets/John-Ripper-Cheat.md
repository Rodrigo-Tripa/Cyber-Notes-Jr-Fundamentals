#tool #cheatsheet #john #password-cracking #hashes

# John the Ripper Cheat Sheet

John the Ripper (John) is a password cracking tool used to recover passwords from hashes and encrypted files. It supports hundreds of hash formats and is commonly used during password audits, penetration tests, and CTFs.

---

# Basic Syntax

```bash
john [OPTIONS] <hash-file>
```

Examples:

```bash
john hashes.txt

john --wordlist=rockyou.txt hashes.txt

john --show hashes.txt
```

---

# Common Workflow

```text
1. Identify the hash type
2. Extract hashes (if needed)
3. Select a cracking mode
4. Crack the hashes
5. Display recovered passwords
```

---

# Most Important Options

| Option | Description | When to Use |
|---------|-------------|-------------|
| `--wordlist=<file>` | Use a wordlist | Most common cracking method. |
| `--rules` | Apply mangling rules | Generate password variations automatically. |
| `--format=<type>` | Specify the hash format | Use when John cannot detect it automatically. |
| `--show` | Display cracked passwords | View recovered credentials. |
| `--incremental` | Brute-force attack | Last resort when dictionary attacks fail. |
| `--single` | Single Crack mode | Uses username and account information to generate guesses. |
| `--fork=<n>` | Use multiple CPU processes | Speed up cracking on multi-core systems. |
| `--session=<name>` | Save session name | Resume long-running attacks later. |
| `--restore` | Resume previous session | Continue interrupted cracking sessions. |
| `--pot=<file>` | Specify a potfile | Store or load cracked passwords from another file. |

---

# Common Cracking Modes

## Dictionary Attack

```bash
john --wordlist=rockyou.txt hashes.txt
```

Uses passwords from a wordlist.

---

## Dictionary + Rules

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

Applies common password mutations such as numbers, symbols and capitalization.

---

## Incremental (Brute Force)

```bash
john --incremental hashes.txt
```

Attempts every possible password combination.

---

## Single Crack Mode

```bash
john --single hashes.txt
```

Generates passwords using usernames and other account information.

---

# Common Formats

| Hash Type | Format |
|-----------|--------|
| MD5 | `raw-md5` |
| SHA1 | `raw-sha1` |
| SHA256 | `raw-sha256` |
| SHA512 | `raw-sha512` |
| NTLM | `NT` |
| bcrypt | `bcrypt` |
| LM | `LM` |
| Kerberos 5 TGS | `krb5tgs` |

Example:

```bash
john --format=NT hashes.txt
```

---

# Common Workflows

## Crack NTLM Hashes

```bash
john --format=NT --wordlist=rockyou.txt ntlm.txt
```

---

## Crack MD5 Hashes

```bash
john --format=raw-md5 --wordlist=rockyou.txt md5.txt
```

---

## Crack SHA256 Hashes

```bash
john --format=raw-sha256 --wordlist=rockyou.txt sha256.txt
```

---

## Display Cracked Passwords

```bash
john --show hashes.txt
```

---

## Resume a Session

```bash
john --restore
```

---

## Create a Named Session

```bash
john --session=office_audit hashes.txt
```

---

## Use Four CPU Cores

```bash
john --fork=4 --wordlist=rockyou.txt hashes.txt
```

---

# Cracking Encrypted Files

John cannot crack encrypted files directly. The password hash must first be extracted using helper tools.

| File Type | Extraction Tool |
|-----------|-----------------|
| ZIP | `zip2john` |
| RAR | `rar2john` |
| PDF | `pdf2john` |
| SSH Private Key | `ssh2john` |
| Office Documents | `office2john` |
| KeePass | `keepass2john` |
| Linux Shadow | `unshadow` |

Example:

```bash
zip2john secret.zip > hash.txt

john --wordlist=rockyou.txt hash.txt
```

---

# Advanced Examples

## Crack Multiple Hash Files

```bash
john hashes1.txt hashes2.txt
```

---

## Force a Hash Format

```bash
john --format=raw-sha512 hashes.txt
```

---

## Generate Password Variations

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

---

## Use a Custom Wordlist

```bash
john --wordlist=company_passwords.txt hashes.txt
```

---

## Crack a ZIP Archive

```bash
zip2john secret.zip > zip.hash

john --wordlist=rockyou.txt zip.hash
```

---

## Crack an SSH Private Key

```bash
ssh2john id_rsa > ssh.hash

john --wordlist=rockyou.txt ssh.hash
```

---

## Crack a PDF

```bash
pdf2john document.pdf > pdf.hash

john --wordlist=rockyou.txt pdf.hash
```

---

## Crack a KeePass Database

```bash
keepass2john database.kdbx > keepass.hash

john --wordlist=rockyou.txt keepass.hash
```

---

# Typical Pentesting Workflow

```text
1. Obtain the password hash
2. Identify the hash format
3. Start with a dictionary attack
4. Retry using rules
5. Use brute force only if necessary
6. Display recovered passwords
```

Typical commands:

```bash
john --wordlist=rockyou.txt hashes.txt

john --wordlist=rockyou.txt --rules hashes.txt

john --format=NT hashes.txt

john --show hashes.txt

john --restore
```

---

# Commands You'll Use Most

```bash
john --wordlist=rockyou.txt hashes.txt

john --wordlist=rockyou.txt --rules hashes.txt

john --format=NT hashes.txt

john --show hashes.txt

john --restore

zip2john archive.zip > hash.txt

ssh2john id_rsa > hash.txt
```
