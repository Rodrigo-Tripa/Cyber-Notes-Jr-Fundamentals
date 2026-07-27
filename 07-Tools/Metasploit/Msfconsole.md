#tool #metasploit #msfconsole #pentesting

# Msfconsole

## Overview

**msfconsole** is the primary command-line interface of the Metasploit Framework. It provides access to every major feature of the framework, including module management, exploitation, payload configuration, session management, database interaction, and post-exploitation.

Nearly all penetration testing activities performed within Metasploit begin inside `msfconsole`.

---

## Core Workflow

The typical workflow inside `msfconsole` consists of:

1. Search for a module.
2. Select the desired module.
3. Review its documentation.
4. Configure required options.
5. Select or modify the payload.
6. Execute the module.
7. Interact with the resulting session.

---

## Searching for Modules

Modules can be located using flexible search filters.

Examples include:

- Module name
- CVE identifier
- Platform
- Service
- Author
- Module type

Searching before exploiting helps identify the most appropriate module for the detected target.

---

## Module Management

After selecting a module, its documentation should always be reviewed.

Important information includes:

- Description
- Supported targets
- References
- Required options
- Available payloads
- Reliability
- Side effects

Understanding the module is essential before executing it against a target.

---

## Module Configuration

Each module exposes configurable parameters.

Common options include:

- Target host
- Target port
- Payload
- Local host
- Local port
- Target URI

Modules cannot execute until all required parameters have been configured.

---

## Sessions

Successful exploitation usually creates a session.

Sessions allow interaction with compromised systems and may provide:

- Shell access
- Meterpreter sessions
- Command execution
- File management
- Post-exploitation capabilities

Multiple sessions can be managed simultaneously from within `msfconsole`.

---

## Jobs

Long-running modules may execute as background jobs.

Jobs continue running independently of the current console, allowing multiple operations to occur simultaneously without interrupting user interaction.

---

## Database Integration

When connected to a database, `msfconsole` can automatically store information collected during engagements, including:

- Hosts
- Services
- Credentials
- Vulnerabilities
- Loot
- Notes

This information can later be reused by other modules, simplifying large penetration tests.

See [[Workspaces]].

---

## Resource Scripts

Resource scripts automate repetitive tasks by executing predefined sequences of Metasploit commands.

They are commonly used to:

- Configure listeners.
- Launch multiple modules.
- Standardize engagements.
- Automate demonstrations and labs.

---

## Best Practices

- Enumerate before exploiting.
- Read module documentation before execution.
- Verify target compatibility.
- Use the least intrusive module capable of validating a vulnerability.
- Keep sessions organized.
- Document every action performed during an engagement.

---

## Related Notes

- [[Metasploit]]
- [[Modules]]
- [[Payloads]]
- [[Meterpreter]]
- [[Msfvenom]]
- [[Workspaces]]