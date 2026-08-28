# LAN

#networking #lan #network-architecture

A **Local Area Network (LAN)** is a network that connects devices within a relatively limited geographical or administrative area, such as a home, office, laboratory, school, or datacenter. Its purpose is to allow connected systems to communicate and share resources over a common network infrastructure. A LAN can contain computers, servers, printers, network appliances, IoT devices, and other network-enabled systems.

LAN communication is normally based on technologies operating primarily at the **Data Link Layer (Layer 2)** and **Network Layer (Layer 3)** of the [[OSI-Model]]. Ethernet is one of the most common technologies used to implement wired LANs, while Wi-Fi provides wireless LAN connectivity. Although Ethernet and Wi-Fi differ significantly at the physical and link layers, both can provide hosts with connectivity to the same IP network.

A typical LAN uses **switches** to connect multiple devices. A switch learns the **MAC addresses** associated with its ports and uses this information to forward Ethernet frames toward the appropriate destination rather than transmitting every frame to every connected device. This makes switching fundamentally different from the behaviour of a traditional network hub. See [[Switching]] and [[Packets-and-Frames]].

At the IP layer, devices within a LAN are commonly assigned addresses belonging to the same subnet. The **subnet mask** or CIDR prefix determines which addresses are considered local. When a host communicates with another host on the same subnet, it can normally deliver traffic directly through the local network. When the destination belongs to another network, the host sends the traffic toward a [[Routing|router]] or default gateway.

LANs frequently use **DHCP** to automatically provide hosts with network configuration. A DHCP server can assign an IP address, subnet mask, default gateway, DNS servers, and other parameters. This avoids manually configuring every device and makes network administration substantially easier. See [[DHCP]].

A LAN may be divided into logical segments using technologies such as **VLANs (Virtual Local Area Networks)**. VLANs allow administrators to separate devices into distinct Layer 2 broadcast domains even when they share the same physical switching infrastructure. Segmentation can improve network organisation, reduce unnecessary broadcast traffic, and provide an additional security boundary when combined with appropriate Layer 3 access controls.

The concept of a LAN does not necessarily imply that every device can communicate freely with every other device. Modern networks commonly implement **firewalls, access-control rules, VLAN segmentation, network access control, and routing policies** to restrict communication. A workstation network, server network, guest network, and management network may therefore coexist within the same physical environment while having different security policies.

LANs also depend on mechanisms for resolving network-layer addresses into link-layer addresses. In IPv4 networks, **ARP (Address Resolution Protocol)** is used to determine the MAC address associated with an IPv4 address on the local network. IPv6 uses **Neighbor Discovery Protocol (NDP)** for comparable functionality. These mechanisms allow IP communication to be translated into the link-layer addressing required to deliver frames locally.

From a cybersecurity perspective, LANs are important because local network access can expose attack surfaces that are not necessarily reachable from the Internet. An attacker who gains access to a LAN may be able to perform reconnaissance, observe broadcast traffic, interact with local services, attempt credential attacks, exploit vulnerable hosts, or abuse protocols that implicitly trust local connectivity. Techniques such as ARP spoofing and rogue DHCP services demonstrate why Layer 2 security is important.

Network segmentation therefore plays a major role in reducing lateral movement. If a compromised workstation can communicate freely with every internal system, compromise of one host can potentially lead to compromise of many others. Restricting unnecessary communication between network segments limits the paths available to an attacker.

A LAN should therefore be understood as more than a collection of nearby computers. It is a local communication domain composed of physical and logical infrastructure, addressing mechanisms, switching, routing, and security controls. Understanding LANs provides a foundation for [[Switching]], [[Routing]], [[TCP-IP]], [[DHCP]], [[NAT]], network reconnaissance, and network security.
```
