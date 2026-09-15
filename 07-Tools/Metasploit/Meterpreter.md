#tool #metasploit #meterpreter #post-exploitation

# Meterpreter

## Overview

**Meterpreter** is Metasploit's advanced in-memory payload designed for post-exploitation. Unlike a traditional shell, Meterpreter runs entirely in memory and communicates with the attacker through an encrypted channel, providing a powerful environment for interacting with compromised systems without relying solely on native operating system commands.

Meterpreter is modular, meaning additional functionality can be loaded during an active session without reconnecting to the target. It is one of the most widely used payloads during penetration tests because it combines remote administration, information gathering, privilege escalation, and post-exploitation into a single interface.

---

## Architecture

After a successful exploitation, the Meterpreter payload establishes a communication channel with the attacker.

Unlike a standard shell, Meterpreter:

- Executes in memory.
- Avoids writing executables to disk whenever possible.
- Supports encrypted communication.
- Loads extensions dynamically.
- Integrates directly with the Metasploit Framework.

This architecture provides significantly more functionality than a basic reverse shell.

---

## Capabilities

Meterpreter provides a wide range of post-exploitation features, including:

- System information gathering
- User enumeration
- Process management
- File upload and download
- Directory navigation
- Command execution
- Network enumeration
- Privilege escalation assistance
- Credential extraction
- Screenshot capture
- Keylogging
- Registry interaction
- Token impersonation

These capabilities allow an operator to perform most post-exploitation activities without leaving the Meterpreter environment.

---

## Session Management

A Meterpreter session remains active after exploitation and can be managed directly through Metasploit.

Sessions can be:

- Backgrounded
- Resumed
- Upgraded
- Migrated into another process
- Closed

Managing sessions efficiently is essential when multiple hosts have been compromised during an engagement.

---

## Extensions

Meterpreter supports dynamically loaded extensions that add new functionality.

Common extensions include:

- **Stdapi** – Standard filesystem, process, and network operations.
- **Kiwi** – Credential extraction and Kerberos interaction.
- **Priv** – Privilege-related functionality.

Extensions allow Meterpreter to remain lightweight while exposing advanced capabilities only when required.

---

## Operational Security

Although Meterpreter reduces its forensic footprint by executing in memory, it is **not invisible**.

Modern Endpoint Detection and Response (EDR) solutions can detect Meterpreter through:

- Memory analysis
- Process injection detection
- Behavioral monitoring
- Network traffic inspection
- Command execution patterns

Operators should therefore consider Meterpreter a productivity tool rather than a stealth mechanism.

---

## Best Practices

- Enumerate before making changes.
- Escalate privileges only when necessary.
- Migrate to stable processes when appropriate.
- Avoid unnecessary persistence mechanisms.
- Collect only the information required for the engagement.
- Document every post-exploitation action.

---

## Related Notes

- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Metasploit]]
- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Msfconsole]]
- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Help/Payloads]]
- [[Modules]]
- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Msfvenom]]