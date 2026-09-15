# Networking Basics

#networking #tcp-ip #osi #internet #communication

## Overview

**Computer networking** is the practice of connecting devices so they can exchange data and share resources. A network enables communication between computers, servers, mobile devices, and other systems using standardized protocols and communication technologies.

Modern networks range from small home environments to global infrastructures such as the Internet. Regardless of their size, they all rely on the same fundamental concepts: addressing, protocols, routing, and layered communication.

Networking forms the foundation of nearly every modern computing service, including web applications, cloud computing, email, remote administration, file sharing, and cybersecurity.

---

## What is a Network?

A **network** is a collection of interconnected devices that communicate using a common set of protocols.

A network allows devices to:

- Exchange data
- Share hardware resources
- Access remote services
- Communicate over short or long distances
- Collaborate efficiently

Every device connected to a network is called a **host** or **node**.

---

## Types of Networks

Networks are commonly classified according to their geographical size.

| Type | Description |
|------|-------------|
| **PAN** | Personal Area Network covering a few meters (Bluetooth, USB). |
| **LAN** | Local Area Network connecting devices within a home, school, or office. |
| **MAN** | Metropolitan Area Network spanning a city or metropolitan region. |
| **WAN** | Wide Area Network connecting geographically distant networks. The Internet is the largest WAN. |

Most organizations build LANs internally while using WAN connections to communicate with other locations or cloud services.

---

## Network Components

A functional network consists of multiple hardware devices working together.

### Hosts

Hosts are devices capable of sending or receiving data.

Examples include:

- Desktop computers
- Laptops
- Smartphones
- Servers
- IoT devices
- Printers

---

### Network Interface Card (NIC)

A **Network Interface Card (NIC)** is the hardware component that connects a device to a network.

Each NIC possesses a unique **MAC address**, which identifies the device on the local network.

---

### Switches

A **switch** connects devices within the same Local Area Network (LAN).

It forwards Ethernet frames based on MAC addresses, allowing efficient communication between local devices.

See: [[Switching]]

---

### Routers

A **router** connects different networks together.

Routers examine IP addresses and determine the best path for forwarding packets between networks.

See: [[Routing]]

---

### Access Points

Wireless Access Points (APs) allow Wi-Fi devices to connect to wired networks.

They bridge wireless clients into the local Ethernet network.

---

## Client-Server Model

Most network communication follows the **client-server architecture**.

A **client** requests a service, while a **server** provides that service.

Examples include:

| Client | Server |
|---------|--------|
| Web Browser | Web Server |
| Email Client | Mail Server |
| SSH Client | SSH Server |
| FTP Client | FTP Server |

One server can provide services to many clients simultaneously.

---

## Protocols

A **protocol** is a standardized set of rules that defines how devices communicate.

Protocols specify:

- Message format
- Data transmission
- Error handling
- Authentication
- Connection management

Examples include:

- HTTP
- HTTPS
- DNS
- DHCP
- FTP
- SSH
- TCP
- UDP
- IPv4
- IPv6

Without protocols, devices from different manufacturers would be unable to communicate reliably.

---

## Network Communication

Communication between two devices follows a structured process.

1. The application generates data.
2. The data is divided into smaller units.
3. Protocol headers are added.
4. The data travels across the network.
5. The destination removes the headers.
6. The application reconstructs the original data.

This layered process enables interoperability between different operating systems, hardware vendors, and networking technologies.

---

## Encapsulation and Decapsulation

As data moves through the networking stack, each protocol layer adds its own control information.

This process is known as **encapsulation**.

At the receiving host, every layer removes the corresponding header until the original application data is recovered.

This reverse process is called **decapsulation**.

Encapsulation allows multiple protocols to cooperate while remaining independent from one another.

---

## Network Models

Modern networking is described using two complementary models.

### OSI Model

The **OSI Model** is a conceptual framework that divides communication into seven layers.

It is primarily used for learning, designing, and troubleshooting networks.

See: [[OSI-Model]]

---

### TCP/IP Model

The **TCP/IP protocol suite** is the practical networking model used by the Internet.

It defines the protocols responsible for real-world communication between devices.

See: [[TCP-IP]]

---

## Network Addressing

Every communicating device requires one or more identifiers.

Common addresses include:

- **IP Address** identifies a device across networks.
- **MAC Address** identifies a device within a local network.
- **Port Number** identifies the application or service running on a device.

These identifiers ensure that data reaches both the correct machine and the correct application.

---

## Network Services

Networks provide a variety of services that enable communication and resource sharing.

Some of the most common include:

| Service | Purpose |
|----------|---------|
| DNS | Resolves domain names into IP addresses. |
| DHCP | Automatically assigns network configuration. |
| HTTP / HTTPS | Web communication. |
| FTP | File transfer. |
| SSH | Secure remote administration. |

---

## Why Networking Matters in Cybersecurity

Nearly every cyber attack involves some form of network communication.

Understanding networking is essential for:

- Network reconnaissance
- Packet analysis
- Vulnerability assessment
- Intrusion detection
- Firewall configuration
- Incident response
- Penetration testing
- Malware analysis

Without a solid understanding of networking, analysing or securing computer systems becomes significantly more difficult.

---

## Related Notes

- [[OSI-Model]]
- [[TCP-IP]]
- [[Packets-and-Frames]]
- [[Ports]]
- [[Routing]]
- [[Switching]]
- [[Cyber-Notes-Jr-Fundamentals/02-Networking/DNS]]
- [[DHCP]]
- [[NAT]]
- [[LAN]]

---

## Key Takeaways

- Computer networks connect devices to exchange data and share resources.
- Communication relies on standardized protocols and layered architectures.
- Hosts communicate using IP addresses, MAC addresses, and port numbers.
- Switches connect devices within LANs, while routers connect different networks.
- The OSI Model provides a conceptual framework, whereas TCP/IP defines the protocols used on the Internet.
- Networking is one of the fundamental disciplines required for cybersecurity.