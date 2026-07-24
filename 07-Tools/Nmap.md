#networking #reconnaissance #enumeration #nmap #port-scanning

# Nmap

## Overview

Nmap (Network Mapper) is the industry-standard tool for network discovery, host identification, and port scanning. It is widely used by system administrators, network engineers, penetration testers, and security professionals to map networks, identify exposed services, assess attack surfaces, and verify security configurations.

Unlike passive packet analyzers such as [[Wireshark]] or [[Tcpdump]], Nmap is an **active reconnaissance tool**. It sends specially crafted packets to target systems and analyzes their responses to determine which hosts are online, which ports are open, what services are running, and, in many cases, which operating system the target is using.

Because nearly every penetration test begins with reconnaissance, Nmap is considered one of the most fundamental tools in offensive security.

---

## How Nmap Works

Nmap communicates directly with remote hosts by sending network probes and observing how the target responds.

Depending on the selected scan type, these probes may consist of:

- TCP packets
- UDP packets
- ICMP messages
- ARP requests
- DNS queries

By analyzing responses, timeouts, and protocol behavior, Nmap can infer information about the target without requiring authenticated access.

---

## Host Discovery

Before scanning ports, Nmap attempts to determine whether a host is alive.

Host discovery may use several techniques, including:

- ICMP Echo Requests
- TCP SYN probes
- TCP ACK probes
- ARP requests on local networks
- UDP probes

Skipping unnecessary scans against offline systems significantly improves efficiency when scanning large networks.

---

## Port Scanning

A primary function of Nmap is determining the state of network ports.

Common port states include:

| State | Description |
|--------|-------------|
| **Open** | A service is actively accepting connections. |
| **Closed** | The host is reachable, but no service is listening. |
| **Filtered** | A firewall or filtering device prevented Nmap from determining the port state. |
| **Unfiltered** | The port is reachable, but its exact state cannot be determined. |
| **Open \| Filtered** | Nmap cannot distinguish whether the port is open or filtered. |
| **Closed \| Filtered** | Nmap cannot determine whether the port is closed or filtered. |

Understanding these states is essential when interpreting scan results.

---

## Common Scan Types

Nmap supports numerous scanning techniques, each designed for different environments and objectives.

### TCP Connect Scan

Uses the operating system's networking stack to establish a complete TCP connection with the target.

- Highly reliable
- Easily detected
- Does not require raw socket privileges

---

### SYN Scan

Often called a **Stealth Scan**, this technique sends only the initial SYN packet and analyzes the response without completing the TCP three-way handshake.

Advantages include:

- Faster than TCP Connect
- Generates less application logging
- Commonly used during penetration testing

---

### UDP Scan

Used to discover services running over UDP.

Examples include:

- DNS
- DHCP
- SNMP
- NTP

UDP scanning is generally slower because UDP provides no acknowledgment mechanism.

---

### Ping Scan

Performs host discovery without scanning ports.

Useful for quickly identifying live systems before performing more detailed enumeration.

---

## Service Detection

Finding an open port is only the beginning.

Nmap can interact with services to identify:

- Service name
- Software version
- Product information
- Supported protocols

This process is known as **Version Detection**.

Knowing service versions helps identify outdated software and potential vulnerabilities.

---

## Operating System Detection

Nmap can estimate the target operating system by analyzing characteristics of its TCP/IP stack.

This process compares observed network behavior against a large fingerprint database.

Although not always perfectly accurate, OS detection often identifies:

- Operating system family
- Version
- Device type

---

## Nmap Scripting Engine (NSE)

One of Nmap's most powerful features is the **Nmap Scripting Engine (NSE)**.

NSE extends Nmap through Lua scripts capable of automating numerous security tasks.

Scripts can perform:

- Service enumeration
- Vulnerability detection
- Authentication testing
- Information gathering
- Misconfiguration detection
- Protocol interaction

Thousands of community-maintained scripts are included with Nmap.

---

## Timing and Performance

Large scans can take considerable time.

Nmap provides timing templates that balance:

- Speed
- Reliability
- Network impact
- Stealth

Aggressive scans complete faster but generate more network traffic, making them easier to detect.

Conservative scans are slower but often produce more reliable results on unstable networks.

---

## Output Formats

Nmap supports multiple output formats for documentation and automation.

Common formats include:

- Human-readable text
- XML
- Grepable output (legacy)
- Structured formats for scripting and reporting

Saving scan results allows them to be reviewed later or imported into other security tools.

---

## Common Use Cases

Nmap is frequently used for:

- Network discovery
- Asset inventory
- Port scanning
- Service enumeration
- Operating system identification
- Security auditing
- Vulnerability assessments
- Penetration testing
- Firewall validation

---

## Advantages

- Fast and highly scalable
- Supports multiple scanning techniques
- Accurate service detection
- Operating system fingerprinting
- Powerful scripting engine
- Extensive documentation
- Cross-platform
- Free and open source

---

## Limitations

Nmap cannot:

- Exploit vulnerabilities
- Passively monitor traffic
- Guarantee operating system detection accuracy
- Identify vulnerabilities solely from open ports
- Replace manual analysis

Scan results should always be interpreted alongside additional enumeration and verification.

---

## Related Notes

- [[Networking-Basics]]
- [[TCP-IP]]
- [[OSI-Model]]
- [[Ports]]
- [[Packets-and-Frames]]
- [[Wireshark]]
- [[Tcpdump]]