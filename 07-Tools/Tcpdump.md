#networking #traffic-analysis #packet-analysis #tcpdump #pcap #cli

# Tcpdump

## Overview

Tcpdump is a command-line packet analyzer used to capture and inspect network traffic on Unix-like operating systems. Built on the **libpcap** library, it provides direct access to packets traversing a network interface, making it one of the most lightweight and efficient tools for network troubleshooting, incident response, and security analysis.

Unlike graphical analyzers such as [[Wireshark]], Tcpdump is designed for terminal-based environments, making it ideal for remote administration, servers without graphical interfaces, embedded systems, and automation scripts. It can capture live traffic, apply filters before packets are recorded, and save captures for later analysis.

---

## How Tcpdump Works

Tcpdump listens on a selected network interface and captures packets as they are transmitted or received.

It relies on the **libpcap** library to interact with the operating system's networking stack, allowing packets to be copied from the network interface into user space for inspection.

Captured packets can be displayed directly in the terminal or written to a packet capture file for offline analysis.

---

## Packet Capture

Tcpdump supports capturing traffic from various network interfaces, including:

- Ethernet
- Wi-Fi
- Loopback interfaces
- VPN interfaces
- Virtual network adapters
- Containers

Capturing traffic generally requires administrative or root privileges because packet capture operates at a low level within the networking stack.

---

## Berkeley Packet Filter (BPF)

One of Tcpdump's most powerful features is its support for **Berkeley Packet Filter (BPF)** expressions.

BPF filters determine **which packets are captured**, reducing unnecessary traffic before it reaches the application.

Filters can match traffic based on:

- Protocols
- Source and destination IP addresses
- Ports
- Networks
- Packet direction
- Boolean logic

Unlike display filters in [[Wireshark]], BPF filters operate during packet capture, making them significantly more efficient when monitoring busy networks.

---

## PCAP Files

Tcpdump can save captured traffic using the **PCAP** format.

Packet capture files preserve the original network traffic exactly as it was observed, allowing it to be reopened later for analysis using tools such as:

- [[Wireshark]]
- Tcpdump
- TShark
- Zeek
- NetworkMiner

This separation between packet capture and packet analysis is common during forensic investigations and incident response.

---

## Output Options

Tcpdump provides multiple ways to display captured packets.

Output can include:

- Packet timestamps
- Source and destination addresses
- Transport protocols
- Port numbers
- Packet length
- Verbose protocol information
- Raw hexadecimal data
- ASCII payloads

These options allow analysts to adjust the amount of detail according to the investigation.

---

## Common Use Cases

Tcpdump is commonly used for:

- Network troubleshooting
- Incident response
- Malware analysis
- Digital forensics
- Remote server diagnostics
- Performance monitoring
- Packet collection for later analysis

It is particularly valuable when working over SSH or on systems where graphical tools are unavailable.

---

## Tcpdump vs Wireshark

| Tcpdump | [[Wireshark]] |
|----------|---------------|
| Command-line interface | Graphical interface |
| Lightweight | Feature-rich |
| Excellent for remote systems | Excellent for interactive analysis |
| Uses BPF capture filters | Uses display filters and capture filters |
| Ideal for capturing traffic | Ideal for detailed packet inspection |

The two tools are often used together. Tcpdump captures traffic on remote systems, while Wireshark provides a more powerful environment for detailed analysis of the resulting PCAP files.

---

## Advantages

- Lightweight
- Fast
- Available on most Unix-like systems
- Excellent for automation
- Remote-friendly
- Supports BPF filtering
- Generates PCAP files compatible with many analysis tools

---

## Limitations

Tcpdump cannot:

- Discover hosts
- Scan ports
- Analyze protocol relationships as deeply as Wireshark
- Reconstruct conversations with the same level of detail as graphical analyzers
- Decrypt encrypted traffic without the required keys

Its primary purpose is efficient packet capture and basic packet inspection.

---

## Related Notes

- [[Wireshark]]
- [[Nmap]]
- [[TCP-IP]]
- [[OSI-Model]]
- [[Packets-and-Frames]]
- [[Networking-Basics]]