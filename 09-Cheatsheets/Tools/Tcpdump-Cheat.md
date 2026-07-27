#tool #cheatsheet #tcpdump #network #packet-capture

# Tcpdump Cheat Sheet

TCPdump is a command-line packet analyzer used to capture and inspect network traffic. It is commonly used for network troubleshooting, protocol analysis, and packet collection before opening captures in Wireshark.

---

# Basic Syntax

```bash
tcpdump [OPTIONS] [FILTER]
```

Examples:

```bash
tcpdump -i eth0

tcpdump port 80

tcpdump host 10.10.10.10
```

---

# Most Important Options

| Option | Description | When to Use |
|---------|-------------|-------------|
| `-i <interface>` | Capture on a specific interface | Select the network interface to monitor. |
| `-A` | Display packets as ASCII | Inspect HTTP requests or other plaintext protocols. |
| `-X` | Display packets in hexadecimal and ASCII | Analyze packet contents in detail. |
| `-n` | Don't resolve hostnames | Faster output and avoids DNS lookups. |
| `-nn` | Don't resolve hostnames or ports | Shows raw IP addresses and port numbers. |
| `-v` | Verbose output | Display additional packet information. |
| `-vv` | More verbose output | Display even more protocol details. |
| `-c <count>` | Capture a specific number of packets | Useful for short captures. |
| `-w <file>` | Save packets to a PCAP file | Analyze later in Wireshark. |
| `-r <file>` | Read packets from a PCAP file | Review previously captured traffic. |

---

# Common Filters

| Filter | Description | Example |
|--------|-------------|---------|
| `host` | Traffic to or from a host | `host 10.10.10.10` |
| `src host` | Source host | `src host 10.10.10.10` |
| `dst host` | Destination host | `dst host 10.10.10.10` |
| `port` | Specific port | `port 80` |
| `src port` | Source port | `src port 53` |
| `dst port` | Destination port | `dst port 443` |
| `net` | Entire network | `net 192.168.1.0/24` |
| `tcp` | TCP packets only | `tcp` |
| `udp` | UDP packets only | `udp` |
| `icmp` | ICMP traffic | `icmp` |
| `arp` | ARP traffic | `arp` |

---

# Common Workflows

## Capture Traffic

```bash
tcpdump -i eth0
```

Capture all traffic on an interface.

---

## Capture a Limited Number of Packets

```bash
tcpdump -i eth0 -c 100
```

Stop automatically after capturing 100 packets.

---

## Capture HTTP Traffic

```bash
tcpdump -i eth0 tcp port 80
```

Monitor HTTP traffic.

---

## Capture HTTPS Traffic

```bash
tcpdump -i eth0 tcp port 443
```

Monitor encrypted HTTPS connections.

---

## Capture DNS Traffic

```bash
tcpdump -i eth0 port 53
```

Inspect DNS queries and responses.

---

## Capture ICMP (Ping)

```bash
tcpdump icmp
```

Monitor ping requests and replies.

---

## Capture Traffic From One Host

```bash
tcpdump host 10.10.10.10
```

Capture all traffic involving the specified host.

---

## Save Capture

```bash
tcpdump -i eth0 -w capture.pcap
```

Save packets for later analysis.

---

## Read a Capture

```bash
tcpdump -r capture.pcap
```

Display packets stored in a PCAP file.

---

# Advanced Examples

## Capture without DNS Resolution

```bash
tcpdump -nn -i eth0
```

Displays raw IP addresses and port numbers.

---

## Capture Only SYN Packets

```bash
tcpdump 'tcp[tcpflags] & tcp-syn != 0'
```

Useful for identifying connection attempts.

---

## Capture Traffic Between Two Hosts

```bash
tcpdump host 10.10.10.10 and host 10.10.10.20
```

---

## Capture Everything Except SSH

```bash
tcpdump not port 22
```

Reduces noise while maintaining the SSH session.

---

## Capture Multiple Ports

```bash
tcpdump 'port 80 or port 443'
```

Monitor HTTP and HTTPS simultaneously.

---

## Capture Packets Larger Than 500 Bytes

```bash
tcpdump greater 500
```

Useful for identifying large transfers.

---

## Display Packet Contents

```bash
tcpdump -X -i eth0
```

Shows packets in hexadecimal and ASCII.

---

## Capture and Write to a File

```bash
tcpdump -i eth0 -nn -w traffic.pcap
```

Ideal for later analysis with Wireshark.

---

# Typical Workflow

```text
1. Select the network interface
2. Apply capture filters
3. Capture traffic
4. Save packets to a PCAP file
5. Analyze the capture using TCPdump or Wireshark
```

Typical commands:

```bash
tcpdump -i eth0

tcpdump -nn -i eth0

tcpdump host 10.10.10.10

tcpdump port 80

tcpdump -i eth0 -w capture.pcap

tcpdump -r capture.pcap
```

---

# Commands You'll Use Most

```bash
tcpdump -i eth0

tcpdump -nn -i eth0

tcpdump host <ip>

tcpdump port <port>

tcpdump -w capture.pcap

tcpdump -r capture.pcap

tcpdump -X -i eth0
```