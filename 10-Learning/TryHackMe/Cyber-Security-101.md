## Search Skills

Learned how to efficiently search for technical information, an essential skill in cybersecurity where finding accurate and up-to-date resources is often more valuable than memorizing commands. The room emphasized evaluating the credibility of sources, distinguishing official documentation from community content, and verifying information before trusting or using it.

The room introduced advanced search engine operators such as `site:`, `filetype:`, quotation marks for exact matches, and keyword exclusion. These techniques allow searches to be narrowed down significantly, making it easier to locate documentation, research papers, configuration guides, or security-related resources without manually filtering hundreds of results.

It also covered specialized search platforms commonly used by security professionals, including Shodan for discovering Internet-connected devices, Censys for searching hosts and certificates, VirusTotal for checking files, hashes, and URLs against multiple antivirus engines, and Exploit Database for finding publicly available exploits and proof-of-concept code. Finally, the room highlighted the importance of reading official documentation and following reputable security communities to stay informed about new technologies, vulnerabilities, and best practices.

---

## Linux Fundamentals Part 1

This room introduced the Linux operating system and explained why it is widely used across servers, cloud infrastructure, embedded devices, Android, and cybersecurity environments. I learned that Linux is not a single operating system but a family of distributions based on the Linux kernel, with Ubuntu serving as the environment for this module.

I became familiar with interacting with a Linux system through the terminal instead of a graphical interface. The room introduced essential commands such as `echo`, `whoami`, `pwd`, `ls`, `cd`, `cat`, and `touch`, allowing me to inspect the current user, navigate directories, create files, and display file contents. These commands form the foundation for almost every task performed on Linux systems.

The room also covered searching and working efficiently with the filesystem. I learned to locate files using `find` and search inside files with `grep`, making it possible to quickly retrieve information without manually browsing directories. Finally, I was introduced to common shell operators such as `>`, `>>`, `&`, and `&&`, which control command execution and input/output redirection, providing the basis for more advanced shell usage.

---

## Linux Fundamentals Part 2

This room expanded my Linux knowledge by introducing remote administration through SSH (Secure Shell). I learned how SSH provides encrypted communication for securely accessing and managing remote Linux systems, a fundamental skill for system administration, cloud environments, and penetration testing.

I also learned how to make better use of Linux commands by using flags and arguments to modify their behavior. Building on the commands introduced in Part 1, I practiced managing the filesystem with operations such as copying, moving, removing, and identifying files. These concepts demonstrated how command-line utilities can be combined to perform everyday administrative tasks efficiently.

Another major topic was the Linux permission model. I learned that every file and directory has ownership and permission settings that determine which users can read, write, or execute them. Understanding these access controls is essential for both securing Linux systems and troubleshooting permission-related issues.

Finally, the room introduced several important directories within the Linux filesystem, including locations for user data, system configuration, executables, temporary files, and logs. Understanding the purpose of these standard directories makes navigating Linux systems more intuitive and provides a foundation for more advanced administration and security topics.

---

## Linux Fundamentals Part 3

This room expanded my Linux skills beyond basic command-line usage by introducing several tools and concepts used in day-to-day system administration. I learned how terminal-based text editors such as Nano and Vim allow files to be created and modified directly from the command line, making them essential utilities when working on remote systems or environments without a graphical interface.

The room also introduced a collection of common Linux utilities for transferring files, downloading resources, and retrieving system information. In addition, I learned how Linux manages running processes, including how to inspect active processes, terminate unresponsive applications, and understand the relationship between programs and the operating system.

Finally, I explored several administrative concepts that are fundamental to maintaining Linux systems. I learned how scheduled tasks automate repetitive operations, how package managers install and update software while handling dependencies, and how system and application logs record events that are valuable for troubleshooting, monitoring, and security investigations. Together, these topics provided a practical introduction to managing and maintaining Linux systems rather than simply using them. 

---

## Windows Fundamentals 1

This room introduced the fundamental components of the Microsoft Windows operating system and how they are organized from both a user and administrator perspective. I learned about the different Windows editions, the graphical user interface (GUI), and the role of common desktop components such as the Start Menu, Taskbar, Notification Area, and File Explorer. The room also explained the purpose of the NTFS file system and why it is the standard file system for modern Windows installations.

The room explored the importance of the `C:\Windows` directory, particularly the `System32` folder, which contains critical operating system files, libraries, and utilities required for Windows to function correctly. It also covered user accounts, user profiles, file permissions, and the difference between standard users and administrators, highlighting how Windows isolates user data while enforcing access control.

Another major topic was User Account Control (UAC), which helps reduce the risk of unauthorized system changes by requiring administrative approval before privileged operations are performed. I also learned the differences between the modern Settings application and the traditional Control Panel, understanding that both are used to configure the operating system, although Microsoft is gradually moving functionality into the Settings interface.

Finally, the room introduced Task Manager as an essential administration and troubleshooting tool. I learned how to monitor running applications and processes, view CPU, memory, disk, and network usage, identify active users, and manage tasks, providing a foundation for understanding Windows performance and process management in later modules.

---

## Windows Fundamentals 2

This room expanded my understanding of Windows administration by introducing several built-in management and diagnostic tools commonly used by system administrators and security professionals. I learned how **System Configuration (MSConfig)** can be used to troubleshoot startup problems, control boot options, manage services, and access various administrative utilities from a single interface. The room also introduced **Computer Management**, which centralizes tools such as Event Viewer, Task Scheduler, Device Manager, Disk Management, Services, and Shared Folders. 

I learned the purpose of **User Account Control (UAC)** in greater detail, understanding how it reduces the attack surface by limiting administrative privileges until explicit approval is granted. The room also covered **System Information (msinfo32)**, which provides detailed information about hardware resources, installed components, drivers, operating system configuration, and the software environment, making it valuable for troubleshooting and system auditing. 

Another important topic was **Resource Monitor (resmon)**, a more advanced monitoring tool than Task Manager. It provides real-time visibility into CPU, memory, disk, and network activity, allowing administrators to identify resource bottlenecks, investigate performance issues, and analyze process behavior in greater detail. The room also reinforced the usefulness of the **Command Prompt (cmd.exe)** as a fundamental interface for system administration and automation. 

Finally, the room introduced the **Windows Registry**, the hierarchical database that stores operating system, hardware, user, and application configuration. I learned that the Registry is managed through **Registry Editor (regedit)** and that modifying registry values can significantly affect system behavior, making careful administration essential. Together, these tools provide the foundation required for diagnosing Windows systems, monitoring performance, and understanding how Windows stores and manages its configuration.

---

## Windows Fundamentals 3

This room introduced the security features built into Windows that help protect the operating system against vulnerabilities, malware, unauthorized access, and data loss. I learned that Windows security is based on multiple defensive layers rather than a single protection mechanism, combining regular updates, endpoint protection, access control, encryption, and system recovery features to strengthen the overall security posture. 

A major topic was **Windows Update**, which delivers security patches, bug fixes, driver updates, and feature improvements. Keeping systems updated is one of the most effective defenses against known vulnerabilities, as attackers frequently target machines that are missing critical security patches. The room also explored **Windows Security**, Microsoft's centralized security dashboard, including **Virus & Threat Protection**, **Firewall & Network Protection**, **App & Browser Control**, and **Device Security**, explaining how each component contributes to defending the system against different types of threats. 

The room also covered **BitLocker Drive Encryption**, which protects data at rest by encrypting entire storage volumes. I learned that BitLocker helps prevent unauthorized access to sensitive information if a device is lost or stolen and that it commonly integrates with the Trusted Platform Module (TPM) to securely manage encryption keys. Another important concept was the **Volume Shadow Copy Service (VSS)**, which creates point-in-time snapshots of files and volumes, enabling backup software and system recovery features to restore previous versions of data when necessary. 

Overall, this room provided an overview of Windows' native security ecosystem, demonstrating how updates, malware protection, firewall rules, hardware-backed security, disk encryption, and recovery mechanisms work together to improve the confidentiality, integrity, and availability of Windows systems. These concepts establish a foundation for understanding Windows hardening and defensive security practices used in enterprise environments. 

---

## Active Directory Basics

This room introduced Microsoft Active Directory (AD), the centralized directory service used to manage identities, devices, and resources in Windows enterprise environments. I learned that Active Directory allows organizations to authenticate users, authorize access to network resources, and simplify administration by managing thousands of users and computers from a centralized infrastructure. I also understood the role of a **Domain Controller (DC)** as the server responsible for hosting Active Directory services and processing authentication requests. 

The room explored the logical structure of an Active Directory environment, including **domains**, **Organizational Units (OUs)**, **users**, **groups**, and **computer objects**. I learned that domains provide administrative and security boundaries, while OUs organize objects to simplify delegation and policy management. Groups were presented as the primary mechanism for assigning permissions efficiently instead of configuring access for each user individually. 

Another important concept was **Group Policy (GPO)**, which enables administrators to centrally configure security settings, software deployment, password policies, desktop configurations, and many other operating system settings across multiple computers and users. The room also introduced the two primary Windows authentication protocols, **Kerberos** and **NTLM**, explaining that Kerberos is the default authentication mechanism in modern Active Directory environments, while NTLM remains available for compatibility with legacy systems.

Finally, I learned how multiple domains can be connected through **trees**, **forests**, and **trust relationships** to create larger enterprise infrastructures while maintaining centralized identity management. Understanding how these components interact provides the foundation required for both Windows system administration and Active Directory security, as most enterprise authentication, authorization, and privilege management depend on these concepts. 

---

## Windows Command Line

This room introduced the Microsoft Windows Command Prompt (`cmd.exe`), the default command-line interpreter used to interact with Windows systems. I learned why command-line interfaces remain essential despite the availability of graphical interfaces, particularly for system administration, automation, remote management, troubleshooting, and cybersecurity operations where speed and efficiency are critical. The room reinforced that mastering the command line allows security professionals to inspect and manage systems far more effectively than relying solely on graphical tools.

I learned how to navigate the Windows filesystem using commands such as `cd`, `dir`, and `tree`, inspect environment variables with `set`, and manipulate files and directories using common file management commands. The room also introduced wildcard characters to efficiently operate on multiple files simultaneously, demonstrating how routine administrative tasks can be performed quickly from the terminal. These skills form the foundation for interacting with Windows systems during administration, incident response, and penetration testing.

Another major focus was gathering system and network information directly from the command line. I explored commands capable of identifying operating system details, hardware configuration, hostname, network interfaces, IP configuration, DNS resolution, routing information, and active network connections. Understanding these commands is fundamental for troubleshooting connectivity issues, performing host enumeration, validating system configurations, and collecting information during security assessments.

Finally, the room introduced process management and several administrative utilities commonly used by Windows administrators. I learned how to inspect running processes, monitor active services and network sessions, terminate processes when necessary, and use built-in help documentation to discover command options. The room also highlighted additional maintenance and diagnostic tools such as filesystem checking, driver enumeration, and system file verification, providing a practical introduction to day-to-day Windows administration through the command line while preparing for more advanced topics such as PowerShell. 

---

## Windows PowerShell

This room introduced Microsoft PowerShell, a modern command-line shell and scripting language built on the .NET platform. Unlike the traditional Windows Command Prompt, PowerShell works with structured objects instead of plain text, allowing commands to exchange rich data through the pipeline. I learned why PowerShell has become the primary automation and administration tool for Windows environments, making it indispensable for system administrators, cybersecurity professionals, and incident responders.

I learned the fundamental structure of PowerShell commands, known as cmdlets, which follow the `Verb-Noun` naming convention (such as `Get-Process` and `Get-Service`). The room introduced navigation through the Windows filesystem, file and directory management, and the use of built-in help documentation to understand available cmdlets and their parameters. This consistent syntax makes PowerShell easier to learn while providing significantly more functionality than the traditional Command Prompt.

Another major concept was PowerShell's object pipeline. Instead of passing text between commands, PowerShell passes .NET objects that can be filtered, sorted, selected, and formatted using cmdlets such as `Where-Object`, `Sort-Object`, and `Select-Object`. This object-oriented design enables powerful data processing and simplifies complex administrative tasks without requiring external utilities or extensive text parsing.

The room also demonstrated how PowerShell can gather system and network information, monitor processes and services, and automate repetitive tasks through scripting. I was introduced to variables, loops, conditional statements, and basic scripting concepts that allow administrative tasks to be automated efficiently. These capabilities make PowerShell one of the most important tools in Windows administration and cybersecurity, where it is widely used for system management, incident response, forensic investigations, and security assessments.
---

## Linux Shells

This room explored Linux shells as the primary interface between users and the operating system. I learned that a shell is a command-line interpreter responsible for receiving user input, launching programs, managing processes, and interacting with the Linux kernel. While Bash is the most common shell, the room introduced the existence of alternative shells such as Zsh, Fish, and Dash, each offering different features, performance characteristics, and customization options depending on the user's needs.

The room explained how Linux executes commands by searching directories listed in the `PATH` environment variable and demonstrated how shell built-in commands differ from external executables stored on the filesystem. I also learned how environment variables influence shell behavior and how user-specific configuration files allow the shell environment to be customized. Understanding these concepts is essential for configuring Linux systems, troubleshooting command execution, and creating efficient working environments.

Another important topic was command execution and shell features that improve productivity. The room introduced command history, tab completion, aliases, command substitution, and shell expansion mechanisms that simplify repetitive tasks and reduce typing. These features allow users to work more efficiently while interacting with the operating system entirely through the command line.

Finally, the room reinforced the role of shells in system administration, automation, and cybersecurity. Since nearly every Linux server, cloud instance, or penetration testing environment relies heavily on shell access, mastering shell behavior and navigation provides a strong foundation for Bash scripting, privilege escalation techniques, remote administration through SSH, and advanced Linux system management.

---

## Networking Concepts

This room introduced the fundamental principles of computer networking by explaining how devices communicate across local and global networks. I learned the purpose of the ISO/OSI reference model and the TCP/IP protocol suite, understanding how network communication is divided into layers that each perform specific responsibilities. This layered architecture provides a framework for understanding how data moves from an application to the physical network and back again.

The room explored the responsibilities of the individual networking layers, including physical transmission, data link communication, logical addressing, routing, end-to-end transport, and application services. I learned how protocols are grouped within these layers and how encapsulation allows each protocol to add the information required for reliable communication across different networks.

Another major topic was IP networking. I learned how IPv4 addressing, subnetting, and routing enable devices on different networks to communicate with one another. The room also introduced the differences between TCP and UDP, explaining their communication models, reliability characteristics, and common use cases, together with the purpose of TCP and UDP port numbers for identifying network services.

Finally, I gained practical experience connecting to network services from the command line while reinforcing the relationship between networking theory and real-world communication. These concepts establish the foundation required for understanding higher-level protocols, network analysis, troubleshooting, and offensive and defensive cybersecurity techniques.

---

## Networking Essentials

This room expanded my understanding of how modern networks operate by introducing the essential protocols and technologies that enable devices to communicate reliably with minimal manual configuration. I learned how hosts automatically obtain network settings through the Dynamic Host Configuration Protocol (DHCP), how Address Resolution Protocol (ARP) maps IPv4 addresses to MAC addresses on local networks, and why these protocols are fundamental for seamless communication between devices.

The room also explored Internet Control Message Protocol (ICMP) and its role in network diagnostics rather than data transport. I learned how tools such as `ping` and `traceroute` use ICMP messages to verify connectivity, measure latency, identify routing paths, and troubleshoot network issues. In addition, I gained a deeper understanding of routing, including how routers forward packets between different networks and make forwarding decisions based on routing information.

Another major topic was Network Address Translation (NAT), which enables multiple devices on a private network to share a single public IPv4 address. I learned why NAT became necessary due to IPv4 address exhaustion, how it provides a level of address abstraction, and how it allows home and enterprise networks to communicate with external networks efficiently while conserving public address space.

By combining automatic configuration, address resolution, routing, network diagnostics, and address translation, this room provided a practical understanding of the technologies that keep modern IP networks functioning. These concepts establish the foundation required for studying higher-level application protocols, packet analysis, network troubleshooting, and cybersecurity operations.

---

## Networking Core Protocols

This room introduced the core application-layer protocols that power many of the Internet's most common services. I learned how these protocols enable users to browse websites, transfer files, retrieve domain information, and exchange email while following the client-server communication model built on top of the TCP/IP protocol suite. Understanding these protocols provides the foundation for analysing network traffic and identifying security issues in real-world environments.

The room explored the Domain Name System (DNS) and WHOIS, explaining how human-readable domain names are translated into IP addresses and how domain registration records can be queried to gather administrative and ownership information. These services are frequently used during network troubleshooting, infrastructure management, and reconnaissance during security assessments. 

Another major topic was the Hypertext Transfer Protocol (HTTP) and the File Transfer Protocol (FTP). I learned how web browsers and servers exchange requests and responses using HTTP, including the role of common methods, headers, and status codes. I also explored how FTP enables file transfers between clients and servers, understanding its authentication process, communication channels, and the limitations of transmitting data without encryption. 

Finally, the room covered the core email protocols: Simple Mail Transfer Protocol (SMTP), Post Office Protocol version 3 (POP3), and Internet Message Access Protocol (IMAP). I learned how SMTP is responsible for sending email, while POP3 and IMAP retrieve messages using different synchronization models. Together, these protocols demonstrated how email systems operate behind the scenes and highlighted the importance of understanding legacy plaintext protocols before learning how they are secured with technologies such as TLS in subsequent networking topics.

---

## Networking Secure Protocols

This room introduced the security mechanisms that protect network communications from eavesdropping, tampering, and impersonation attacks. I learned that many traditional Internet protocols, including HTTP, SMTP, POP3, IMAP, FTP, and Telnet, were originally designed without encryption, leaving sensitive information such as credentials and personal data vulnerable to interception.

A major focus of the room was Transport Layer Security (TLS), which provides confidentiality, integrity, and authenticity for network communications. I learned how TLS uses digital certificates, Certificate Authorities (CAs), and public key cryptography to verify the identity of communicating parties before establishing an encrypted session. Understanding the TLS handshake and the role of certificates demonstrated how secure communications are established over untrusted networks.

The room also explored how TLS enhances existing application-layer protocols. I learned how HTTP becomes HTTPS, SMTP becomes SMTPS, and email retrieval protocols become POP3S and IMAPS, protecting both authentication credentials and transferred data. In addition, I studied how Secure Shell (SSH) replaces the insecure Telnet protocol for remote administration and how SFTP and FTPS provide secure alternatives for file transfers.

Finally, I learned how Virtual Private Networks (VPNs) create encrypted tunnels over public networks, allowing remote users and sites to communicate securely as if they were connected to the same private network. Together, TLS, SSH, secure application protocols, and VPNs form the foundation of modern secure network communications and are essential technologies for protecting enterprise and Internet infrastructure.

---

## Wireshark: The Basics

This room introduced Wireshark, one of the most widely used network protocol analyzers for inspecting live network traffic and offline packet capture (PCAP) files. I learned how packet analysis provides visibility into network communications by decoding protocols across the TCP/IP stack, making Wireshark an essential tool for network troubleshooting, incident response, malware analysis, and penetration testing.

I became familiar with the Wireshark interface, including the packet list, packet details, and packet bytes panes. The room demonstrated how individual packets can be dissected layer by layer, allowing information such as Ethernet frames, IP addresses, transport protocols, and application-layer data to be examined. Understanding how each protocol encapsulates the next makes it easier to trace communications and identify abnormal network behavior.

The room also covered efficient packet navigation and analysis techniques. I learned how to search for specific packets, inspect protocol fields, follow packet streams, read packet metadata and comments, and move quickly through large captures using navigation features. These capabilities allow analysts to investigate communications without manually inspecting every packet.

Finally, I learned how display filters narrow the visible traffic to specific protocols, addresses, ports, or packet attributes without modifying the original capture. Using display filters significantly improves the speed and accuracy of packet analysis by isolating relevant traffic from large network captures, providing the foundation for more advanced traffic analysis and protocol investigation.

---

## Tcpdump: The Basics

This room introduced `tcpdump`, a lightweight command-line packet analyzer widely used on Unix-like operating systems for capturing and inspecting network traffic. I learned that `tcpdump` is built on the `libpcap` library, which provides low-level access to network packets and serves as the foundation for many packet capture tools. Its speed, stability, and minimal resource usage make it a standard utility for system administrators, network engineers, incident responders, and penetration testers.

I learned how to capture traffic from specific network interfaces, limit the number of captured packets, save captures to PCAP files, and read previously captured traffic for offline analysis. Understanding how to create reusable packet captures allows investigations to be performed without requiring continuous access to the target system and enables captures to be shared with other analysis tools such as Wireshark.

The room also covered Berkeley Packet Filter (BPF) expressions, which allow traffic to be filtered before it is captured. I learned how to isolate packets based on protocols, IP addresses, hosts, ports, and other packet attributes, reducing unnecessary data and making network analysis significantly more efficient. In addition, I explored several display options that control how packet information is presented, including verbosity levels, disabling hostname and port resolution, and displaying packet payloads in different formats. These features enable fast investigation of network communications directly from the terminal without relying on a graphical interface.

---

## Nmap: The Basics

This room introduced Nmap (Network Mapper), the industry-standard tool for network discovery and security auditing. I learned how Nmap efficiently discovers live hosts, identifies open ports, and enumerates network services, making it a fundamental tool for reconnaissance, system administration, vulnerability assessments, and penetration testing. The room also emphasized how automated scanning dramatically reduces the time required to map large networks compared to manual techniques.

I explored the complete workflow of an Nmap scan, beginning with host discovery to determine which systems are online before performing port scanning to identify accessible network services. The room explained the differences between common port scanning techniques and demonstrated how version detection can identify the software and service versions running behind open ports, providing valuable information for further enumeration and vulnerability assessment.

Another important topic was scan optimization. I learned how timing templates influence scan speed, reliability, and stealth, allowing scans to be adapted to different environments and objectives. Finally, the room covered Nmap's output formats, showing how scan results can be presented in human-readable and machine-readable formats for documentation, reporting, and integration with other security tools. Together, these concepts establish the foundation required for more advanced network reconnaissance and Nmap usage.

---

## Cryptography Basics

This room introduced the fundamental principles of cryptography and explained how encryption protects the confidentiality of data by transforming plaintext into ciphertext. I learned the difference between encryption and encoding, the distinction between symmetric and asymmetric encryption, and the purpose of keys in securing communications.

The room also introduced two important mathematical concepts used throughout cryptography. **XOR (Exclusive OR)** is a bitwise operation that outputs `1` when two bits differ and `0` when they are equal, making it reversible and widely used in stream ciphers. **Modular arithmetic (`mod`)** performs calculations using remainders after division, keeping values within a fixed range. This concept forms the mathematical foundation of many public-key cryptosystems such as RSA and Diffie-Hellman.

---

## Public Key Cryptography Basics

This room introduced the principles of asymmetric cryptography and explained how public-key encryption solves the problem of securely exchanging secret keys over untrusted networks. I learned that asymmetric cryptography relies on a mathematically related pair of keys: a public key, which can be shared freely, and a private key, which must remain secret. Unlike symmetric encryption, the two keys perform different roles, making secure communication possible without first sharing a secret.

The room explored the most common public-key algorithms and their purposes. I learned that RSA can be used for both encryption and digital signatures, Diffie-Hellman enables two parties to securely establish a shared secret over an insecure channel, and Elliptic Curve Cryptography (ECC) provides similar security to RSA while requiring much smaller keys. These algorithms form the foundation of many modern cryptographic protocols.

Finally, the room demonstrated how public-key cryptography is applied in real-world systems. I learned how SSH uses key pairs for passwordless authentication, how digital signatures provide authenticity, integrity, and non-repudiation, and how digital certificates and Public Key Infrastructure (PKI) allow clients to verify the identity of servers. Modern protocols such as HTTPS combine asymmetric cryptography for authentication and key exchange with symmetric encryption to efficiently protect data in transit.

---

## Hashing Basics

This room introduced cryptographic hash functions and explained how they generate a fixed-length output from data of any size. I learned the essential properties of secure hash functions, including determinism, the avalanche effect, collision resistance, and the fact that hashing is a one-way operation designed to be computationally infeasible to reverse.

The room explored the role of hashing in authentication systems, showing why passwords should never be stored in plaintext. I learned how password hashes are securely stored using salts to defnd against rainbow table attacks, how common hash algorithms can be recognized, and why weak or unsalted hashes are vulnerable to password-cracking techniques such as dictionary and brute-force attacks

Finally, the room demonstrated how hashing is used to verify data integrity. By comparing the hash values of files, software downloads, or messages, it is possible to detect accidental corruption or malicious tampering without comparing the entire contents. This makes cryptographic hashing a fundamental building block for password storage, file verification, digital signatures, and many other security mechanisms.

---

## John the Ripper: The Basics

This room introduced **John the Ripper (JtR)**, one of the most widely used password-cracking tools in cybersecurity. I learned how John identifies different hash formats and performs dictionary attacks to recover plaintext passwords from cryptographic hashes. The room also covered the importance of selecting the correct hash format and using appropriate wordlists to improve cracking efficiency. 

The room explored several real-world password-cracking scenarios. I learned how to crack Windows authentication hashes, Linux `/etc/shadow` password hashes, password-protected ZIP and RAR archives, and encrypted SSH private keys. It also introduced John’s **Single Crack Mode** and **custom rules**, which generate additional password candidates by applying transformations to existing words, increasing the likelihood of recovering weak passwords.

Finally, the room demonstrated how John the Ripper fits into penetration testing and security assessments. Rather than exploiting cryptographic weaknesses, the tool takes advantage of poor password choices, weak policies, and predictable patterns. This highlighted the importance of strong, unique passwords, proper password storage practices, and effective password policies as essential defenses against offline password-cracking attacks.

---

## Moniker Link (CVE-2024-21413)

This room explored **CVE-2024-21413 (Moniker Link)**, a critical Microsoft Outlook vulnerability disclosed in February 2024 that can lead to **NTLM credential leakage** and contribute to **Remote Code Execution (RCE)** attack chains. The vulnerability abuses Outlook's handling of specially crafted Moniker Links, allowing attackers to bypass Protected View and coerce Outlook into initiating SMB authentication to an attacker-controlled server, exposing the victim's NTLM hash. The room also introduced the real-world impact of this vulnerability, its CVSS score, affected Office versions, and the importance of rapid patch management for widely deployed enterprise software.

The practical section demonstrated how attackers can leverage this behavior by crafting malicious emails containing specially formatted hyperlinks. Rather than exploiting memory corruption, the attack abuses Windows authentication mechanisms to force outbound SMB connections, enabling tools such as Responder to capture NTLM challenge-response hashes. This highlighted how seemingly harmless user interactions, such as clicking a hyperlink in an email, can expose authentication material that may later be relayed or cracked depending on the target environment.

The room also emphasized defensive techniques by explaining how to detect exploitation attempts through network and endpoint telemetry, including unexpected outbound SMB traffic from Outlook and suspicious authentication events. Finally, it covered mitigation strategies such as applying Microsoft's security updates, restricting outbound SMB traffic, hardening email clients, and understanding the limitations of client-side protections like Protected View. Together, these concepts reinforce the importance of combining vulnerability management, network controls, and monitoring to defend against modern phishing and credential theft attacks.

---

## Metasploit: Introduction

This room introduced the **Metasploit Framework**, the most widely used open-source exploitation framework in penetration testing. Rather than focusing solely on launching exploits, the room explained how Metasploit supports multiple phases of an engagement, including information gathering, vulnerability validation, exploitation, and post-exploitation. I learned the distinction between the commercial **Metasploit Pro** and the open-source **Metasploit Framework**, with the latter providing a modular command-line environment through `msfconsole` for interacting with exploits, payloads, scanners, and post-exploitation modules.

The room explored the core concepts that make up the framework, including the relationship between **vulnerabilities**, **exploits**, and **payloads**. I learned how Metasploit organizes its functionality into modules such as **Auxiliary**, **Exploits**, **Payloads**, **Encoders**, and **Post** modules, each serving a specific purpose during an assessment. It also introduced the difference between **staged** and **single (inline)** payloads, explaining how staged payloads first establish a communication channel before delivering the remaining payload, while single payloads execute as a single self-contained component.

Another major focus was learning to navigate and operate `msfconsole`. The room demonstrated how to search for modules, inspect their documentation, select appropriate exploits, configure required parameters, review module options, and launch attacks against vulnerable services. It also covered managing active sessions and understanding how Metasploit's modular architecture simplifies the exploitation workflow without abstracting away the underlying concepts of the vulnerability being targeted. 

Finally, the room emphasized that Metasploit is a productivity tool rather than a replacement for technical knowledge. Effective use of the framework requires understanding the target service, verifying vulnerabilities, selecting appropriate payloads, and interpreting exploitation results. This reinforces the importance of combining manual enumeration and vulnerability analysis with automation, allowing penetration testers to perform assessments more efficiently while maintaining a clear understanding of the techniques being executed.

---

## Metasploit: Exploitation

This room focused on applying the **Metasploit Framework** throughout a complete exploitation workflow, moving beyond simply launching exploits to performing reconnaissance, vulnerability assessment, exploitation, and post-exploitation. I learned how Metasploit can be used not only as an exploitation framework but also as a platform for scanning services, validating vulnerabilities, managing discovered hosts, and organizing penetration testing engagements through its integrated database features.

The room demonstrated how to perform service enumeration using Metasploit's **Auxiliary** scanner modules, identify vulnerable services, and verify findings before selecting an appropriate exploit. I also learned how the Metasploit database stores information about hosts, services, vulnerabilities, credentials, loot, and active sessions, making it easier to manage larger engagements without repeating reconnaissance or manually tracking results. This reinforced the importance of maintaining structured information during a penetration test rather than relying on isolated commands.

A major objective of the room was exploiting real-world vulnerabilities using Metasploit. I practiced exploiting **MS17-010 (EternalBlue)** to obtain a Meterpreter session on a vulnerable Windows host and exploited the **vsftpd 2.3.4 backdoor** on a Linux target, demonstrating that the same exploitation methodology applies across different operating systems and services. The room emphasized selecting the correct exploit module, configuring payloads, validating target compatibility, and interacting with compromised systems through Meterpreter sessions.

Finally, the room introduced **msfvenom**, showing how custom payloads can be generated for different operating systems and architectures before being delivered to a target. After obtaining access, I learned to leverage Meterpreter together with Metasploit's post-exploitation modules to gather credentials, dump password hashes, and further assess the compromised system. Overall, the room highlighted that successful exploitation depends not only on launching exploits, but also on effective enumeration, proper payload selection, session management, and systematic post-exploitation activities.

---

## Meterpreter

This room explored **Meterpreter**, Metasploit's advanced in-memory payload designed for post-exploitation. Unlike a traditional reverse shell that simply executes operating system commands, Meterpreter operates as a fully featured agent within a command-and-control (C2) architecture. Running entirely in memory, it avoids writing files to disk, establishes encrypted communication channels with the attacker, and provides a modular environment that can be extended with additional functionality as required. The room also discussed how these design choices improve flexibility while highlighting that modern Endpoint Detection and Response (EDR) solutions are still capable of detecting Meterpreter through behavioral and memory analysis.

A major focus of the room was learning how to interact with an active Meterpreter session. I learned how to gather system information, identify the current user, inspect running processes, navigate the filesystem, upload and download files, execute operating system commands, migrate into other processes, and manage multiple sessions. These capabilities demonstrate how Meterpreter provides a unified interface for interacting with compromised systems without relying solely on native shell commands

The room also introduced Meterpreter's post-exploitation capabilities, including privilege enumeration, credential harvesting, password hash dumping, screenshot capture, keylogging, registry interaction, network enumeration, token impersonation, and loading additional extensions such as Kiwi for credential extraction. Rather than treating these as isolated commands, the room emphasized how they fit into a structured post-exploitation workflow focused on gathering intelligence, escalating privileges, and expanding access while maintaining operational efficiency.

Finally, the room highlighted effective session management within Metasploit. I learned how Meterpreter sessions integrate with Metasploit's `post/` modules, allowing automated post-exploitation tasks to reuse existing compromised sessions. The room reinforced that Meterpreter is far more than an interactive shell, serving as a flexible platform for post-exploitation while also emphasizing its limitations against modern defensive technologies and the importance of understanding the techniques behind its functionality rather than relying solely on automation.

---

## Blue

This room provided a practical introduction to the complete exploitation lifecycle against a vulnerable Windows system by leveraging **MS17-010 (EternalBlue)**, one of the most well-known SMB vulnerabilities ever disclosed. I learned how to perform reconnaissance with Nmap, identify exposed SMB services, correlate enumeration results with publicly known vulnerabilities, and validate that the target was susceptible to EternalBlue before attempting exploitation. The room reinforced the importance of enumeration as the foundation of every penetration test, demonstrating that exploitation should always be driven by evidence rather than assumption.

The exploitation phase focused on using the Metasploit Framework to compromise a Windows 7 machine through the EternalBlue exploit. Beyond simply obtaining initial access, I learned how to configure exploit modules, select and customize payloads, establish reverse shells, and upgrade them into Meterpreter sessions for more advanced interaction with the target. The room illustrated how Metasploit streamlines exploitation while still requiring an understanding of the underlying vulnerability, SMB protocol, and payload behavior.

Following initial access, the room introduced several essential post-exploitation techniques. I learned how to migrate Meterpreter into stable SYSTEM processes, dump NTLM password hashes from the Security Account Manager (SAM), crack captured credentials using offline password-cracking tools, and navigate the Windows filesystem to locate sensitive information. These tasks demonstrated that obtaining code execution is only the beginning of an engagement, with credential access, privilege management, and data collection representing equally important phases of a penetration test.

Finally, the room highlighted the real-world significance of EternalBlue by connecting the technical exploitation process to one of the most impactful Windows vulnerabilities in history. I gained a deeper understanding of how unpatched SMB services can lead to complete system compromise, why legacy protocols such as SMBv1 pose significant security risks, and how vulnerability management, timely patching, and disabling deprecated services are critical defensive measures. Overall, the room combined reconnaissance, exploitation, privilege escalation, credential access, and post-exploitation into a cohesive workflow that reflects the methodology used during real-world penetration testing engagements.

---

## Web Application Basics

This room introduced the fundamental architecture of web applications and explained how users interact with them through a web browser. I learned that a web application consists of front-end technologies such as HTML, CSS, and JavaScript, which provide the user interface, while back-end components including web servers, databases, application servers, and Web Application Firewalls (WAFs) process requests, store data, and protect the application. Understanding how these components work together provides the foundation for both web development and web application security.

The room also explored the structure of Uniform Resource Locators (URLs), breaking them into their main components such as the scheme, domain, port, path, query string, and fragment. I learned how each element determines how a client reaches a resource and why user-controlled values like URL paths and query parameters must be validated and sanitised to prevent attacks such as injection or unauthorised access. The module also introduced concepts such as HTTPS, default ports, and typosquatting, highlighting both usability and security implications of URL design. 

Another major focus was the HTTP protocol and the communication model between clients and servers. I learned how HTTP requests and responses are structured, including the start line, headers, body, and the purpose of the empty line separating metadata from content. The room covered the most common HTTP methods, including GET, POST, PUT, and DELETE, demonstrating how each represents a different action performed on server resources. I also became familiar with HTTP status codes and how they communicate the outcome of requests, making them essential for troubleshooting, development, and security testing.

Finally, the room introduced HTTP headers and their role in controlling communication, content negotiation, caching, authentication, and security. I learned that security-related headers help mitigate common web attacks by instructing browsers how to handle application content safely. Overall, the room established the core concepts required before studying web application vulnerabilities, API security, and offensive web penetration testing, providing the networking and protocol knowledge necessary for more advanced web security topics. 

---

## JavaScript Essentials

This room introduced the fundamentals of JavaScript from both a web development and cybersecurity perspective. I learned that JavaScript is an interpreted scripting language primarily used to add dynamic and interactive functionality to web applications, executing directly within the browser through its JavaScript engine. The room covered the language's core syntax, including variables, data types, operators, functions, objects, arrays, loops, and conditional statements, providing the programming foundation required to understand how modern web applications behave.

The room also explored how JavaScript integrates with HTML through inline scripts, internal `<script>` tags, and external JavaScript files. I learned how JavaScript interacts with the Document Object Model (DOM) to modify page content, respond to user events, and validate user input. Understanding this interaction is essential because much of a web application's client-side logic executes inside the browser before requests are sent to the server.

From a security perspective, the room demonstrated how legitimate browser features can be abused. I learned about JavaScript dialog functions such as `alert()`, `confirm()`, and `prompt()`, how attackers may leverage them in phishing or proof-of-concept payloads, and why client-side validation and control flow should never be trusted as security mechanisms. The room also showed how modifying JavaScript code in the browser or bypassing client-side checks can circumvent application restrictions, reinforcing the importance of performing all security-critical validation on the server side.

Finally, the room introduced minified JavaScript files and explained why developers compress code to improve website performance. I learned how minification removes whitespace, comments, and readable variable names while preserving functionality, making manual analysis more difficult during security assessments. The module concluded with JavaScript security best practices, including avoiding sensitive logic on the client, validating input server-side, writing maintainable code, and understanding that any JavaScript delivered to a browser should be considered fully accessible to an attacker. These concepts provide the necessary foundation for studying web vulnerabilities such as Cross-Site Scripting (XSS), insecure client-side logic, and modern web application testing.

---

## Burp Suite: The Basics

This room introduced Burp Suite as one of the most widely used tools for web application security testing. I learned that Burp Suite functions as an intercepting proxy positioned between the browser and the target web application, allowing HTTP and HTTPS traffic to be captured, inspected, modified, and replayed before reaching the server. The room also explained the differences between the Community and Professional editions, while familiarising me with Burp's user interface and its core workflow for analysing web traffic. This knowledge forms the foundation for nearly every web penetration testing engagement. (https://tryhackme.com/room/burpsuitebasics)

A major focus of the room was configuring Burp Suite as the browser's proxy and understanding how intercepted requests travel between the client and the server. I learned how to install Burp's Certificate Authority (CA) certificate to inspect encrypted HTTPS traffic without browser errors, as well as how interception can be enabled or disabled depending on the testing scenario. Understanding this proxy architecture is essential because it allows testers to observe and manipulate application behaviour that would otherwise remain hidden within encrypted communications. (https://tryhackme.com/room/burpsuitebasics)

The room also introduced several of Burp Suite's core modules. I learned how **Proxy** captures and modifies requests in real time, **HTTP History** records all communication between the browser and target, **Repeater** allows requests to be manually edited and resent multiple times to observe different server responses, and **Target** provides an organised view of the application's discovered structure. Together, these modules enable systematic exploration of web applications, efficient testing of parameters, and detailed analysis of server behaviour without repeatedly navigating through the browser interface. (https://tryhackme.com/room/burpsuitebasics)

Finally, the room demonstrated how Burp Suite integrates into a typical web application assessment by allowing requests to be intercepted, modified, and replayed during vulnerability testing. I learned that manually manipulating HTTP requests is a critical technique for identifying insecure input validation, authentication flaws, access control issues, and other web vulnerabilities. The skills developed in this room establish the practical foundation required for more advanced Burp Suite modules covering Intruder, Decoder, Comparer, Extender, and the testing of vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), authentication bypasses, and insecure direct object references (IDOR). (https://tryhackme.com/room/burpsuitebasics)