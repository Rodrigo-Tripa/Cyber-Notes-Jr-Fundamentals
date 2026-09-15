#networking #traffic-analysis #packet-analysis #wireshark #pcap

# Wireshark

## Overview

Wireshark is the world's most widely used network protocol analyzer. It captures, decodes, and displays network traffic, allowing analysts to inspect communications between devices at every layer of the networking stack.

Unlike scanners such as [[Cyber-Notes-Jr-Fundamentals/07-Tools/Nmap]], which actively send packets to gather information about remote systems, Wireshark is primarily a **passive analysis tool**. It observes existing traffic without interacting with the network, making it invaluable for troubleshooting, incident response, malware analysis, protocol debugging, and forensic investigations.

Wireshark can analyze both live network traffic and previously captured packet capture (PCAP) files, providing detailed visibility into how devices communicate.

---

## How Wireshark Works

When capturing traffic, Wireshark relies on packet capture libraries such as:

- libpcap (Linux/macOS)
- Npcap (Windows)

These libraries place the selected network interface into a mode that allows packets traversing the network to be copied to Wireshark for analysis.

Captured packets are then decoded according to hundreds of supported protocols, presenting the information in a human-readable format.

---

## Packet Analysis

Each captured packet contains multiple protocol layers.

For example:

```
Ethernet
└── IPv4
    └── TCP
        └── HTTP
```

Wireshark automatically dissects every protocol layer, allowing analysts to inspect individual fields without manually decoding packet bytes.

This layered view follows the encapsulation model used throughout computer networks.

See also:

- [[OSI-Model]]
- [[TCP-IP]]
- [[Packets-and-Frames]]

---

## Interface Layout

The Wireshark interface is divided into three primary panes.

### Packet List

Displays every captured packet with summary information, including:

- Timestamp
- Source address
- Destination address
- Protocol
- Packet length
- Short description

Each row represents a single captured packet.

---

### Packet Details

Displays the protocol hierarchy for the selected packet.

Each protocol layer can be expanded to inspect individual header fields such as:

- MAC addresses
- IP addresses
- TCP flags
- Sequence numbers
- HTTP headers

---

### Packet Bytes

Displays the raw packet contents in hexadecimal and ASCII.

This allows low-level inspection of packet data and verification of protocol decoding.

---

## Packet Capture

Wireshark can capture traffic from:

- Ethernet
- Wi-Fi
- Loopback interfaces
- VPN interfaces
- Virtual machines
- Containers

Captured traffic may be viewed in real time or saved for later analysis.

---

## PCAP Files

Packet captures are commonly stored using the PCAP or PCAPNG formats.

These files preserve captured packets exactly as they appeared on the network and can later be reopened for analysis.

PCAP files are widely used in:

- Digital forensics
- Malware analysis
- Incident response
- Threat hunting
- Capture-the-Flag challenges
- Security training

---

## Display Filters

Display Filters determine **which packets are shown** inside Wireshark without modifying the capture itself.

Examples include:

- HTTP traffic
- DNS requests
- TCP packets
- Traffic from a specific IP address
- Traffic to a specific port

Filtering allows analysts to isolate relevant communications from very large captures.

> Display filters do **not** discard packets. They only control what is displayed.

---

## Following Streams

Wireshark can reconstruct complete conversations between hosts.

Examples include:

- TCP Streams
- HTTP conversations
- TLS handshakes
- Telnet sessions

Following streams allows analysts to inspect application-layer communications without manually reassembling packets.

---

## Common Use Cases

Wireshark is commonly used for:

- Network troubleshooting
- Security monitoring
- Malware analysis
- Incident response
- Digital forensics
- Protocol debugging
- Application development
- Network performance analysis

---

## Advantages

- Supports thousands of protocols
- Deep packet inspection
- Live capture
- Offline PCAP analysis
- Powerful filtering capabilities
- Cross-platform
- Free and open source

---

## Limitations

Wireshark cannot:

- Discover hosts on its own
- Scan ports
- Exploit vulnerabilities
- Intercept encrypted traffic without the required keys
- Recover packets that were never captured

It is an analysis tool, not an offensive security tool.

---

## Related Notes

- [[TCP-IP]]
- [[OSI-Model]]
- [[Packets-and-Frames]]
- [[Networking-Basics]]
- [[Ports]]
- [[Cyber-Notes-Jr-Fundamentals/07-Tools/Nmap]]
- [[Tcpdump]]