#tool #cheatsheet #wireshark #packet-analysis #networking

# Wireshark Cheat Sheet

Wireshark is a graphical network protocol analyzer used to inspect captured network traffic. It is commonly used during network troubleshooting, malware analysis, incident response, and penetration testing.

---

# Basic Workflow

```text
1. Select a network interface
2. Start capturing packets
3. Apply display filters
4. Follow streams
5. Inspect protocols
6. Export or save the capture
```

---

# Capture vs Display Filters

| Type | Purpose | Example |
|------|---------|---------|
| Capture Filter | Limits what is captured | `port 80` |
| Display Filter | Filters packets already captured | `http` |

> Capture Filters use **BPF syntax** (same as TCPdump).
>
> Display Filters use **Wireshark syntax**.

---

# Most Useful Display Filters

## IP Addresses

```text
ip.addr == 10.10.10.10
ip.src == 10.10.10.10
ip.dst == 10.10.10.10
```

---

## TCP / UDP

```text
tcp
udp

tcp.port == 80
udp.port == 53

tcp.srcport == 443
tcp.dstport == 22
```

---

## Common Protocols

```text
http
https
tls
dns
icmp
arp
ftp
ssh
smtp
imap
pop
dhcp
ntp
```

---

## HTTP

```text
http.request

http.response

http.request.method == "GET"

http.request.method == "POST"

http.host

http.user_agent

http contains "password"
```

---

## DNS

```text
dns

dns.flags.response == 0

dns.flags.response == 1

dns.qry.name

dns.qry.name contains "google"
```

---

## TLS / HTTPS

```text
tls

tls.handshake

tls.handshake.type == 1

tls.handshake.type == 2
```

---

## TCP Analysis

```text
tcp.flags.syn == 1

tcp.flags.ack == 1

tcp.flags.reset == 1

tcp.analysis.retransmission

tcp.analysis.lost_segment

tcp.analysis.duplicate_ack
```

---

## Search for Text

```text
frame contains "admin"

frame contains "password"

http contains "login"
```

---

# Operators

| Operator | Meaning |
|----------|---------|
| `==` | Equals |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `contains` | Contains text |
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

Example:

```text
http && ip.addr == 10.10.10.10

tcp.port == 80 || tcp.port == 443

dns && ip.src == 10.10.10.5
```

---

# Most Useful Capture Filters

```text
host 10.10.10.10

src host 10.10.10.10

dst host 10.10.10.10

port 80

tcp

udp

icmp

arp

net 192.168.1.0/24

port 80 or port 443

not port 22
```

---

# Essential Features

## Follow TCP Stream

```
Right Click → Follow → TCP Stream
```

Reconstructs an entire TCP conversation, making it easy to read HTTP requests, responses, credentials, and other transmitted data.

---

## Follow UDP Stream

```
Right Click → Follow → UDP Stream
```

Displays all packets belonging to the same UDP conversation.

---

## Statistics

```
Statistics → Conversations
```

Shows communication between hosts.

---

```
Statistics → Endpoints
```

Lists all discovered IP and MAC addresses.

---

```
Statistics → Protocol Hierarchy
```

Shows protocol distribution within the capture.

---

```
Statistics → IO Graphs
```

Visualizes network traffic over time.

---

## Expert Information

```
Analyze → Expert Information
```

Highlights warnings, errors, retransmissions and suspicious packets.

---

## Export Objects

```
File → Export Objects
```

Extract files transferred over:

- HTTP
- SMB
- TFTP
- DICOM

Useful for malware analysis and forensic investigations.

---

# Coloring Rules

Wireshark automatically colors packets to make analysis easier.

Common examples:

- TCP
- UDP
- HTTP
- DNS
- Errors
- Retransmissions

---

# Advanced Examples

## Find Failed Connections

```text
tcp.flags.reset == 1
```

---

## Find Retransmissions

```text
tcp.analysis.retransmission
```

---

## Show Only HTTP Requests

```text
http.request
```

---

## Show DNS Queries

```text
dns.flags.response == 0
```

---

## Show Only Traffic To or From a Host

```text
ip.addr == 10.10.10.10
```

---

## Find Login Requests

```text
http.request.method == "POST"
```

---

## Search for Passwords

```text
frame contains "password"
```

---

## Find SSH Traffic

```text
ssh
```

---

## Find Large Packets

```text
frame.len > 1000
```

---

## Combine Filters

```text
http && ip.addr == 10.10.10.10

dns && udp.port == 53

tcp.port == 443 && tls
```

---

# Typical Investigation Workflow

```text
1. Open the capture
2. Identify the main protocols
3. Filter the interesting traffic
4. Follow streams
5. Inspect suspicious packets
6. Export transferred files if needed
7. Review Expert Information
```

---

# Filters You'll Use Most

```text
ip.addr == <IP>

tcp.port == <PORT>

http

dns

tls

icmp

http.request

frame contains "<TEXT>"

tcp.analysis.retransmission

tcp.flags.reset == 1

http.request.method == "POST"
```