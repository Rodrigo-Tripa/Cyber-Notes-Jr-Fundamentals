#tool #metasploit #msfvenom #payloads

# Msfvenom

## Overview

**Msfvenom** is Metasploit's payload generation utility. It combines the functionality of the former `msfpayload` and `msfencode` tools into a single command-line application capable of generating payloads for multiple operating systems, architectures, and output formats.

Rather than exploiting vulnerabilities itself, Msfvenom creates payloads that can later be delivered through exploits, social engineering attacks, malicious documents, or other delivery mechanisms.

---

## Purpose

Msfvenom is primarily used to:

- Generate payloads for different operating systems.
- Select communication methods between the target and attacker.
- Produce payloads in various executable formats.
- Encode payloads when required.
- Customize payload parameters before deployment.

It is commonly used during penetration tests, red team engagements, and security research.

---

## Payload Types

Msfvenom supports several categories of payloads.

### Singles

A **single payload** (also called **stageless**) contains all required functionality within one executable component.

Advantages include:

- Simpler execution.
- No secondary download stage.
- Better compatibility in restricted environments.

---

### Staged

A **staged payload** consists of two components.

The first stage establishes communication with the attacker, while the second stage downloads and executes the remaining payload.

Advantages include:

- Smaller initial payload.
- Greater flexibility.
- Ability to deliver larger payloads after exploitation.

---

## Communication Methods

Payloads may establish communication using different techniques.

The most common include:

- Reverse TCP
- Reverse HTTP
- Reverse HTTPS
- Bind TCP

The selected communication method depends on the target environment, firewall restrictions, and engagement objectives.

---

## Output Formats

Msfvenom can generate payloads for numerous operating systems and file formats.

Examples include:

- Windows executables
- Linux ELF binaries
- macOS binaries
- ASP
- JSP
- PHP
- Python
- PowerShell
- Raw shellcode

The generated format must match both the target operating system and the intended delivery method.

---

## Encoders

Msfvenom supports payload encoders that transform payload bytes without changing their functionality.

Historically, encoders were used to avoid problematic characters or bypass simple signature-based antivirus detection.

Today, modern endpoint protection solutions generally detect malicious behavior regardless of encoding, making encoders unsuitable as a reliable evasion technique.

---

## Limitations

Generating a payload does not guarantee successful exploitation.

The payload must:

- Match the target architecture.
- Match the operating system.
- Be compatible with the selected exploit.
- Successfully evade or bypass security controls where applicable.

Incorrect payload selection is one of the most common causes of failed exploitation attempts.

---

## Related Notes

- [[Metasploit]]
- [[Payloads]]
- [[Meterpreter]]
- [[Msfconsole]]