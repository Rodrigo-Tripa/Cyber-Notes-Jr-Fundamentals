# HyperText Transfer Protocol Secure (HTTPS)

## Overview

**HTTPS (HyperText Transfer Protocol Secure)** is the secure version of HTTP. It combines HTTP with **Transport Layer Security (TLS)** to provide encrypted communication between clients and web servers.

HTTPS protects sensitive information from interception, modification, and impersonation attacks, making it the standard protocol for modern websites.

## Transport Layer Security (TLS)

TLS establishes an encrypted connection before HTTP data is exchanged. It provides:

- Confidentiality through encryption.
- Integrity by detecting data modification.
- Authentication using digital certificates.

## Digital Certificates

A **digital certificate** verifies the identity of a website or service. Certificates contain the server's public key and are digitally signed by a trusted **Certificate Authority (CA)**.

Web browsers validate certificates before establishing secure communications, helping prevent impersonation attacks.

## TLS Interception

Under normal circumstances, HTTPS prevents third parties from reading or modifying encrypted traffic. However, an **intercepting proxy** such as Burp Suite can inspect HTTPS traffic by performing a controlled **Man-in-the-Middle (MITM)** operation.

When HTTPS interception is enabled:

1. The browser sends a request to the proxy.
2. The proxy establishes its own TLS connection with the target server.
3. The proxy generates a new certificate for the requested domain.
4. The browser accepts this certificate because it trusts the proxy's installed Certificate Authority (CA).
5. The proxy decrypts, inspects, and optionally modifies the traffic before forwarding it to the destination server.

This process allows security testers to analyse encrypted HTTP traffic while maintaining encrypted communication on both sides of the connection.

## TLS Handshake

Before encrypted communication begins, the client and server perform a **TLS Handshake**, during which they:

1. Negotiate the TLS version and encryption algorithms.
2. Verify the server's certificate.
3. Exchange cryptographic information.
4. Generate a shared session key used for symmetric encryption.

## Public Key Infrastructure (PKI)

HTTPS relies on a **Public Key Infrastructure (PKI)**, which consists of Certificate Authorities, digital certificates, and cryptographic key pairs used to establish trust between communicating parties.

## Benefits

HTTPS provides:

- Encrypted communication.
- Server authentication.
- Data integrity.
- Protection against eavesdropping.
- Protection against man-in-the-middle attacks.

## HTTPS and Security Testing

Because HTTPS encrypts communication, packet capture tools alone cannot inspect application-layer traffic without access to the encryption keys. Web security testing therefore commonly relies on **intercepting proxies**, which terminate and recreate TLS connections to allow requests and responses to be analysed.

This enables security testers to:

- Inspect encrypted HTTP requests and responses.
- Modify request parameters and headers.
- Analyse cookies and authentication tokens.
- Replay requests multiple times.
- Identify vulnerabilities in web applications.

Common HTTPS interception tools include:

- Burp Suite
- OWASP ZAP
- mitmproxy

HTTPS interception should only be performed on systems for which explicit authorization has been granted.

## Goal

HTTPS secures web communication by combining HTTP with TLS, ensuring that data exchanged between clients and servers remains private, authentic, and resistant to tampering.