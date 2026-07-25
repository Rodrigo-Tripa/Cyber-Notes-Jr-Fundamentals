# John the Ripper

#password-cracking #hashes #authentication #passwords #linux #cybersecurity #tool

## Overview

**John the Ripper (JtR)** is one of the most widely used password-cracking tools in cybersecurity. It is designed to recover plaintext passwords from password hashes and encrypted files by systematically testing password candidates until a match is found.

Originally developed for Unix systems, John now supports hundreds of hash formats and encrypted file types through the **Jumbo** community edition. It is widely used during penetration tests, security audits, digital forensics, and password policy assessments to identify weak passwords before attackers can exploit them.

Unlike vulnerability scanners or exploitation frameworks, John does not attack systems directly. Instead, it performs **offline password-cracking attacks** against password hashes or encrypted files that have already been obtained.

---

## How John the Ripper Works

John attempts to recover passwords by repeatedly generating password candidates, hashing them using the same algorithm as the target, and comparing the result against the stored hash.

```text
Candidate Password
        │
        ▼
Hash Algorithm
        │
        ▼
Generated Hash
        │
Compare
        │
        ▼
Match?
```

If the generated hash matches the target hash, the original password has been successfully recovered.

Since modern cryptographic hash functions are designed to be one-way, John cannot decrypt hashes. Instead, it relies on guessing passwords until the resulting hash matches the stored value.

---

## Supported Hash Types

John supports a large number of authentication systems and encrypted file formats.

Common examples include:

- Unix `/etc/shadow`
- Windows NTLM
- LM
- SHA-1
- SHA-256
- SHA-512
- bcrypt
- Kerberos
- ZIP archives
- RAR archives
- PDF documents
- OpenSSH private keys
- KeePass databases

Support depends on the installed version, with **John Jumbo** including significantly more formats than the core release.

---

## Password Cracking Modes

John provides several cracking strategies optimized for different situations.

### Single Crack Mode

Single Crack Mode attempts to generate passwords using information extracted from the target itself.

For example, usernames, full names, or other metadata may be transformed into likely password candidates using predefined rules.

This mode is extremely fast and is often used as the first attack.

---

### Wordlist Mode

Wordlist Mode uses a dictionary containing thousands or millions of candidate passwords.

Each entry is hashed and compared against the target.

This is the most common attack because many users choose weak or predictable passwords.

Popular wordlists include:

- rockyou.txt
- SecLists
- CrackStation dictionaries

---

### Incremental Mode

Incremental Mode performs a brute-force attack.

Instead of using existing words, John systematically generates every possible password combination according to predefined character sets and length limits.

Although extremely thorough, brute-force attacks become computationally expensive as password complexity increases.

---

### Rule-Based Mode

Rule-Based Mode modifies words from a dictionary to produce additional candidates.

Examples include:

- Capitalizing letters
- Appending numbers
- Replacing characters
- Adding symbols
- Reversing words

For example:

```text
password
Password
Password1
P@ssword
Password123
```

This significantly increases the effectiveness of dictionary attacks while remaining much faster than full brute force.

---

## Jumbo Utilities

The Jumbo edition includes numerous helper utilities that extract password hashes from encrypted files before they can be cracked.

Common examples include:

| Utility | Purpose |
|---------|---------|
| zip2john | Extract ZIP password hashes |
| rar2john | Extract RAR password hashes |
| ssh2john | Extract encrypted SSH private keys |
| keepass2john | Extract KeePass database hashes |
| pdf2john | Extract encrypted PDF hashes |
| dmg2john | Extract Apple DMG hashes |
| office2john | Extract Microsoft Office document hashes |

---

## Performance and Limitations

The effectiveness of John the Ripper depends primarily on the strength of the target passwords and the computational cost of the hashing algorithm.

Weak passwords can often be recovered within seconds using common wordlists, while long, random passwords protected with modern password hashing algorithms such as **bcrypt**, **scrypt**, or **Argon2** may require an impractical amount of time to crack.

Modern CPUs and GPUs can compute billions of hashes per second for fast algorithms like **MD5** or **SHA-1**, but intentionally slow password hashing algorithms greatly reduce the number of guesses that can be performed each second.

---

## Salts

A **salt** is a random value added to a password before hashing.

Instead of storing:

```text
password
```

The system hashes:

```text
password + random_salt
```

This ensures that identical passwords produce different hashes for different users.

Salts provide several important security benefits:

- Prevent identical passwords from generating identical hashes.
- Defeat precomputed rainbow tables.
- Force attackers to crack each password individually.

John fully supports salted password hashes, although salts prevent attackers from reusing work across multiple accounts.

---

## Password Strength

John demonstrates that the weakest component of many authentication systems is not the cryptographic algorithm, but the password itself.

Strong passwords should:

- Be long.
- Contain random characters.
- Avoid dictionary words.
- Be unique for every account.
- Be generated and stored using a password manager whenever possible.

Modern authentication systems should also use slow password hashing algorithms together with unique salts for every stored password.

---

## Typical Workflow

A typical password-cracking assessment follows these steps:

1. Obtain password hashes or encrypted files.
2. Identify the correct hash format.
3. Select an appropriate cracking mode.
4. Run John against the target.
5. Review recovered passwords.
6. Assess password policy weaknesses.

The objective is to evaluate password security rather than compromise cryptographic algorithms.

---

## Ethical Use

John the Ripper is a legitimate security tool intended for authorized environments.

Common use cases include:

- Penetration testing
- Security assessments
- Password auditing
- Incident response
- Digital forensics
- Password recovery

Running password-cracking attacks against systems without authorization may violate organizational policies and applicable laws.

---

## Best Practices

When using John the Ripper:

- Always identify the correct hash format before cracking.
- Begin with Single Crack Mode when applicable.
- Use high-quality wordlists before attempting brute force.
- Apply custom rules to improve dictionary attacks.
- Prefer John Jumbo for its extended format support.
- Store recovered credentials securely during assessments.
- Verify findings responsibly and report weak password policies.

---

## Related Notes

- [[Cryptography]]
- [[Linux]]
- [[Linux-CLI]]
- [[Permissions]]
- [[Active-Directory]]

---

## Key Takeaways

- John the Ripper is an offline password-cracking tool used to recover plaintext passwords from hashes and encrypted files.
- It supports hundreds of hash formats through the Jumbo edition.
- Single Crack, Wordlist, Incremental, and Rule-Based modes provide different cracking strategies.
- Helper utilities such as `zip2john` and `ssh2john` extract hashes from encrypted files before cracking.
- Password strength and modern hashing algorithms have a far greater impact on security than the cracking tool itself.
- John the Ripper is primarily used for penetration testing, password auditing, digital forensics, and security assessments.