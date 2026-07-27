#tool #metasploit #modules

# Modules

## Overview

A **module** is a reusable component that provides a specific capability within the Metasploit Framework. Every action performed in Metasploit, from scanning a target to exploiting a vulnerability or performing post-exploitation, is executed through a module.

This modular architecture allows new functionality to be added without modifying the core framework and provides a consistent interface regardless of the module type.

---

## Module Types

### Auxiliary

Auxiliary modules perform tasks that do not require exploitation.

Common uses include:

- Service enumeration
- Vulnerability scanning
- Banner grabbing
- Brute-force attacks
- Protocol testing

---

### Exploit

Exploit modules take advantage of known vulnerabilities to obtain code execution on a target system.

Most exploit modules require a compatible payload to be selected before execution.

---

### Payload

Payload modules define the code executed after a successful exploitation.

They determine what level of access the attacker receives, such as a command shell or a Meterpreter session.

See [[Payloads]].

---

### Post

Post modules automate tasks performed after obtaining access to a target.

Typical functions include:

- System enumeration
- Credential collection
- Privilege escalation checks
- Persistence
- Evidence gathering

These modules operate against existing sessions rather than exploiting new vulnerabilities.

---

### Encoder

Encoders transform payloads while preserving their functionality.

Although historically useful for avoiding problematic characters and bypassing basic antivirus signatures, they are generally ineffective against modern security solutions.

---

### NOP

NOP (No Operation) modules generate instruction sequences that perform no action.

They are primarily used during exploit development to improve payload reliability and are rarely used directly during penetration testing.

---

## Related Notes

- [[Metasploit]]
- [[Msfconsole]]
- [[Payloads]]
- [[Meterpreter]]