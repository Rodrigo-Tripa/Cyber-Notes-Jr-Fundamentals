#burp-suite #proxy #web-security #pentesting #http #https #portswigger

> [!NOTE]
> This note is intentionally a **Lite Edition**. While it covers the fundamental concepts, architecture, core modules, and workflow of Burp Suite, it is not intended to be a complete reference.
>
> Burp Suite is an extensive platform with dozens of features, advanced configuration options, and a large ecosystem of extensions. A comprehensive guide would be significantly larger than the standard notes in this vault and would negatively impact readability and navigation.
>
> This document therefore focuses on the knowledge required to understand Burp Suite, use it effectively during web application security assessments, and establish a solid foundation. For advanced topics, detailed workflows, and in-depth module documentation, refer to the official PortSwigger documentation and additional learning resources.

# Burp Suite

## Overview

**Burp Suite** is an integrated platform for web application security testing developed by **PortSwigger**. It is considered the industry standard tool for manual web penetration testing and is widely used by penetration testers, bug bounty hunters, security researchers, and application security engineers.

Unlike packet analyzers such as [[Wireshark]], which inspect network traffic at multiple protocol layers, Burp Suite operates at the **application layer (Layer 7)**, focusing on HTTP, HTTPS, WebSockets, and modern web APIs. Its primary purpose is to allow testers to intercept, inspect, modify, replay, and automate HTTP requests and responses, making it significantly easier to understand how a web application behaves and identify security vulnerabilities.

Burp Suite is suitable for both learning web security and performing professional security assessments.

---

## How Burp Suite Works

Burp Suite acts as an **intercepting proxy**, positioning itself between the browser and the target web application.

```
Browser

↓

Burp Suite

↓

Target Application
```

Instead of communicating directly with the server, every request first passes through Burp Suite. This allows the tester to inspect or modify requests before they reach the application, as well as analyze the responses returned by the server.

When working with HTTPS, Burp performs TLS interception using its own Certificate Authority (CA), allowing encrypted traffic to be decrypted, inspected, and re-encrypted transparently.

---

## Core Modules

Burp Suite is organized into several modules, each designed for a specific stage of a web application assessment.

### Target

Builds a map of the application as you browse it, discovering hosts, directories, endpoints, APIs, JavaScript files, and other resources. It also allows defining the assessment's scope to keep testing organized.

### Proxy

The central component of Burp Suite. It intercepts HTTP(S) traffic between the browser and the target application, allowing requests and responses to be inspected, modified, forwarded, or dropped before reaching their destination.

### Repeater

Allows individual HTTP requests to be modified and resent repeatedly. It is primarily used for manual testing, enabling precise analysis of how the application responds to different inputs.

### Intruder

Automates repetitive requests by replacing selected values with payload lists. It is commonly used for fuzzing parameters, brute-forcing inputs, enumerating resources, and testing input validation.

### Decoder

Provides utilities for encoding and decoding common formats such as Base64, URL Encoding, HTML Encoding, and hexadecimal, simplifying the analysis of encoded application data.

### Comparer

Highlights the differences between two requests or responses, making it easier to identify subtle changes during authentication, authorization, or session testing.

### Logger

Maintains a searchable log of requests processed by Burp and can be configured to capture only specific traffic, helping organize large assessments.

### Extender

Allows Burp Suite to be extended through plugins, enabling additional functionality beyond the default feature set.

---

## BApp Store

Burp Suite includes access to the **BApp Store**, PortSwigger's official repository of extensions.

Extensions can significantly expand Burp's capabilities, adding support for technologies, automation, authentication testing, payload generation, logging improvements, and many other features.

Some of the most widely used extensions include:

- Logger++
- JWT Editor
- Hackvertor
- Autorize
- Param Miner
- Turbo Intruder

For most users, installing only the extensions required for the current assessment is preferable to loading a large number of plugins unnecessarily.

---

## Typical Workflow

A typical manual web application assessment follows a workflow similar to:

```
Configure Browser

↓

Browse Application

↓

Map the Target

↓

Capture Requests

↓

Analyze Traffic

↓

Send Requests to Repeater

↓

Modify Parameters

↓

Validate Responses

↓

Document Findings
```

Automation tools such as Intruder are generally introduced only after the application's behaviour has been understood through manual testing.

---

## Community vs Professional

Burp Suite is available in two primary editions.

The **Community Edition** is free and includes all the modules required to learn web application security and perform manual testing. However, some features such as Intruder are intentionally rate-limited, and advanced capabilities like the automated scanner and Burp Collaborator are unavailable.

The **Professional Edition** adds automated vulnerability scanning, unrestricted Intruder performance, Burp Collaborator, advanced reporting, AI-assisted features, and additional tools intended for commercial penetration testing.

---

## Advantages

- Industry-standard web security testing platform.
- Powerful HTTP and HTTPS interception.
- Excellent support for REST APIs and WebSockets.
- Highly extensible through the BApp Store.
- Combines manual and automated testing.
- Cross-platform.
- Active development and frequent updates.
- Large community and extensive official documentation.

---

## Limitations

Burp Suite cannot:

- Discover hosts like [[Nmap]].
- Capture raw network traffic like [[Wireshark]].
- Analyze packets below the application layer.
- Replace a complete penetration testing methodology.

It is a specialized tool for **web application security testing**, not a general-purpose network analysis tool.

---

## Best Practices

- Configure the application's scope before testing.
- Spend time understanding the application's functionality before attempting exploitation.
- Use Repeater for manual validation of potential vulnerabilities.
- Organize requests using meaningful Repeater tabs and Logger filters.
- Install only trusted extensions from the official BApp Store whenever possible.
- Keep Burp Suite and installed extensions up to date.

---

## Related Notes

- [[HTTP]]
- [[HTTPS]]
- [[Web-Architecture]]
- [[Cookies]]
- [[Sessions]]
- [[JavaScript]]
- [[SQL]]
- [[Wireshark]]
- [[Nmap]]

---

## Key Takeaways

- Burp Suite is the industry-standard platform for web application penetration testing.
- It functions primarily as an intercepting proxy between the browser and the target application.
- Its modular architecture supports every stage of a manual web security assessment, from mapping an application to validating vulnerabilities.
- While the Community Edition is sufficient for learning and many practical scenarios, the Professional Edition provides advanced automation and enterprise-focused features.
- Mastering modules such as **Proxy**, **Target**, and **Repeater** provides a strong foundation for understanding and testing modern web applications.