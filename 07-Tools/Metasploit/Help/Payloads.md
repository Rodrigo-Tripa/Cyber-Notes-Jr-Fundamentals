#tool #metasploit #payloads

# Payloads

## Overview

A **payload** is the code executed on a target after a vulnerability has been successfully exploited. While an exploit provides the initial entry point, the payload determines what actions can be performed once code execution has been achieved.

Metasploit provides hundreds of payloads designed for different operating systems, architectures, communication methods, and post-exploitation objectives.

---

## Payload Categories

### Singles

Single (or **stageless**) payloads contain all required functionality in a single executable component.

Advantages include:

- Simpler execution
- No secondary download stage
- Better compatibility in restricted environments

---

### Staged

Staged payloads execute in multiple phases.

The first stage establishes communication with the attacker before downloading and executing the remaining payload.

This approach allows larger and more flexible payloads while keeping the initial stage relatively small.

---

## Common Payload Types

Some of the most frequently used payloads include:

- Command Shell
- Meterpreter
- Reverse TCP
- Reverse HTTP
- Reverse HTTPS
- Bind TCP

Each payload is designed for different objectives and network environments.

---

## Payload Selection

Choosing the correct payload depends on several factors:

- Target operating system
- Target architecture
- Available network connectivity
- Firewall restrictions
- Desired level of interaction
- Operational security requirements

Selecting an incompatible payload will usually cause the exploitation attempt to fail.

---

## Related Notes

- [[Metasploit]]
- [[Msfvenom]]
- [[Meterpreter]]
- [[Modules]]