# Client-Server Model

## Overview

The **client-server model** is a network architecture in which **clients** request resources or services and **servers** provide and process those requests.

It is one of the fundamental models behind modern computer networks and the Internet. Services such as web browsing, DNS, email, file sharing, remote administration, and database access commonly rely on client-server communication.

The client and server are defined by their **role in the communication**, not necessarily by the physical device they run on. A single computer can act as a client for one service and a server for another.

## Client

A **client** is a device, application, or process that initiates communication with a server to request a resource or service.

The client normally consumes the service provided by the server and may be responsible for presenting the returned information to the user.

Common examples include:

- Web browsers
    
- Email clients
    
- SSH clients
    
- FTP clients
    
- Database clients
    
- Mobile applications
    
- Command-line utilities
    

A client does not necessarily require a graphical interface. A command-line SSH client or a program making a DNS query is also a client.

## Server

A **server** is a system or process that listens for incoming requests and provides a resource or service to clients.

Servers commonly run continuously or remain available whenever their service is required. Depending on the application, a server may authenticate users, process data, access databases, execute application logic, or return files.

Common examples include:

- **Web servers** - Serve websites and web applications.
    
- **DNS servers** - Resolve domain names and provide DNS information.
    
- **File servers** - Provide access to stored files.
    
- **Database servers** - Process queries and manage structured data.
    
- **Mail servers** - Send, receive, and store email.
    
- **SSH servers** - Provide remote command-line access.
    

A single server can handle requests from many clients simultaneously.

## Client-Server Communication

Client-server communication generally follows a **request-response model**.

The client sends a request to the server, the server processes the request, and the server returns a response.

```text
Client
  │
  │ Request
  ▼
Server
  │
  │ Response
  ▼
Client
```

The exact contents of the request and response depend on the protocol and service being used.

For example, an HTTP client may request a webpage while an HTTP server returns the requested HTML document.

## Protocols

Client-server communication requires **network protocols** that define how data is formatted, transmitted, and interpreted.

Common protocols include:

|Protocol|Typical Use|
|---|---|
|HTTP|Web communication|
|HTTPS|Secure web communication|
|DNS|Domain name resolution|
|SSH|Secure remote administration|
|FTP|File transfer|
|SMTP|Sending email|
|IMAP|Retrieving and managing email|

Protocols operate at different layers of the networking stack. For example, HTTP is an application-layer protocol, while TCP and UDP provide transport-layer communication.

## Ports and Services

Network services running on a server are commonly associated with **TCP or UDP ports**.

A port allows the operating system to determine which process should receive incoming network traffic.

Common examples include:

|Port|Protocol|Service|
|---|---|---|
|22|TCP|SSH|
|25|TCP|SMTP|
|53|TCP/UDP|DNS|
|80|TCP|HTTP|
|443|TCP|HTTPS|

These port assignments are conventional rather than mandatory. A service can be configured to listen on a different port.

From a cybersecurity perspective, identifying open ports and the services associated with them is an important part of **network enumeration** and **attack-surface analysis**.

## Example: Web Browser and Web Server

When a user accesses a website, the browser acts as the **client** and the web server acts as the **server**.

A simplified process is:

1. The browser needs the server's IP address.
    
2. DNS can be used to resolve the domain name.
    
3. The client establishes the required network connection.
    
4. The browser sends an HTTP or HTTPS request.
    
5. The web server processes the request.
    
6. The server returns an HTTP response.
    
7. The browser processes and displays the returned resources.
    

The response may contain HTML, CSS, JavaScript, images, JSON, or other resources.

This same basic client-server architecture is used by many applications beyond traditional websites.

## Stateful and Stateless Communication

Client-server systems can be **stateful** or **stateless**.

A **stateless** system does not require the server to retain information about previous requests in order to process a new request. Each request contains the information necessary for the server to handle it.

HTTP is fundamentally a **stateless protocol**. Web applications commonly introduce state through mechanisms such as cookies, sessions, and authentication tokens.

A **stateful** system maintains information about a client's previous interactions or current connection.

The distinction is particularly important in cybersecurity because authentication sessions, cookies, and tokens can contain security-sensitive information.

## Centralized Architecture

One advantage of the client-server model is **centralized resource management**.

Instead of every client maintaining its own copy of a resource, clients can access resources from a centralized server.

This makes it easier to:

- Manage resources.
    
- Apply access controls.
    
- Authenticate users.
    
- Monitor activity.
    
- Perform backups.
    
- Update services centrally.
    

However, centralization can also create a **single point of failure**. If a critical server becomes unavailable, many clients may lose access to the service.

Modern infrastructures therefore commonly use redundancy, load balancing, replication, and distributed architectures to reduce this risk.

## Client-Server vs Peer-to-Peer

The client-server model differs from a **peer-to-peer (P2P)** architecture.

In a traditional client-server architecture, clients primarily consume services while servers provide them.

In a P2P architecture, systems can act as both clients and servers and communicate directly with other peers.

Some modern systems use a **hybrid architecture**, combining centralized servers with peer-to-peer communication.

## Security Considerations

The client-server model creates several security boundaries that must be protected.

The server should not automatically trust information received from a client, and the client should not automatically trust information received from a server.

Important security properties include:

- **Authentication** - Verifying the identity of a user or system.
    
- **Authorization** - Determining what an authenticated entity is allowed to access.
    
- **Confidentiality** - Preventing unauthorized parties from reading communications.
    
- **Integrity** - Preventing unauthorized modification of data.
    
- **Availability** - Ensuring that services remain accessible.
    
- **Input validation** - Preventing malicious or malformed input from being processed unsafely.
    

Encryption protocols such as TLS can provide confidentiality and integrity for network communications, while authentication and authorization mechanisms control access to resources.

## Client-Server Model in Cybersecurity

Understanding client-server architecture is essential for cybersecurity because many attacks target the communication between clients and servers or the services exposed by servers.

During a security assessment, a tester may identify:

- Which hosts are reachable.
    
- Which ports are open.
    
- Which services are running.
    
- Which protocols are being used.
    
- Which versions of services are exposed.
    
- Which authentication mechanisms are present.
    
- Which resources can be accessed by different users.
    

Tools such as **Nmap**, **Wireshark**, and intercepting proxies can help security professionals observe and analyse these interactions.

For example, discovering that a server exposes TCP port `22` may indicate an SSH service. Identifying the service is only the beginning; further analysis can determine its configuration, authentication methods, version, and security posture.

The exposed services of a system collectively contribute to its **attack surface**.

## Key Takeaways

The **client-server model** separates the roles of requesting and providing services.

A **client** initiates requests and consumes resources, while a **server** processes requests and provides services.

Communication is governed by protocols such as HTTP, HTTPS, DNS, SSH, and FTP, while transport protocols such as TCP and UDP provide network communication between endpoints.

Servers commonly expose services through network ports. Identifying these services is fundamental to network administration and cybersecurity activities such as enumeration and attack-surface analysis.

Understanding the client-server model provides the foundation for studying networking, web applications, authentication, network enumeration, firewalls, and common network attacks.