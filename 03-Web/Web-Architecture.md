# Web Architecture

#web #architecture #http #web-security #networking

## Overview

Web architecture describes how the components of a web application communicate to process client requests and deliver responses. Rather than being a single server, modern web applications consist of multiple interconnected services responsible for networking, application logic, data storage, security, and performance.

Understanding web architecture is fundamental for both web development and penetration testing, as vulnerabilities often arise from the interaction between these components rather than from a single system.

---

## Basic Request Flow

A typical web request follows this sequence:

```
Browser
    │
    ▼
DNS
    │
    ▼
Load Balancer (optional)
    │
    ▼
Reverse Proxy / Web Server
    │
    ▼
Application Server
    │
    ▼
Database
```

The server processes the request and returns an HTTP response following the reverse path until it reaches the client's browser.

---

## Components

### Browser

The browser is the client responsible for requesting web resources and rendering the returned content.

It sends HTTP or HTTPS requests, stores cookies, executes JavaScript, and displays HTML and CSS to the user.

Examples include Firefox, Chromium, Edge, and Safari.

---

### DNS

Before contacting a website, the browser resolves the domain name into an IP address using the Domain Name System (DNS).

For example:

```
example.com
      │
      ▼
93.184.216.34
```

Only after DNS resolution can the browser establish a network connection with the server.

---

### Load Balancer

Large applications often distribute incoming traffic across multiple servers using a load balancer.

Its responsibilities include:

- Distributing requests.
- Improving availability.
- Increasing scalability.
- Preventing individual servers from becoming overloaded.

Examples include HAProxy, Nginx, AWS Elastic Load Balancer, and Cloudflare Load Balancing.

---

### Reverse Proxy

A reverse proxy receives requests on behalf of backend servers and forwards them internally.

Unlike a forward proxy, which acts for the client, a reverse proxy represents the server.

Common responsibilities include:

- TLS termination.
- Request routing.
- Compression.
- Caching.
- Rate limiting.
- Hiding internal infrastructure.

Examples:

- Nginx
- Apache
- Traefik
- Caddy

---

### Web Server

The web server receives HTTP requests and serves static resources such as:

- HTML
- CSS
- JavaScript
- Images
- Downloads

If dynamic content is required, the request is forwarded to an application server.

Examples include Apache HTTP Server, Nginx, IIS, and Caddy.

---

### Application Server

The application server contains the business logic of the application.

Typical responsibilities include:

- Authentication
- Authorization
- Processing user input
- Executing application logic
- Communicating with databases
- Returning dynamically generated responses

Examples include:

- Node.js
- Django
- Flask
- Laravel
- Spring Boot
- ASP.NET

---

### Database

Most web applications store persistent information inside databases.

Examples of stored data include:

- User accounts
- Password hashes
- Orders
- Blog posts
- Configuration
- Logs

Common database systems include:

- MySQL
- PostgreSQL
- MariaDB
- Microsoft SQL Server
- SQLite
- MongoDB

---

### Web Application Firewall (WAF)

A WAF analyses HTTP traffic before it reaches the application.

It attempts to detect and block attacks such as:

- SQL Injection
- Cross-Site Scripting (XSS)
- Command Injection
- Path Traversal
- Malicious bots

Examples include:

- Cloudflare WAF
- AWS WAF
- ModSecurity

A WAF provides an additional security layer but should never replace secure application development.

---

### Content Delivery Network (CDN)

A CDN stores cached copies of static resources on geographically distributed servers.

Benefits include:

- Lower latency.
- Reduced server load.
- Faster downloads.
- Improved availability.
- Basic DDoS mitigation.

Examples include:

- Cloudflare
- Akamai
- Fastly
- Amazon CloudFront

---

## Static vs Dynamic Content

### Static Content

Static resources are returned exactly as they are stored.

Examples:

- HTML
- CSS
- Images
- PDFs
- JavaScript files

No server-side processing is required.

---

### Dynamic Content

Dynamic resources are generated during the request.

They often involve:

- Authentication
- Database queries
- User-specific content
- API calls
- Business logic

Most modern web applications generate dynamic responses.

---

## Forward Proxy vs Reverse Proxy

| Forward Proxy | Reverse Proxy |
|---------------|---------------|
| Represents the client | Represents the server |
| Used by end users | Used by web infrastructure |
| Often filters outgoing traffic | Routes incoming traffic |
| Example: Burp Suite, Squid | Example: Nginx, HAProxy |

---

## Intercepting Proxy

During security assessments, an **intercepting proxy** is placed between the browser and the target application.

```
Browser
    │
    ▼
Intercepting Proxy
(Burp Suite)
    │
    ▼
Target Web Application
```

An intercepting proxy allows testers to:

- Capture HTTP requests.
- Modify headers.
- Edit parameters.
- Replay requests.
- Analyse responses.
- Test application behaviour.

Common tools include:

- Burp Suite
- OWASP ZAP
- mitmproxy

---

## Typical Web Application Workflow

A simplified request lifecycle is:

1. The user enters a URL.
2. DNS resolves the domain name.
3. The browser establishes a TCP connection.
4. If HTTPS is used, a TLS handshake occurs.
5. The request reaches the reverse proxy or web server.
6. Static files are returned immediately or the request is forwarded to the application server.
7. The application server executes business logic.
8. If necessary, the application queries the database.
9. A response is generated.
10. The browser renders the returned content.

---

## Goal

Understanding web architecture provides the foundation for analysing how web applications process requests, manage resources, and enforce security. This knowledge is essential for understanding authentication mechanisms, session management, APIs, reverse proxies, web application firewalls, and common web vulnerabilities encountered during penetration testing.