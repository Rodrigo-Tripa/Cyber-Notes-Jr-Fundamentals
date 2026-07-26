#tool #cheatsheet #nmap #reconnaissance #network-scanning

# Nmap Cheat Sheet

Nmap (Network Mapper) is a network scanning tool used to discover hosts, identify open ports, detect running services, fingerprint operating systems, and perform service enumeration. It is one of the first tools used during the reconnaissance phase of a penetration test or CTF.

---

# Basic Syntax

```bash
nmap [OPTIONS] <target>
```

Examples:

```bash
nmap 10.10.10.10
nmap scanme.nmap.org
nmap 192.168.1.0/24
```

---

# Most Important Options

| Option | Description | When to Use |
|---------|-------------|-------------|
| `-sS` | TCP SYN (Stealth) Scan | Default TCP scan when running with privileges. Fast and less detectable. |
| `-sT` | TCP Connect Scan | Use when SYN scans are unavailable (no root privileges). |
| `-sU` | UDP Scan | Scan UDP services such as DNS, SNMP, DHCP or TFTP. |
| `-sV` | Service Version Detection | Identify software and versions running on open ports. |
| `-O` | OS Detection | Attempt to identify the target operating system. |
| `-A` | Aggressive Scan | Enables OS detection, version detection, default scripts and traceroute. |
| `-Pn` | Skip Host Discovery | Assume the host is online even if ping fails. |
| `-p <ports>` | Scan Specific Ports | Scan only selected ports. |
| `-p-` | Scan All TCP Ports | Scan every TCP port (1-65535). |
| `-T4` | Faster Timing | Speed up scans on reliable networks. |
| `-sC` | Default NSE Scripts | Execute the default Nmap scripts. |
| `--script <name>` | Specific NSE Scripts | Execute selected NSE scripts or categories. |
| `-oN <file>` | Normal Output | Save human-readable results. |
| `-oA <name>` | All Output Formats | Save results as `.nmap`, `.xml`, and `.gnmap`. |

---

# Common Workflows

## Quick Scan

```bash
nmap 10.10.10.10
```

Scans the most common TCP ports.

---

## Full TCP Port Scan

```bash
nmap -p- 10.10.10.10
```

Scans every TCP port to avoid missing uncommon services.

---

## Service Enumeration

```bash
nmap -sC -sV 10.10.10.10
```

Runs the default NSE scripts while identifying service versions.

---

## Aggressive Enumeration

```bash
nmap -A 10.10.10.10
```

Performs deeper enumeration by combining version detection, OS detection, default scripts and traceroute.

---

## UDP Scan

```bash
nmap -sU 10.10.10.10
```

Useful for identifying UDP services such as DNS or SNMP.

---

## Vulnerability Scan

```bash
nmap --script vuln 10.10.10.10
```

Runs vulnerability detection scripts included with NSE.

---

# Common NSE Script Categories

| Category | Purpose |
|----------|---------|
| `default` | Safe scripts executed with `-sC`. |
| `safe` | Non-intrusive information gathering. |
| `discovery` | Host and service enumeration. |
| `auth` | Authentication-related checks. |
| `vuln` | Vulnerability detection. |
| `brute` | Brute-force authentication attempts. |
| `exploit` | Exploitation scripts. |

Example:

```bash
nmap --script vuln,safe 10.10.10.10
```

---

# Advanced Examples

## Scan all ports and detect services

```bash
nmap -p- -sV 10.10.10.10
```

---

## Discover live hosts only

```bash
nmap -sn 192.168.1.0/24
```

---

## Scan the 100 most common ports

```bash
nmap --top-ports 100 10.10.10.10
```

---

## Scan multiple hosts

```bash
nmap 10.10.10.10 10.10.10.20 10.10.10.30
```

---

## Scan an entire subnet

```bash
nmap 10.10.10.0/24
```

---

## Read targets from a file

```bash
nmap -iL targets.txt
```

---

## Exclude specific hosts

```bash
nmap 10.10.10.0/24 --exclude 10.10.10.5
```

---

## Scan specific ports

```bash
nmap -p 22,80,443 10.10.10.10
```

---

## Save results in all formats

```bash
nmap -oA initial_scan 10.10.10.10
```

---

## Enumerate HTTP services

```bash
nmap --script http-title,http-enum -p80,443 10.10.10.10
```

---

## Enumerate SMB

```bash
nmap --script smb-enum-shares,smb-enum-users -p445 10.10.10.10
```

---

## Scan IPv6

```bash
nmap -6 <IPv6-address>
```

---

# Typical Pentesting Workflow

```text
1. Discover live hosts
2. Scan all TCP ports
3. Detect service versions
4. Run default NSE scripts
5. Execute targeted NSE scripts
6. Save scan results
```

Typical commands:

```bash
nmap -sn 10.10.10.0/24

nmap -p- -T4 10.10.10.10

nmap -sC -sV -O -p <open-ports> 10.10.10.10

nmap --script vuln 10.10.10.10

nmap -oA final_scan 10.10.10.10
```

---

# Commands You'll Use Most

```bash
nmap -sC -sV <target>

nmap -p- <target>

nmap -A <target>

nmap -Pn <target>

nmap -oA scan <target>

nmap --script vuln <target>
```