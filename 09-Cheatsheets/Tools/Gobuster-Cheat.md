# Gobuster Cheat Sheet

#gobuster #cheatsheet #enumeration #web-security #reconnaissance

## Basic Syntax

```bash
gobuster <mode> [options]
```

Gobuster is organized around different enumeration modes. The most commonly used modes are:

```text
dir    Directory and file enumeration
dns    DNS subdomain enumeration
vhost  Virtual host enumeration
```

---

## Directory Enumeration

Basic directory enumeration:

```bash
gobuster dir -u http://TARGET -w wordlist.txt
```

* `dir` — Directory enumeration mode
* `-u` — Target URL
* `-w` — Wordlist

Example:

```bash
gobuster dir -u http://10.10.10.10 -w /path/to/wordlist.txt
```

Gobuster tests words from the wordlist as paths against the target.

For example:

```text
/admin
/login
/uploads
/backup
```

---

## File Enumeration

Specify extensions to test:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -x php,txt,html
```

This causes Gobuster to test combinations such as:

```text
/index.php
/index.txt
/index.html
/admin.php
/admin.txt
/admin.html
```

Multiple extensions can be separated by commas.

---

## Status Codes

By default, Gobuster reports responses that indicate potentially interesting resources. You can explicitly specify which status codes should be considered valid:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -s 200,204,301,302,307,401,403
```

Common HTTP status codes:

```text
200  OK
204  No Content
301  Moved Permanently
302  Found / Redirect
307  Temporary Redirect
401  Unauthorized
403  Forbidden
404  Not Found
```

A `403 Forbidden` response can be particularly interesting during enumeration because it may indicate that the resource exists but access is restricted.

---

## Excluding Status Codes

Instead of specifying allowed responses, unwanted status codes can be excluded:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -b 404
```

`-b` specifies status codes to blacklist.

This is useful when a server returns a consistent response for nonexistent resources.

---

## Response Size

Some applications return custom error pages with the same status code as valid resources. Response size can help distinguish them.

Display response information:

```bash
gobuster dir -u http://TARGET -w wordlist.txt
```

If the application produces false positives with identical response sizes, filtering can be useful:

```bash
gobuster dir -u http://TARGET -w wordlist.txt --exclude-length 1234
```

The value represents the response body length to exclude.

---

## Threads

Increase the number of concurrent requests:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -t 50
```

`-t` specifies the number of concurrent threads.

Higher concurrency can significantly increase enumeration speed, but it also increases traffic and can cause:

* Rate limiting
* Detection
* Network congestion
* Server instability

Use an appropriate value for the target environment.

---

## Request Timeout

Set a timeout for HTTP requests:

```bash
gobuster dir -u http://TARGET -w wordlist.txt --timeout 10s
```

Useful when the target responds slowly or has unreliable connectivity.

---

## User-Agent

Specify a custom User-Agent:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -a "Mozilla/5.0"
```

This can be useful when the server behaves differently depending on the HTTP client.

---

## Cookies

Send cookies with requests:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -c "session=VALUE"
```

Useful when enumerating resources that require an authenticated session.

---

## Authentication

For HTTP Basic Authentication:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -U username -P password
```

This supplies credentials for HTTP Basic Authentication.

For more complex authenticated applications, inspect the actual HTTP request with [[Burp Suite]] and determine whether cookies or custom headers are required.

---

## Custom Headers

Add HTTP headers:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -H "X-Custom-Header: value"
```

Multiple headers can be supplied when required by the target application.

Headers can be useful when testing APIs, authenticated applications, or applications that rely on custom request metadata.

---

## HTTPS

Gobuster can enumerate HTTPS targets directly:

```bash
gobuster dir -u https://TARGET -w wordlist.txt
```

If the target uses an invalid or self-signed TLS certificate:

```bash
gobuster dir -u https://TARGET -w wordlist.txt -k
```

`-k` disables TLS certificate verification.

---

# DNS Enumeration

DNS enumeration attempts to discover subdomains using a wordlist.

```bash
gobuster dns -d example.com -w subdomains.txt
```

* `dns` — DNS enumeration mode
* `-d` — Target domain
* `-w` — Subdomain wordlist

For example, a wordlist might discover:

```text
admin.example.com
dev.example.com
api.example.com
mail.example.com
```

---

## DNS Wildcard Detection

Some domains use wildcard DNS records, meaning that arbitrary subdomains resolve to the same address.

This can create false positives during subdomain enumeration.

Gobuster can detect wildcard DNS behaviour and help prevent these results from being interpreted as genuine discoveries.

Always investigate suspiciously broad DNS results before treating them as valid subdomains.

---

# Virtual Host Enumeration

Virtual host enumeration attempts to identify different websites hosted on the same server.

```bash
gobuster vhost -u http://TARGET -w vhosts.txt
```

A server can host multiple applications while using the same IP address:

```text
IP Address
    │
    ├── example.com
    ├── admin.example.com
    └── dev.example.com
```

The HTTP `Host` header determines which virtual host the web server should respond to.

---

## DNS vs Virtual Host Enumeration

These techniques are related but not identical.

DNS enumeration asks:

```text
Which subdomains resolve through DNS?
```

Virtual host enumeration asks:

```text
Which hostnames does the web server recognize?
```

A hostname may therefore be useful to test even if it is not publicly listed through ordinary DNS enumeration.

---

# Wordlists

Wordlists determine which names Gobuster will test.

For directory enumeration, useful candidates can include:

```text
admin
login
dashboard
uploads
backup
config
api
test
dev
```

For DNS enumeration:

```text
www
mail
vpn
dev
test
api
admin
portal
```

A larger wordlist provides broader coverage but increases the number of requests.

A targeted wordlist can be considerably more efficient when information about the target technology or application is already available.

---

# Useful Options

```text
-u URL              Target URL
-w WORDLIST         Wordlist
-x EXTENSIONS       File extensions
-s STATUS_CODES     Positive status codes
-b STATUS_CODES     Blacklisted status codes
-t THREADS          Concurrent threads
-H HEADER            Custom HTTP header
-c COOKIE            HTTP cookie
-a USER_AGENT        User-Agent
-k                  Ignore TLS certificate errors
-U USERNAME          HTTP authentication username
-P PASSWORD          HTTP authentication password
-o FILE              Output file
--exclude-length N   Exclude responses with specific length
--timeout TIME       Request timeout
```

---

# Output

Save results to a file:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -o gobuster.txt
```

This is useful for keeping enumeration results as part of penetration-testing documentation.

---

# Common Workflows

## Web Directory Enumeration

```text
Identify Web Service
        ↓
Determine HTTP/HTTPS
        ↓
Enumerate Directories
        ↓
Enumerate Files
        ↓
Investigate Interesting Resources
        ↓
Test Discovered Attack Surface
```

Example:

```bash
gobuster dir -u http://TARGET -w wordlist.txt
```

Then extend the enumeration:

```bash
gobuster dir -u http://TARGET -w wordlist.txt -x php,txt,html
```

---

## Subdomain Enumeration

```text
Identify Domain
      ↓
Select Subdomain Wordlist
      ↓
DNS Enumeration
      ↓
Validate Discovered Hosts
      ↓
Enumerate Interesting Hosts
```

Example:

```bash
gobuster dns -d example.com -w subdomains.txt
```

---

## Virtual Host Enumeration

```text
Identify Web Server
      ↓
Determine Domain
      ↓
Enumerate Candidate Hostnames
      ↓
Analyse HTTP Responses
      ↓
Investigate Valid Virtual Hosts
```

Example:

```bash
gobuster vhost -u http://TARGET -w vhosts.txt
```

---

# Gobuster + Nmap

[[Cyber-Notes-Jr-Fundamentals/07-Tools/Nmap]] can identify exposed ports and services before Gobuster is used.

Example workflow:

```bash
nmap -sV TARGET
```

If a web service is identified:

```bash
gobuster dir -u http://TARGET -w wordlist.txt
```

This follows the broader reconnaissance model:

```text
Network Enumeration
        ↓
Service Enumeration
        ↓
Web Enumeration
        ↓
Application Analysis
        ↓
Vulnerability Identification
```

---

# Gobuster + Burp Suite

[[Burp Suite]] can be used to inspect discovered web applications in greater detail.

Gobuster is useful for discovering resources:

```text
Gobuster
    ↓
/admin
/api
/backup
```

Burp Suite can then be used to analyse how those resources behave and how the application processes HTTP requests.

This makes the tools complementary rather than interchangeable.

---

# False Positives

One of the most important aspects of Gobuster is recognizing false positives.

Some web servers return the same response for:

```text
/does-not-exist
```

and:

```text
/real-resource
```

For example, both might return:

```text
HTTP 200
```

If this happens, status code alone is insufficient.

Compare:

* Response status
* Response length
* Response body
* Redirect behaviour
* Headers
* Application-specific error pages

Enumeration results should always be validated manually.

---

# Common Mistakes

### Using an inappropriate wordlist

A wordlist that does not match the target can produce poor coverage.

### Ignoring false positives

A `200` response does not automatically mean a real resource exists.

### Using excessive threads

High concurrency can trigger defensive mechanisms or overload fragile applications.

### Enumerating without reconnaissance

Gobuster is more effective when you already understand what service and application you are targeting.

### Treating enumeration as exploitation

Gobuster primarily discovers attack surface. The discovered resources must then be manually analysed for vulnerabilities or sensitive functionality.

---

# Quick Reference

```bash
# Directory enumeration
gobuster dir -u http://TARGET -w WORDLIST

# Directory + file extensions
gobuster dir -u http://TARGET -w WORDLIST -x php,txt,html

# Custom threads
gobuster dir -u http://TARGET -w WORDLIST -t 50

# Status codes
gobuster dir -u http://TARGET -w WORDLIST -s 200,301,302,403

# Exclude status code
gobuster dir -u http://TARGET -w WORDLIST -b 404

# Exclude response size
gobuster dir -u http://TARGET -w WORDLIST --exclude-length 1234

# HTTPS with invalid certificate
gobuster dir -u https://TARGET -w WORDLIST -k

# Custom header
gobuster dir -u http://TARGET -w WORDLIST -H "Header: value"

# Cookies
gobuster dir -u http://TARGET -w WORDLIST -c "session=VALUE"

# Save output
gobuster dir -u http://TARGET -w WORDLIST -o gobuster.txt

# DNS enumeration
gobuster dns -d example.com -w subdomains.txt

# Virtual host enumeration
gobuster vhost -u http://TARGET -w vhosts.txt
```

## Related Notes

* [[Cyber-Notes-Jr-Fundamentals/07-Tools/Gobuster]]
* [[Cyber-Notes-Jr-Fundamentals/07-Tools/Nmap]]
* [[Burp Suite]]
* [[Cyber-Notes-Jr-Fundamentals/03-Web/HTTP]]
* [[HTTPS]]
* [[Cyber-Notes-Jr-Fundamentals/02-Networking/DNS]]
* [[Web-Architecture]]
* [[Cyber-Notes-Jr-Fundamentals/03-Web/Websites]]
* [[Offensive-Security]]
