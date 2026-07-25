# Cryptography

#cryptography #encryption #hashing #pki #tls #cybersecurity

## Overview

**Cryptography** is the science of protecting information by transforming it into a form that can only be understood by authorized parties. It combines mathematics, algorithms, and cryptographic keys to secure data against unauthorized access, modification, and forgery.

Originally developed to protect military and diplomatic communications, cryptography is now a fundamental component of modern computing. It secures Internet communications, protects sensitive information, verifies digital identities, safeguards financial transactions, and forms the basis of many cybersecurity technologies.

Rather than being a single technology, cryptography encompasses a collection of techniques that provide different security properties depending on the problem being solved.

---

## Why Cryptography Matters

Whenever information is transmitted or stored, it may be exposed to unauthorized access or manipulation.

Without cryptography, attackers could:

- Read confidential information.
- Modify data without detection.
- Impersonate legitimate users or systems.
- Forge digital documents or transactions.
- Steal authentication credentials.

Cryptography mitigates these risks by ensuring that only authorized parties can access or verify information.

---

## Core Security Objectives

Modern cryptographic systems are designed to achieve one or more of the following security objectives.

### Confidentiality

Confidentiality ensures that information can only be accessed by authorized parties.

This is achieved through **encryption**, which converts readable data into an unreadable format that requires a cryptographic key to recover.

---

### Integrity

Integrity guarantees that data has not been altered during storage or transmission.

Rather than encrypting data, integrity is commonly provided through **cryptographic hash functions**, which generate a unique fingerprint of the original data.

---

### Authentication

Authentication verifies the identity of users, devices, or services before communication begins.

Modern authentication mechanisms frequently rely on digital certificates, digital signatures, passwords, cryptographic keys, or challenge-response protocols.

---

### Non-Repudiation

Non-repudiation prevents an individual from denying that they performed a particular action.

This property is typically achieved through **digital signatures**, which provide verifiable proof that a specific private key was used to sign data.

---

## Plaintext and Ciphertext

Cryptographic operations transform information between two forms.

**Plaintext** is the original, human-readable information.

**Ciphertext** is the encrypted version of that information, which appears random and cannot be interpreted without the appropriate cryptographic key.

Encryption converts plaintext into ciphertext, while decryption performs the reverse operation.

---

## Basic Cryptographic Operations

Many cryptographic algorithms rely on simple mathematical operations that provide useful security properties.

### XOR (Exclusive OR)

XOR is a bitwise operation that outputs `1` when two bits differ and `0` when they are equal. One of its most important properties is reversibility:

Plaintext XOR Key = Ciphertext
Ciphertext XOR Key = Plaintext

This makes XOR a fundamental building block of stream ciphers and many modern cryptographic algorithms.

### Modular Arithmetic

Modular arithmetic performs calculations using the remainder after division, causing numbers to "wrap around" within a fixed range.

Examples:

- 17 mod 5 = 2
- 25 mod 7 = 4

Modular arithmetic forms the mathematical foundation of many public-key algorithms, including RSA, Diffie-Hellman, and Elliptic Curve Cryptography.

---

## Encryption

Encryption protects the confidentiality of information by making data unreadable to unauthorized parties.

Modern encryption algorithms fall into two primary categories.

### Symmetric Encryption

Symmetric encryption uses the **same key** for both encryption and decryption.

Because both parties must possess the same secret key, secure key distribution is one of its primary challenges.

Advantages:

- Extremely fast.
- Efficient for encrypting large amounts of data.
- Commonly used for files, disks, databases, and network traffic.

Common algorithms include:

- AES
- ChaCha20

---

### Asymmetric Encryption

Asymmetric encryption uses a **pair of mathematically related keys**:

- Public Key
- Private Key

The public key can be shared openly, while the private key must remain secret.

Data encrypted with one key can only be decrypted using the other.

Asymmetric cryptography enables secure key exchange, digital signatures, and authentication without requiring both parties to share a secret beforehand.

Common algorithms include:

- RSA (encryption and digital signatures)
- Diffie-Hellman (secure key exchange)
- Elliptic Curve Cryptography (ECC)

---

## Cryptographic Keys

A **cryptographic key** is a value used by cryptographic algorithms to perform encryption, decryption, signing, or verification.

The security of a cryptographic system depends far more on protecting its keys than on hiding the encryption algorithm itself.

Modern cryptographic systems assume that algorithms are publicly known, while only the keys remain secret.

---

## Cryptographic Hash Functions

A **cryptographic hash function** transforms data of any size into a fixed-length value known as a **hash** or **digest**.

Unlike encryption, hashing is **one-way**. The original data cannot feasibly be reconstructed from its hash.

An effective cryptographic hash function should:

- Always produce the same output for identical input.
- Produce significantly different outputs from minor input changes.
- Be computationally infeasible to reverse.
- Resist collisions.

Hashing is commonly used for:

- Password storage.
- File integrity verification.
- Digital signatures.
- Malware detection.

Common algorithms include:

- SHA-256
- SHA-384
- SHA-512
- SHA-3

Important properties include:

- Deterministic output
- Fixed-length output
- Avalanche effect
- Pre-image resistance
- Collision resistance

Algorithms such as **MD5** and **SHA-1** are considered cryptographically broken and should no longer be used for security-sensitive purposes.

---

## Password Hashing

Passwords should never be stored in plaintext.

Instead, systems store salted password hashes. During authentication, the entered password is hashed again and compared with the stored value.

Modern password hashing algorithms intentionally require significant computational resources to slow down brute-force attacks.

Common password hashing algorithms include:

- bcrypt
- scrypt
- Argon2

---

## Password Cracking

Password-cracking tools attempt to recover plaintext passwords from hashes.

Rather than breaking cryptographic algorithms, these tools exploit weak or predictable passwords.

Common attack methods include:

- Dictionary attacks
- Brute-force attacks
- Rule-based attacks

Popular tools include:

- John the Ripper
- Hashcat

---

## Digital Signatures

A **digital signature** provides proof that data originated from a specific entity and has not been modified.

Unlike handwritten signatures, digital signatures rely on asymmetric cryptography.

The sender signs data using their **private key**, while recipients verify the signature using the corresponding **public key**.

Digital signatures provide:

- Authentication
- Integrity
- Non-repudiation

---

## Public Key Infrastructure (PKI)

A **Public Key Infrastructure (PKI)** is the collection of technologies, policies, and procedures used to manage public-key cryptography at scale.

A PKI enables organizations to distribute, validate, renew, and revoke digital certificates securely.

Core PKI components include:

- Certificate Authorities (CAs)
- Registration Authorities (RAs)
- Digital Certificates
- Certificate Revocation Lists (CRLs)
- Online Certificate Status Protocol (OCSP)

PKI forms the trust foundation of secure Internet communications.

---

## Digital Certificates

A **digital certificate** binds a public key to the identity of a user, server, or organization.

Certificates are digitally signed by a trusted **Certificate Authority (CA)**, allowing clients to verify that a public key genuinely belongs to the claimed entity.

Certificates are widely used by:

- HTTPS
- TLS
- VPNs
- Code signing
- Email encryption

---

## Cryptography in Network Security

Cryptography secures nearly every modern network protocol.

Some common examples include:

| Technology | Purpose |
|------------|---------|
| [[HTTPS]] | Encrypts web traffic using TLS. |
| SSH | Secure remote administration. |
| TLS | Encrypts application-layer communication. |
| VPN | Creates encrypted tunnels across untrusted networks. |
| WPA2/WPA3 | Protect wireless network communications. |

Without cryptography, secure communication across the Internet would not be possible.

---

## Common Algorithms

| Algorithm | Purpose |
|-----------|---------|
| AES | Symmetric encryption |
| ChaCha20 | Symmetric encryption |
| RSA | Asymmetric encryption |
| ECC | Asymmetric encryption |
| SHA-2 | Cryptographic hashing |
| SHA-3 | Cryptographic hashing |

Each algorithm is designed for specific use cases, balancing security, performance, and computational requirements.

---

## Common Applications

Cryptography is integrated into countless modern technologies, including:

- HTTPS
- VPNs
- SSH
- Password managers
- Disk encryption
- Secure messaging
- Digital signatures
- Software updates
- Online banking
- Cryptocurrencies
- Multi-factor authentication
- Public Key Infrastructure (PKI)

---

## Related Notes

- [[HTTPS]]
- [[TCP-IP]]
- [[Operating-Systems]]
- [[Defensive-Security]]
- [[Offensive-Security]]

---

## Key Takeaways

- Cryptography protects information using mathematical algorithms and cryptographic keys.
- Its primary objectives are confidentiality, integrity, authentication, and non-repudiation.
- Encryption protects confidentiality, while hashing protects integrity.
- Symmetric encryption uses a single shared key, whereas asymmetric encryption uses a public/private key pair.
- Digital signatures verify authenticity and integrity while providing non-repudiation.
- PKI and digital certificates establish trust between communicating parties.
- Cryptography underpins modern cybersecurity and secures technologies such as HTTPS, SSH, VPNs, and digital authentication.