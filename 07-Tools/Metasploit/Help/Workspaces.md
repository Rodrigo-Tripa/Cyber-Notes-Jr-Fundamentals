#tool #metasploit #database

# Workspaces

## Overview

A **workspace** is a logical container used by the Metasploit Framework to organize information collected during a penetration test. Workspaces separate engagements from one another, preventing hosts, services, credentials, and vulnerabilities from becoming mixed across different projects.

They are particularly valuable during larger assessments involving multiple targets or clients.

---

## Stored Information

A workspace can store information such as:

- Hosts
- Open ports
- Running services
- Operating systems
- Vulnerabilities
- Credentials
- Loot
- Notes
- Active sessions

This information can be reused by Metasploit modules throughout an engagement.

---

## Benefits

Using workspaces provides several advantages:

- Separates multiple engagements.
- Keeps collected information organized.
- Reduces repeated enumeration.
- Simplifies reporting.
- Improves collaboration during larger assessments.

---

## Database Integration

Workspaces rely on Metasploit's database functionality.

When database support is enabled, information discovered through scans, exploits, and post-exploitation modules is automatically stored and can be queried later without repeating previous work.

---

## Related Notes

- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Metasploit]]
- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Metasploit/Msfconsole]]
- [[Modules]]