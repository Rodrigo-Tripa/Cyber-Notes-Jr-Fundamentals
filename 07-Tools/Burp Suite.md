#burp-suite #web-security #pentesting #http #https #proxy #portswigger

> [!NOTE]
> This document is the **complete edition** of the Burp Suite notes. It provides a far more detailed explanation of Burp Suite's architecture, modules, workflows, advanced features, and practical usage than the standard note.
>
> If you are looking for a concise reference or are just getting started, the **[[Burp Suite Lite]]** note is recommended, as it covers the essential concepts in a shorter and more approachable format.
>
> Due to its size and level of detail, this version is primarily intended for **security professionals, penetration testers, bug bounty hunters, and advanced learners** who want a deeper understanding of Burp Suite and its capabilities.

# Burp Suite

# Part 1 - Introduction and Fundamentals

> *"Burp Suite is not simply a proxy. It is a complete web application security testing platform that allows security professionals to understand, analyze, manipulate, and assess every aspect of HTTP and HTTPS communication between a client and a web application."*

---

# What is Burp Suite?

**Burp Suite** is an integrated platform developed by **PortSwigger** for testing the security of web applications and APIs.

Unlike traditional network analysis tools such as Wireshark or Tcpdump, Burp Suite operates at the **application layer (Layer 7)**, allowing security professionals to inspect, modify, replay, and automate HTTP(S) communication.

It has become the de facto standard for professional web application penetration testing and is used by:

- Penetration Testers
- Red Team Operators
- Security Consultants
- Bug Bounty Hunters
- Application Security Engineers
- Web Developers
- Security Researchers

Burp Suite can be used during every phase of a web assessment, from reconnaissance to vulnerability validation and final reporting.

---

# Why Burp Suite Exists

Modern web applications are extremely complex.

A single request may involve:

- Cookies
- Authentication tokens
- Sessions
- JWTs
- APIs
- JSON
- XML
- CSRF Tokens
- Multiple redirects
- JavaScript-generated requests
- WebSockets

Although browsers hide most of this complexity, understanding and manipulating these communications is essential during a security assessment.

Burp Suite exposes everything that normally happens behind the scenes.

Instead of guessing what a browser is sending, Burp allows you to see the exact request before it reaches the server.

Even more importantly, it allows you to modify that request.

For example:

- Change parameters
- Remove authentication
- Modify cookies
- Replay requests
- Edit headers
- Test edge cases
- Send malformed input
- Compare responses

This ability is fundamental because many vulnerabilities only appear after altering requests in ways a normal browser would never generate.

---

# The Philosophy Behind Burp Suite

Burp Suite follows a simple philosophy:

> Never trust what the browser shows you.
>
> Trust what is actually being transmitted.

Everything displayed in a browser is simply the result of HTTP communication.

Burp works directly with that communication.

Rather than interacting with buttons, forms, and menus, Burp allows you to work with the protocol itself.

This provides complete visibility into the application's behaviour.

---

# The Client-Server Model

Every web application follows the same basic communication model.

```
Client
(Browser)

        │

HTTP / HTTPS

        │

        ▼

Server
(Web Application)
```

The browser creates an HTTP request.

The server processes it.

The server returns an HTTP response.

The browser renders that response.

Although this appears simple, hundreds of requests may occur while loading a single webpage.

Burp allows every one of them to be inspected.

---

# Burp's Position

Burp Suite inserts itself between the browser and the web server.

Instead of communicating directly with the target, the browser communicates with Burp.

```
Browser

    │

    ▼

Burp Suite

    │

    ▼

Target Application
```

This architecture is known as an **Intercepting Proxy**.

---

# What is an Intercepting Proxy?

A proxy is a system that forwards requests between two parties.

Burp is a **forward intercepting proxy**.

Its responsibilities include:

- Receiving requests from the browser
- Displaying them to the tester
- Allowing modification
- Forwarding them to the server
- Receiving responses
- Allowing inspection
- Returning responses to the browser

Nothing reaches the server without first passing through Burp.

This gives the tester complete control over HTTP communication.

---

# Browser Without Burp

```
Browser
     │
     ▼
Target
```

Simple.

No inspection.

No modification.

No replay.

---

# Browser With Burp

```
Browser

     │

     ▼

Burp Suite

     │

     ▼

Target
```

Now every request can be:

- Captured
- Modified
- Replayed
- Dropped
- Logged
- Compared

---

# Why This Is Powerful

Imagine a login request.

Normally, your browser sends something similar to:

```http
POST /login HTTP/1.1

username=alice
password=password123
```

Without Burp, this request immediately reaches the server.

With Burp:

```
Browser

↓

Burp intercepts

↓

Tester edits request

↓

Burp forwards request

↓

Server
```

The tester may decide to change:

```http
username=administrator
```

or

```http
password=' OR 1=1--
```

or remove cookies entirely.

None of these actions require changing the application's source code.

Burp simply edits the network traffic.

---

# Burp Works With HTTP

Burp understands HTTP natively.

It recognizes:

- Methods
- Headers
- Cookies
- Parameters
- Multipart forms
- JSON
- XML
- URL Encoding
- Base64
- GraphQL
- REST APIs

This makes testing considerably easier than manually editing raw packets.

---

# Burp Works With HTTPS

One of the first questions beginners ask is:

> "How can Burp read HTTPS if HTTPS is encrypted?"

The answer lies in TLS interception.

Normally:

```
Browser

======= TLS =======

Server
```

Burp creates two encrypted connections instead.

```
Browser

==== TLS ====

Burp

==== TLS ====

Server
```

Burp decrypts the traffic in the middle.

The browser accepts this because Burp installs its own trusted Certificate Authority (CA).

This allows encrypted traffic to be viewed without breaking HTTPS.

This process is discussed in much greater detail later in this document.

---

# Common Use Cases

Burp Suite is commonly used to:

- Test authentication systems
- Analyse cookies
- Modify requests
- Replay API calls
- Test file uploads
- Validate access controls
- Manipulate JSON requests
- Discover hidden endpoints
- Enumerate parameters
- Test web APIs
- Analyze JWTs
- Validate input filtering
- Inspect WebSockets
- Perform manual vulnerability verification

It is used in virtually every modern web penetration test.

---

# Typical Workflow

Although Burp contains dozens of modules, the workflow generally follows the same pattern.

```
Configure Browser

↓

Browse Target

↓

Capture Requests

↓

Map Application

↓

Choose Interesting Request

↓

Modify Request

↓

Replay

↓

Observe Response

↓

Repeat
```

As the assessment progresses, Burp becomes the central hub for almost every testing activity.

---

# Manual vs Automated Testing

Burp supports both manual and automated testing.

Manual testing provides maximum control and is preferred when analysing complex application logic.

Automated testing speeds up repetitive tasks such as fuzzing parameters or crawling applications.

Professional testers usually combine both approaches.

Automation finds opportunities.

Manual testing confirms and exploits them.

---

# Burp Community vs Professional

Burp Suite is available in several editions.

### Community Edition

Free.

Provides the core functionality needed for learning web security.

Includes:

- Proxy
- Target
- Repeater
- Decoder
- Comparer
- HTTP History
- Extender
- BApp Store

Limitations include:

- Rate-limited Intruder
- No Scanner
- No Collaborator Server
- No AI features
- Limited automation

Despite these limitations, the Community Edition remains one of the best tools available for learning web penetration testing.

---

### Professional Edition

Commercial.

Designed for professional security consultants and penetration testers.

Adds features such as:

- Automated Scanner
- Fast Intruder
- Burp Collaborator
- Audit Checks
- CI/CD Integration
- Advanced Reporting
- AI Assistance
- Better Automation
- Enterprise Workflow

Most commercial penetration testing companies use the Professional edition.

---

# Learning Burp Suite

Burp can initially appear overwhelming.

The interface contains dozens of tabs, modules, settings, and options.

Fortunately, only a handful of modules are required to perform most web penetration tests.

The remaining modules gradually become useful as assessments become more advanced.

A good learning strategy is:

1. Understand HTTP.
2. Learn the Proxy.
3. Learn Repeater.
4. Learn Target.
5. Learn Intruder.
6. Learn Extensions.

Trying to master every feature immediately often leads to confusion.

Understanding the workflow is far more important than memorising every menu.

---

# Key Takeaways

After reading this chapter, you should understand that:

- Burp Suite is an integrated web security testing platform.
- It operates as an intercepting proxy.
- It allows complete inspection and modification of HTTP(S) traffic.
- It is the industry-standard tool for manual web application penetration testing.
- Understanding HTTP is far more important than memorising Burp's interface.
- Nearly every feature in Burp ultimately revolves around analysing and manipulating client-server communication.

The following chapters will examine each Burp module in depth, explaining not only how to use it, but also why it exists and how professional penetration testers integrate it into their workflow.

# Part 2 - Installation, Projects, Interface and Initial Configuration

Before Burp Suite can be used effectively, it must be configured correctly. Fortunately, the default configuration is sufficient for most beginner and intermediate assessments, but understanding what Burp is doing behind the scenes will make troubleshooting significantly easier later on.

Unlike many penetration testing tools that require extensive command-line interaction, Burp Suite provides a graphical interface where every action can be observed visually. Nevertheless, almost every option has a purpose, and understanding these settings early will prevent confusion when working on larger web applications.

---

# Installing Burp Suite

Burp Suite is developed by **PortSwigger** and is available for:

- Linux
- Windows
- macOS

The official installer can always be downloaded from:

https://portswigger.net/burp

Avoid downloading Burp from unofficial sources.

Because Burp receives frequent security updates and feature improvements, using the latest stable version is highly recommended.

---

# Community vs Professional Installation

The installation process is identical.

The difference is determined by the license.

Without a license, Burp automatically starts in **Community Edition**.

With a valid license, Burp unlocks all Professional features.

---

# Java Runtime

Modern Burp releases already include their own Java Runtime Environment (JRE).

Older versions required installing Java manually.

Today, this is no longer necessary.

---

# First Launch

The first time Burp starts, it presents several options.

Typically you will see:

```
New Project

Open Existing Project

Open Temporary Project
```

Most beginners immediately choose **Temporary Project**, which is perfectly acceptable.

However, understanding the difference between these project types becomes important during long engagements.

---

# Temporary Projects

A temporary project stores its configuration only while Burp is running.

Once Burp closes, everything disappears.

This is ideal for:

- TryHackMe
- Hack The Box
- CTFs
- Small exercises
- Learning

Advantages:

- Fast
- No configuration required
- No files created

Disadvantages:

- History is lost
- Configuration is not saved

---

# Project Files

Project files permanently save Burp's state.

They contain information such as:

- Proxy History
- Site Map
- Scope
- Logger entries
- Repeater tabs
- Intruder attacks
- Settings

These files become extremely useful during:

- Professional engagements
- Long bug bounty investigations
- Large applications
- Multi-day assessments

Instead of rebuilding the project every day, Burp simply reloads the previous session.

---

# User Configuration

After selecting the project type, Burp asks which configuration should be loaded.

Most users simply select:

```
Use Burp Defaults
```

The default configuration is suitable for almost every assessment.

Later, experienced testers often maintain multiple configuration profiles depending on the target.

---

# The Main Interface

When Burp opens, it may initially appear intimidating.

There are numerous tabs, panels, buttons and menus.

Fortunately, the interface follows a logical structure.

At the highest level, Burp is divided into modules.

Each module performs a specific task.

For example:

```
Dashboard

Target

Proxy

Intruder

Repeater

Logger

Extensions
```

Every module focuses on a different phase of testing.

---

# Navigation Bar

The navigation bar contains Burp's primary modules.

Think of these tabs as separate workspaces.

Each workspace specialises in one activity.

For example:

- Proxy captures traffic.
- Repeater edits requests.
- Logger stores traffic.
- Extensions adds functionality.

Rather than trying to understand every tab immediately, learn one module at a time.

---

# Dashboard

The Dashboard is Burp's control center.

Depending on the edition, it displays:

- Running tasks
- Crawl progress
- Scan progress
- Issues
- Event Log
- Notifications

Community Edition mainly uses the Dashboard as an event viewer.

Professional Edition also displays automated scan information.

---

# Event Log

The Event Log records everything Burp is doing internally.

Examples include:

- Proxy started
- Certificate installed
- Extensions loaded
- Errors
- Scanner events

If something behaves unexpectedly, this is often the first place to investigate.

---

# Target

The Target module represents everything Burp has discovered about the application.

It eventually contains:

- Hosts
- Directories
- Files
- Parameters
- APIs
- JavaScript files

This module gradually builds a map of the application while browsing.

It will be covered extensively later.

---

# Proxy

The Proxy module is Burp's heart.

Every HTTP request normally passes through here.

Its responsibilities include:

- Interception
- Forwarding
- Modification
- History
- WebSockets

Most beginners spend the majority of their time inside Proxy and Repeater.

---

# Repeater

Repeater allows individual requests to be modified and resent.

Unlike the browser, which automatically follows user interactions, Repeater gives complete manual control.

This becomes one of the most heavily used modules during manual testing.

---

# Logger

Logger records requests and responses that Burp processes.

Unlike HTTP History, Logger can be customised to capture very specific events.

Professional testers often use Logger during long assessments.

---

# Extensions

Extensions allow Burp to gain entirely new capabilities.

They can add:

- JWT editors
- GraphQL tools
- Active scanning improvements
- Parameter discovery
- Authorization testing
- Custom payload generators

The Burp ecosystem is one of its greatest strengths.

Extensions will be discussed in detail later.

---

# Understanding the Workflow

A beginner often believes Burp works like this:

```
Open Burp

↓

Hack Website
```

In reality, the workflow is much more structured.

```
Configure Browser

↓

Configure Proxy

↓

Browse Application

↓

Understand Functionality

↓

Capture Requests

↓

Identify Interesting Traffic

↓

Send Requests to Other Modules

↓

Perform Testing

↓

Document Findings
```

Notice that most of the time is spent understanding the application before attempting any exploitation.

---

# Configuring the Browser

Burp does not magically receive traffic.

The browser must be configured to use Burp as its proxy.

By default Burp listens on:

```
127.0.0.1

Port 8080
```

Every request generated by the browser is sent to Burp first.

Burp then forwards it to the destination.

Without this configuration, Burp cannot inspect traffic.

---

# Burp Browser

Recent versions of Burp include a built-in Chromium-based browser.

Advantages include:

- Preconfigured proxy settings
- Automatic certificate trust
- Isolated browsing environment
- Easier testing

For beginners, the Burp Browser is usually the simplest option.

Professional testers often alternate between Burp Browser and their preferred browser depending on the engagement.

---

# External Browsers

Many professionals still use Firefox.

Reasons include:

- Better extension ecosystem
- FoxyProxy support
- Multiple browser profiles
- Familiar development tools

Using an external browser requires additional configuration, including importing Burp's CA certificate.

This process will be covered in a later chapter.

---

# Default Proxy Listener

When Burp starts, it automatically creates a listener.

Typically:

```
127.0.0.1:8080
```

This means Burp accepts connections only from the local machine.

Additional listeners can be created if necessary.

---

# Why Beginners Think Burp Is Broken

One of the most common mistakes is forgetting that Burp is intercepting traffic.

The browser appears frozen.

No pages load.

Nothing happens.

In reality, Burp is simply waiting.

The request is paused inside the Proxy module.

Until the tester clicks **Forward**, the request never reaches the server.

This behaviour surprises almost everyone the first time they use Burp.

It is not a bug.

It is the entire purpose of an intercepting proxy.

---

# Key Takeaways

After completing the installation and initial configuration, you should understand:

- How Burp projects work.
- The difference between temporary and persistent projects.
- The purpose of the main interface.
- The role of each primary module.
- Why Burp must be configured as the browser's proxy.
- Why requests sometimes appear to "freeze" during interception.

The next chapter explores Burp's core modules in depth, beginning with **Target**, **Proxy**, **HTTP History**, and **Repeater**, which together form the foundation of nearly every manual web application security assessment.

# Part 3 - Core Modules

At first glance, Burp Suite may appear to be a single application. In reality, it is a collection of specialized modules designed to perform different tasks during a web application security assessment.

Although Burp contains many modules, only a small number are used continuously during almost every penetration test. Understanding these core modules and how they interact is significantly more valuable than memorizing every menu or option.

A common workflow is illustrated below:

```
Target

↓

Proxy

↓

HTTP History

↓

Repeater

↓

Intruder

↓

Extensions
```

Each module builds upon information gathered by the previous one.

---

# Target

The **Target** module is responsible for organizing everything Burp discovers about the application.

Rather than simply recording requests, Target builds a structured map of the web application.

Think of it as Burp's understanding of the target.

As you browse the website, Burp automatically learns:

- Domains
- Subdomains
- Directories
- Pages
- Static resources
- JavaScript files
- APIs
- Parameters
- Cookies

Over time, this creates a complete representation of the application's attack surface.

---

## Site Map

The most important feature inside Target is the **Site Map**.

The Site Map automatically organizes resources into a directory tree similar to a filesystem.

Example:

```
example.com

├── /
├── /login
├── /register
├── /dashboard
├── /admin
├── /api
│   ├── /users
│   └── /settings
└── /logout
```

Instead of manually remembering every endpoint, Burp maintains the structure automatically.

Professional testers constantly refer back to the Site Map throughout an engagement.

---

## Why the Site Map Matters

The Site Map helps identify:

- Hidden directories
- Administrative interfaces
- Backup files
- APIs
- Authentication pages
- JavaScript resources
- Static assets

It also reveals the application's overall complexity.

Large enterprise applications may contain thousands of discovered endpoints.

---

# Scope

One of Burp's most important concepts is the **Scope**.

Scope defines which targets belong to the current assessment.

Without Scope, Burp records everything.

That includes:

- Google
- CDN resources
- Analytics
- Fonts
- Images
- Advertisements

This quickly becomes overwhelming.

Instead, Burp allows testers to specify exactly which domains should be analyzed.

Example:

```
https://app.example.com
```

Everything else can be ignored.

Keeping a clean Scope dramatically improves efficiency.

---

## Benefits of Scope

Using Scope provides several advantages.

It:

- Reduces noise
- Keeps history organized
- Prevents accidental testing of unrelated domains
- Simplifies reporting
- Helps automated tools remain focused

One of the first tasks in any professional engagement is correctly defining Scope.

---

# Proxy

The **Proxy** module is Burp's central component.

Every HTTP request normally passes through it.

Its primary responsibilities include:

- Capturing requests
- Modifying requests
- Forwarding traffic
- Recording communication
- Managing WebSocket traffic

Without Proxy, Burp loses most of its functionality.

---

## Request Flow

When Proxy is active:

```
Browser

↓

Burp Proxy

↓

Web Server
```

Every request follows this path.

The tester can decide whether to:

- Forward
- Drop
- Edit

before the request reaches the server.

---

# Intercept

The **Intercept** tab pauses requests before they leave the browser.

Instead of immediately forwarding traffic, Burp waits for user input.

Example:

```
POST /login
```

Burp stops.

Nothing reaches the server.

The tester may now inspect the request.

Possible actions include:

- Forward
- Drop
- Edit
- Send to Repeater
- Send to Intruder
- Send to Decoder
- Send to Comparer

Only after forwarding does the request continue.

---

## Forward

Forward sends the request unchanged.

```
Browser

↓

Burp

↓

Server
```

This is the normal behaviour when no modifications are required.

---

## Drop

Drop simply discards the request.

The server never receives it.

This is useful for testing:

- Client behaviour
- Timeouts
- Missing requests
- Error handling

---

## Editing Requests

One of Burp's greatest strengths is allowing requests to be modified before transmission.

Examples include changing:

```
username=administrator
```

```
role=user
```

to

```
role=admin
```

or

```
price=25
```

to

```
price=1
```

The browser itself would never generate these requests.

Burp makes them possible.

---

# HTTP History

While Intercept pauses traffic, **HTTP History** records it.

Every request and response is stored automatically.

Information typically includes:

- Method
- Host
- URL
- Status Code
- MIME Type
- Response Length
- Timestamp

HTTP History effectively becomes the audit trail of the assessment.

---

## Why HTTP History Is Important

During testing, it is common to revisit earlier requests.

Perhaps a parameter looked interesting.

Perhaps authentication changed.

Perhaps a hidden API was discovered.

Instead of reproducing user actions manually, testers simply locate the original request inside HTTP History.

---

## Filtering History

Large applications may generate thousands of requests.

Burp allows filtering by:

- Status Code
- Host
- Extension
- MIME Type
- Search Terms
- Scope

Learning to filter effectively saves considerable time.

---

# WebSockets History

Modern applications increasingly rely on WebSockets.

Unlike HTTP, which follows a request-response model, WebSockets establish a persistent bidirectional connection.

Burp records these messages separately.

Examples include:

- Live chat
- Notifications
- Multiplayer games
- Dashboards
- Stock prices

Being able to inspect WebSocket communication is essential when testing modern web applications.

---

# Repeater

If Proxy is Burp's heart, **Repeater** is its laboratory.

Repeater allows a single request to be modified and sent repeatedly.

Unlike a browser, Repeater never changes the request automatically.

Every request remains exactly as the tester defines it.

---

## Typical Workflow

```
Capture Request

↓

Send to Repeater

↓

Modify Parameter

↓

Send

↓

Observe Response

↓

Modify Again

↓

Send Again
```

This process may be repeated hundreds of times during an assessment.

---

## Why Repeater Exists

Imagine testing an IDOR vulnerability.

Instead of logging in repeatedly, the tester simply changes:

```
user_id=15
```

↓

```
user_id=16
```

↓

```
user_id=17
```

↓

```
user_id=18
```

Each request can be sent instantly.

Repeater dramatically speeds up manual testing.

---

## Multiple Tabs

Repeater supports multiple tabs simultaneously.

A tester might dedicate one tab to:

- Authentication
- API Testing
- File Uploads
- JWTs
- Admin Panel
- GraphQL

This keeps testing organized.

---

# Intruder

Intruder automates repetitive requests.

Instead of changing parameters manually, Burp generates many requests automatically.

Examples include:

- Username enumeration
- Password spraying
- Parameter fuzzing
- Directory guessing
- Header testing
- Token brute forcing

Community Edition intentionally limits Intruder's speed.

Professional Edition removes this limitation.

---

## Attack Positions

Intruder first identifies which parts of a request should change.

These are called **Positions**.

Example:

```
username=§admin§
```

Burp replaces everything inside the markers with payloads.

---

## Payloads

Payloads are the values Burp inserts.

Examples include:

```
admin

administrator

root

test

guest
```

or

```
1

2

3

4

5
```

Payload lists may contain millions of entries.

---

# Decoder

Many web applications encode information.

Examples include:

- URL Encoding
- Base64
- HTML Encoding
- Hexadecimal

Decoder converts between formats.

Example:

```
SGVsbG8=
```

↓

```
Hello
```

It also supports hashing and format conversion.

---

# Comparer

Comparer analyzes differences between two requests or responses.

This is particularly useful when only small changes exist.

Instead of manually inspecting hundreds of lines, Burp highlights differences automatically.

Typical uses include:

- Comparing authenticated responses
- Session analysis
- Role comparisons
- JWT changes
- API responses

---

# Logger

Logger records traffic passing through Burp.

Unlike HTTP History, Logger allows much greater customization.

It can selectively record:

- Specific tools
- Particular hosts
- Certain response codes
- Extension-generated traffic

Large engagements often rely heavily on Logger.

---

# Organizer

Organizer provides a simple method for bookmarking important findings.

Rather than searching through thousands of requests later, interesting requests can be saved immediately.

Examples include:

- Authentication bypasses
- Potential SQL Injection
- XSS candidates
- Interesting APIs
- Sensitive responses

Think of Organizer as Burp's notebook.

---

# How the Modules Work Together

Professional testers rarely remain inside a single module.

Instead, requests flow naturally between tools.

Example:

```
Target

↓

Proxy

↓

HTTP History

↓

Repeater

↓

Intruder

↓

Comparer

↓

Organizer
```

Each module performs one task exceptionally well.

Combined, they form a complete manual testing workflow.

---

# Key Takeaways

After studying Burp's core modules, you should understand that:

- **Target** maps the application.
- **Scope** defines what belongs to the assessment.
- **Proxy** intercepts HTTP traffic.
- **HTTP History** records communication.
- **Repeater** enables precise manual testing.
- **Intruder** automates repetitive requests.
- **Decoder** converts encoded data.
- **Comparer** identifies differences.
- **Logger** stores customizable traffic logs.
- **Organizer** bookmarks important findings.

These modules represent the foundation of nearly every web application penetration test. Mastering them is considerably more valuable than attempting to learn every Burp feature at once, as they form the workflow used daily by professional penetration testers.

# Part 4 - Advanced Features and Extensibility

Once the core modules become familiar, Burp Suite begins to reveal its true strength. Beyond intercepting and replaying HTTP requests, Burp provides a collection of advanced features that significantly improve efficiency during professional security assessments.

Many experienced penetration testers spend as much time configuring Burp as they do actively testing an application. A well-configured Burp environment can automate repetitive tasks, simplify authentication workflows, improve visibility into application behaviour, and dramatically reduce the time required to validate vulnerabilities.

---

# Match and Replace

One of Burp's most underrated features is **Match and Replace**.

Instead of manually editing every request, Burp can automatically modify traffic as it passes through the proxy.

Examples include:

- Adding custom headers
- Removing headers
- Replacing cookies
- Modifying User-Agent strings
- Rewriting hostnames
- Updating API tokens

For example, every outgoing request could automatically receive:

```http
X-Test: BurpSuite
```

or

```http
User-Agent: Mozilla/5.0 Pentest
```

without any manual intervention.

This feature is particularly useful during repetitive API testing or when bypassing application restrictions.

---

# Session Handling Rules

Many modern web applications rely on short-lived authentication tokens.

Examples include:

- CSRF Tokens
- JWTs
- OAuth Tokens
- Session Cookies

Manually updating these values quickly becomes frustrating.

Session Handling Rules allow Burp to automate this process.

Burp can:

- Extract tokens from responses.
- Update requests automatically.
- Refresh expired sessions.
- Re-authenticate when necessary.
- Execute custom authentication workflows.

Professional testers frequently rely on Session Handling Rules during long engagements.

---

# Macros

Macros automate sequences of HTTP requests.

Imagine an application that requires the following workflow:

```
Login

↓

Dashboard

↓

Generate CSRF Token

↓

Submit Form
```

Instead of performing these actions manually every time, Burp can execute them automatically before sending the final request.

This is especially useful for:

- Multi-step authentication
- Shopping carts
- Administrative panels
- Complex workflows
- Applications using anti-CSRF protections

---

# Cookie Jar

Burp includes its own **Cookie Jar**.

Rather than depending entirely on the browser, Burp manages cookies internally.

This allows:

- Session persistence
- Automatic cookie updates
- Manual cookie editing
- Cookie synchronization
- Multiple simultaneous sessions

During testing, cookies often represent authenticated users.

Understanding how Burp stores and updates them is essential.

---

# Authentication Testing

Many web vulnerabilities involve authentication.

Burp greatly simplifies testing scenarios such as:

- Session fixation
- Session hijacking
- Cookie manipulation
- JWT modification
- Missing authentication
- Broken authorization
- Privilege escalation

Because every request can be edited before transmission, testers can easily observe how applications behave when authentication data changes.

---

# Cross-Site Request Forgery (CSRF)

Applications commonly protect forms using CSRF tokens.

Burp helps testers:

- Locate tokens.
- Observe where they are generated.
- Verify whether tokens change.
- Replay requests.
- Test missing or invalid tokens.

Combined with Session Handling Rules, Burp can automatically refresh CSRF tokens before each request.

---

# Sequencer

Some applications generate values that appear random.

Examples include:

- Session IDs
- Password reset tokens
- CSRF tokens
- API Keys

The **Sequencer** module analyzes whether these values are actually random.

It performs statistical analysis on large numbers of generated tokens.

Weak randomness may indicate vulnerabilities that allow attackers to predict future values.

Although beginners rarely use Sequencer, it is an extremely valuable tool during professional engagements.

---

# Burp Collaborator

Burp Collaborator is available in the Professional Edition.

It provides an external server that detects interactions initiated by the target application.

This makes it possible to identify vulnerabilities that do not produce immediate responses.

Examples include:

- Blind SSRF
- Blind XXE
- Blind Command Injection
- Blind Deserialization
- Blind Out-of-Band SQL Injection

Rather than returning output directly to the browser, the vulnerable application contacts the Collaborator server.

Burp records these interactions automatically.

---

# Burp Browser

Burp includes its own Chromium-based browser.

Unlike a standard browser, Burp Browser is already configured for:

- Proxy settings
- Certificate trust
- Cookie handling
- Isolation from personal browsing

Advantages include:

- No additional setup.
- Cleaner testing environment.
- Fewer browser-related issues.
- Easy reset between engagements.

Many professionals still prefer Firefox, but Burp Browser remains an excellent choice for learning and quick assessments.

---

# TLS Configuration

Burp allows extensive customization of TLS settings.

Examples include:

- Supported protocol versions
- Cipher suites
- Client certificates
- Upstream TLS configuration
- Server certificate validation

Most users never modify these settings.

However, understanding that they exist can be valuable when testing legacy or enterprise environments.

---

# Certificate Management

Burp automatically generates certificates for intercepted HTTPS connections.

Internally, the process is:

```
Browser

↓

Burp CA

↓

Temporary Certificate

↓

Browser Trusts Certificate

↓

Encrypted Connection
```

Without trusting Burp's Certificate Authority, browsers will display certificate warnings for every intercepted HTTPS request.

Proper certificate installation is therefore one of the first steps when configuring Burp.

---

# Performance Considerations

Large applications can generate tens of thousands of HTTP requests.

Several practices help maintain Burp's performance:

- Configure Scope early.
- Filter HTTP History.
- Disable unnecessary logging.
- Close unused Repeater tabs.
- Remove inactive extensions.
- Archive completed projects.

Good project organization becomes increasingly important as assessments grow.

---

# Extender

One of Burp Suite's greatest strengths is its extensibility.

The **Extender** module allows additional functionality to be added through extensions.

Rather than modifying Burp itself, developers create extensions that integrate directly into the platform.

These extensions can:

- Add new tabs.
- Analyze traffic.
- Generate payloads.
- Manipulate requests.
- Detect vulnerabilities.
- Improve workflows.

This modular architecture allows Burp to evolve far beyond its default capabilities.

---

# BApp Store

The **BApp Store** is PortSwigger's official extension repository.

It provides a curated collection of community-developed extensions that can be installed directly from within Burp.

Unlike downloading scripts from random websites, extensions available through the BApp Store undergo review before publication, making it the safest and most reliable source for expanding Burp's functionality.

The BApp Store continues to grow and contains extensions for nearly every stage of a web application assessment.

---

# Popular Extensions

Although hundreds of extensions are available, a small number have become industry favourites.

## Logger++

One of the most popular extensions available.

Logger++ provides significantly more powerful logging capabilities than Burp's default Logger.

Features include:

- Advanced filtering
- Color coding
- Searching
- Better organization
- Long-term traffic analysis

---

## JWT Editor

JWT Editor simplifies the analysis and modification of JSON Web Tokens.

It allows testers to:

- Decode JWTs
- Edit claims
- Modify headers
- Re-sign tokens
- Generate new tokens

It has become almost essential for API assessments involving JWT authentication.

---

## Hackvertor

Hackvertor provides rapid data transformation.

Examples include:

- Base64
- URL Encoding
- HTML Encoding
- Hexadecimal
- Hashing
- Compression

Rather than repeatedly switching to Decoder, many testers use Hackvertor directly inside requests.

---

## Autorize

Broken Access Control remains one of the most common web vulnerabilities.

Autorize automatically compares requests from different user accounts.

This allows testers to quickly identify authorization flaws without manually repeating every request.

---

## Turbo Intruder

Turbo Intruder is designed for high-performance HTTP request generation.

Unlike Burp's standard Intruder, it is capable of sending extremely large numbers of requests efficiently.

It is frequently used during:

- Race condition testing
- Large-scale fuzzing
- High-speed parameter discovery

---

## Param Miner

Param Miner searches for undocumented HTTP parameters.

Many applications contain hidden parameters that developers never intended users to discover.

Finding these parameters can reveal:

- Debug functionality
- Administrative features
- Hidden APIs
- Legacy behaviour

---

## Active Scan++

This extension improves Burp Professional's automated scanning by adding additional passive and active security checks.

It complements rather than replaces Burp's built-in scanner.

---

# Which Extensions Should Beginners Install?

New users often install dozens of extensions immediately.

This usually creates unnecessary complexity.

A better starting point is:

- Logger++
- JWT Editor
- Hackvertor
- Autorize
- Param Miner

Additional extensions can be introduced gradually as new testing scenarios arise.

---

# Key Takeaways

By now you should understand that Burp Suite is far more than an intercepting proxy.

Features such as Session Handling Rules, Macros, Match and Replace, the Cookie Jar, and Burp Collaborator allow testers to automate repetitive tasks and focus on analysing application behaviour rather than fighting the testing environment.

The Extender module and the official BApp Store transform Burp into an extensible platform capable of adapting to virtually any web security assessment. While Burp's default modules are sufficient for learning and many real-world engagements, mastering its advanced features and carefully selecting extensions can dramatically improve both efficiency and testing depth.

# Part 5 - Practical Workflow and Professional Methodology

Knowing how each Burp module works is only half the battle. The true value of Burp Suite comes from understanding **when**, **why**, and **in what order** each tool should be used.

Professional penetration testers rarely jump directly into exploiting vulnerabilities. Instead, they follow a structured methodology designed to maximize coverage while minimizing the risk of overlooking critical functionality.

Although every assessment differs, most manual web application penetration tests follow a workflow similar to the one presented in this chapter.

---

# The Typical Burp Workflow

```
Configure Burp

↓

Configure Browser

↓

Define Scope

↓

Browse Application

↓

Map Application

↓

Identify Interesting Requests

↓

Manual Testing

↓

Automation

↓

Validate Findings

↓

Document Evidence

↓

Write Report
```

Notice that exploitation represents only a small portion of the assessment.

Most of the work consists of understanding how the application behaves.

---

# Phase 1 - Initial Configuration

Before interacting with the target:

- Start Burp.
- Create a project.
- Verify Proxy Listener.
- Configure your browser.
- Install the Burp CA certificate (if using HTTPS).
- Configure Scope.
- Enable HTTP History.

This takes only a few minutes but prevents countless problems later.

---

# Phase 2 - Passive Reconnaissance

The first objective is **not** to attack the application.

Instead:

Browse.

Click everything.

Observe everything.

Map everything.

Professional testers usually spend a significant amount of time simply understanding the application.

Examples:

- Registration
- Login
- Logout
- Password Reset
- User Profile
- Settings
- File Uploads
- Search Functions
- Administration
- APIs

The goal is to understand how the application works before attempting to break it.

---

# Mapping the Application

While browsing, Burp automatically collects information.

Pay attention to:

- Directories
- Parameters
- API Endpoints
- Static Files
- JavaScript
- Cookies
- Authentication
- Session Tokens

The Site Map gradually becomes one of your most valuable assets.

Many vulnerabilities are discovered simply because an unusual endpoint appears during reconnaissance.

---

# Understanding Authentication

Authentication deserves careful attention.

Questions worth asking include:

- How does login work?
- Is MFA enabled?
- Are JWTs used?
- Are sessions cookie-based?
- Are tokens rotated?
- How long do sessions last?
- Can sessions be reused?

Do not attempt privilege escalation before understanding authentication.

---

# Identifying Interesting Requests

Not every request deserves attention.

A request for:

```
logo.png
```

is rarely interesting.

A request for:

```
POST /api/admin/updateUser
```

certainly is.

Good candidates include:

- POST requests
- PUT requests
- DELETE requests
- Authenticated API calls
- File uploads
- JSON payloads
- GraphQL queries
- Administrative actions

These requests usually become your primary testing targets.

---

# Sending Requests to Repeater

Whenever an interesting request appears:

```
Right Click

↓

Send to Repeater
```

Repeater becomes your workspace.

Rather than repeatedly interacting with the browser, all testing now occurs inside Repeater.

This dramatically increases efficiency.

---

# Manual Testing

Professional penetration testers strongly favor manual testing.

Why?

Because business logic cannot usually be automated.

Examples:

- Changing parameters
- Removing headers
- Editing cookies
- Altering roles
- Changing identifiers
- Modifying JSON
- Testing unusual values

Each modification teaches something about the application.

---

# Testing Input Validation

Nearly every user-controlled parameter deserves attention.

Examples include:

```
username=

email=

id=

page=

file=

token=

role=
```

Questions to ask:

- Can this value be modified?
- Is input validated?
- Is input sanitized?
- Is server-side validation present?
- Are unexpected characters accepted?

Poor input validation often leads to vulnerabilities.

---

# Authorization Testing

One of the most important phases.

Suppose User A requests:

```
GET /profile/15
```

Change:

```
15
```

↓

```
16
```

↓

```
17
```

↓

```
18
```

Does the application still return data?

If yes, an IDOR vulnerability may exist.

Authorization testing should never be overlooked.

---

# Cookie Analysis

Cookies frequently contain valuable information.

Inspect:

- Session IDs
- JWTs
- Preferences
- Tracking Values
- Authentication Tokens

Questions include:

- Can they be modified?
- Are they predictable?
- Are security flags present?
- Do they expire?

Cookie analysis often reveals authentication weaknesses.

---

# JWT Analysis

When JWTs are encountered:

Inspect:

- Header
- Payload
- Signature

Questions include:

- Which algorithm is used?
- Are sensitive claims exposed?
- Can claims be modified?
- Is signature validation enforced?

JWT Editor becomes extremely useful here.

---

# File Upload Testing

Whenever file uploads exist, verify:

- Allowed extensions
- MIME validation
- Content validation
- File size restrictions
- Double extensions
- Executable uploads

Upload functionality is frequently abused.

---

# API Testing

Modern applications often expose REST APIs.

Inspect:

- JSON requests
- Authentication
- Rate limits
- Error handling
- Hidden endpoints

Many web applications are now API-first.

Ignoring APIs leaves large portions of the attack surface untested.

---

# Automation

Only after understanding the application should automation be introduced.

Examples include:

Intruder

↓

Parameter Fuzzing

Param Miner

↓

Hidden Parameters

Autorize

↓

Broken Access Control

Automation should support manual testing.

It should never replace it.

---

# Validating Findings

Never report a vulnerability immediately.

Instead:

Repeat it.

Verify it.

Understand it.

Professional testers attempt to reproduce every issue multiple times before considering it confirmed.

False positives waste everyone's time.

---

# Recording Evidence

As vulnerabilities are confirmed:

Save:

- Requests
- Responses
- Screenshots
- Notes
- Payloads
- Impact

Do not rely on memory.

Several hours later, seemingly obvious details become surprisingly easy to forget.

---

# Writing Notes During Testing

Experienced testers constantly document their work.

Useful notes include:

```
Admin endpoint discovered.

Requires JWT.

Returns 403.

Parameter "role" appears trusted.

Potential IDOR.
```

These notes eventually become the foundation of the final report.

---

# Common Beginner Mistakes

Many newcomers:

- Attack immediately.
- Ignore Scope.
- Skip reconnaissance.
- Forget to save requests.
- Never organize Repeater tabs.
- Test randomly.
- Ignore HTTP History.
- Install dozens of unnecessary extensions.

Burp rewards organization.

A disciplined workflow almost always outperforms a chaotic one.

---

# Professional Best Practices

Professional testers commonly:

- Define Scope immediately.
- Browse the application completely before testing.
- Keep Repeater organized.
- Name important tabs.
- Filter HTTP History.
- Save evidence continuously.
- Validate every finding.
- Document everything.

Good organization often distinguishes experienced testers from beginners.

---

# Ethical Considerations

Burp Suite is an extremely powerful tool.

With only a few clicks it becomes possible to:

- Modify requests.
- Replay sensitive operations.
- Bypass client-side controls.
- Test authentication.
- Discover hidden functionality.

These capabilities should only be used against systems for which explicit authorization has been granted.

Unauthorized testing may violate laws, contractual agreements, or acceptable use policies.

Always ensure you have permission before conducting any security assessment.

---

# Key Takeaways

A successful Burp Suite workflow is built on understanding before exploitation. Professional testers invest significant time mapping the application, learning its authentication mechanisms, identifying high-value requests, and documenting their observations before attempting to exploit vulnerabilities.

Burp Suite is most effective when its modules are used together as part of a structured methodology rather than in isolation. Reconnaissance, manual testing, selective automation, validation, and careful documentation form the foundation of high-quality web application security assessments. Mastering this workflow is considerably more valuable than memorizing individual features, as it reflects how Burp Suite is used during real-world penetration tests.

# Part 5 - Practical Workflow and Professional Methodology

Knowing how each Burp module works is only half the battle. The true value of Burp Suite comes from understanding **when**, **why**, and **in what order** each tool should be used.

Professional penetration testers rarely jump directly into exploiting vulnerabilities. Instead, they follow a structured methodology designed to maximize coverage while minimizing the risk of overlooking critical functionality.

Although every assessment differs, most manual web application penetration tests follow a workflow similar to the one presented in this chapter.

---

# The Typical Burp Workflow

```
Configure Burp

↓

Configure Browser

↓

Define Scope

↓

Browse Application

↓

Map Application

↓

Identify Interesting Requests

↓

Manual Testing

↓

Automation

↓

Validate Findings

↓

Document Evidence

↓

Write Report
```

Notice that exploitation represents only a small portion of the assessment.

Most of the work consists of understanding how the application behaves.

---

# Phase 1 - Initial Configuration

Before interacting with the target:

- Start Burp.
- Create a project.
- Verify Proxy Listener.
- Configure your browser.
- Install the Burp CA certificate (if using HTTPS).
- Configure Scope.
- Enable HTTP History.

This takes only a few minutes but prevents countless problems later.

---

# Phase 2 - Passive Reconnaissance

The first objective is **not** to attack the application.

Instead:

Browse.

Click everything.

Observe everything.

Map everything.

Professional testers usually spend a significant amount of time simply understanding the application.

Examples:

- Registration
- Login
- Logout
- Password Reset
- User Profile
- Settings
- File Uploads
- Search Functions
- Administration
- APIs

The goal is to understand how the application works before attempting to break it.

---

# Mapping the Application

While browsing, Burp automatically collects information.

Pay attention to:

- Directories
- Parameters
- API Endpoints
- Static Files
- JavaScript
- Cookies
- Authentication
- Session Tokens

The Site Map gradually becomes one of your most valuable assets.

Many vulnerabilities are discovered simply because an unusual endpoint appears during reconnaissance.

---

# Understanding Authentication

Authentication deserves careful attention.

Questions worth asking include:

- How does login work?
- Is MFA enabled?
- Are JWTs used?
- Are sessions cookie-based?
- Are tokens rotated?
- How long do sessions last?
- Can sessions be reused?

Do not attempt privilege escalation before understanding authentication.

---

# Identifying Interesting Requests

Not every request deserves attention.

A request for:

```
logo.png
```

is rarely interesting.

A request for:

```
POST /api/admin/updateUser
```

certainly is.

Good candidates include:

- POST requests
- PUT requests
- DELETE requests
- Authenticated API calls
- File uploads
- JSON payloads
- GraphQL queries
- Administrative actions

These requests usually become your primary testing targets.

---

# Sending Requests to Repeater

Whenever an interesting request appears:

```
Right Click

↓

Send to Repeater
```

Repeater becomes your workspace.

Rather than repeatedly interacting with the browser, all testing now occurs inside Repeater.

This dramatically increases efficiency.

---

# Manual Testing

Professional penetration testers strongly favor manual testing.

Why?

Because business logic cannot usually be automated.

Examples:

- Changing parameters
- Removing headers
- Editing cookies
- Altering roles
- Changing identifiers
- Modifying JSON
- Testing unusual values

Each modification teaches something about the application.

---

# Testing Input Validation

Nearly every user-controlled parameter deserves attention.

Examples include:

```
username=

email=

id=

page=

file=

token=

role=
```

Questions to ask:

- Can this value be modified?
- Is input validated?
- Is input sanitized?
- Is server-side validation present?
- Are unexpected characters accepted?

Poor input validation often leads to vulnerabilities.

---

# Authorization Testing

One of the most important phases.

Suppose User A requests:

```
GET /profile/15
```

Change:

```
15
```

↓

```
16
```

↓

```
17
```

↓

```
18
```

Does the application still return data?

If yes, an IDOR vulnerability may exist.

Authorization testing should never be overlooked.

---

# Cookie Analysis

Cookies frequently contain valuable information.

Inspect:

- Session IDs
- JWTs
- Preferences
- Tracking Values
- Authentication Tokens

Questions include:

- Can they be modified?
- Are they predictable?
- Are security flags present?
- Do they expire?

Cookie analysis often reveals authentication weaknesses.

---

# JWT Analysis

When JWTs are encountered:

Inspect:

- Header
- Payload
- Signature

Questions include:

- Which algorithm is used?
- Are sensitive claims exposed?
- Can claims be modified?
- Is signature validation enforced?

JWT Editor becomes extremely useful here.

---

# File Upload Testing

Whenever file uploads exist, verify:

- Allowed extensions
- MIME validation
- Content validation
- File size restrictions
- Double extensions
- Executable uploads

Upload functionality is frequently abused.

---

# API Testing

Modern applications often expose REST APIs.

Inspect:

- JSON requests
- Authentication
- Rate limits
- Error handling
- Hidden endpoints

Many web applications are now API-first.

Ignoring APIs leaves large portions of the attack surface untested.

---

# Automation

Only after understanding the application should automation be introduced.

Examples include:

Intruder

↓

Parameter Fuzzing

Param Miner

↓

Hidden Parameters

Autorize

↓

Broken Access Control

Automation should support manual testing.

It should never replace it.

---

# Validating Findings

Never report a vulnerability immediately.

Instead:

Repeat it.

Verify it.

Understand it.

Professional testers attempt to reproduce every issue multiple times before considering it confirmed.

False positives waste everyone's time.

---

# Recording Evidence

As vulnerabilities are confirmed:

Save:

- Requests
- Responses
- Screenshots
- Notes
- Payloads
- Impact

Do not rely on memory.

Several hours later, seemingly obvious details become surprisingly easy to forget.

---

# Writing Notes During Testing

Experienced testers constantly document their work.

Useful notes include:

```
Admin endpoint discovered.

Requires JWT.

Returns 403.

Parameter "role" appears trusted.

Potential IDOR.
```

These notes eventually become the foundation of the final report.

---

# Common Beginner Mistakes

Many newcomers:

- Attack immediately.
- Ignore Scope.
- Skip reconnaissance.
- Forget to save requests.
- Never organize Repeater tabs.
- Test randomly.
- Ignore HTTP History.
- Install dozens of unnecessary extensions.

Burp rewards organization.

A disciplined workflow almost always outperforms a chaotic one.

---

# Professional Best Practices

Professional testers commonly:

- Define Scope immediately.
- Browse the application completely before testing.
- Keep Repeater organized.
- Name important tabs.
- Filter HTTP History.
- Save evidence continuously.
- Validate every finding.
- Document everything.

Good organization often distinguishes experienced testers from beginners.

---

# Ethical Considerations

Burp Suite is an extremely powerful tool.

With only a few clicks it becomes possible to:

- Modify requests.
- Replay sensitive operations.
- Bypass client-side controls.
- Test authentication.
- Discover hidden functionality.

These capabilities should only be used against systems for which explicit authorization has been granted.

Unauthorized testing may violate laws, contractual agreements, or acceptable use policies.

Always ensure you have permission before conducting any security assessment.

---

# Key Takeaways

A successful Burp Suite workflow is built on understanding before exploitation. Professional testers invest significant time mapping the application, learning its authentication mechanisms, identifying high-value requests, and documenting their observations before attempting to exploit vulnerabilities.

Burp Suite is most effective when its modules are used together as part of a structured methodology rather than in isolation. Reconnaissance, manual testing, selective automation, validation, and careful documentation form the foundation of high-quality web application security assessments. Mastering this workflow is considerably more valuable than memorizing individual features, as it reflects how Burp Suite is used during real-world penetration tests.

# Part 6 - Burp Suite Reference, FoxyProxy Setup and Additional Resources

By this point, you should understand Burp Suite's architecture, its core modules, advanced features, and the methodology followed during professional web application security assessments.

This final chapter serves as a practical reference that you can revisit whenever you need to configure a new environment, remember a shortcut, install useful extensions, or continue your learning through official resources.

---

# Burp Suite Cheat Sheet

## Typical Workflow

```
Configure Browser

↓

Configure Burp

↓

Install CA Certificate

↓

Define Scope

↓

Browse Application

↓

Inspect HTTP History

↓

Send Interesting Requests to Repeater

↓

Modify Requests

↓

Validate Responses

↓

Document Findings
```

---

## Most Common Right-Click Actions

During an assessment, these options are used constantly.

```
Send to Repeater

Send to Intruder

Send to Decoder

Send to Comparer

Send to Organizer
```

Learning these shortcuts significantly improves workflow efficiency.

---

## Core Modules

| Module | Purpose |
|----------|---------|
| Target | Maps the application |
| Proxy | Intercepts traffic |
| HTTP History | Records communication |
| Repeater | Manual testing |
| Intruder | Automated requests |
| Decoder | Encoding and decoding |
| Comparer | Compare requests/responses |
| Logger | Traffic logging |
| Organizer | Save important requests |
| Extender | Install extensions |

---

# Useful Keyboard Shortcuts

The exact shortcuts may vary slightly between operating systems and Burp versions.

Some of the most frequently used include:

| Shortcut | Action |
|-----------|--------|
| Ctrl + R | Send to Repeater |
| Ctrl + I | Send to Intruder |
| Ctrl + Shift + D | Send to Decoder |
| Ctrl + Shift + C | Send to Comparer |
| Ctrl + F | Search |
| Ctrl + Tab | Switch Tabs |
| Ctrl + W | Close Current Tab |

Always verify shortcuts in your installed Burp version, as PortSwigger occasionally updates them.

---

# Recommended Beginner Extensions

If you are new to Burp Suite, avoid installing dozens of extensions immediately.

Start with:

- Logger++
- JWT Editor
- Hackvertor
- Autorize
- Param Miner

These five extensions provide excellent functionality without overwhelming the interface.

As your experience grows, install additional extensions only when you understand the problem they solve.

---

# Installing Extensions

Installing extensions is straightforward.

1. Open **Extensions**.
2. Open the **BApp Store**.
3. Search for the desired extension.
4. Select it.
5. Click **Install**.
6. Wait for Burp to download and load the extension.

After installation, many extensions automatically create a new tab within Burp.

Some also add new context menu options.

---

# The BApp Store

The **BApp Store** is PortSwigger's official repository of Burp Suite extensions.

Unlike downloading scripts from random GitHub repositories, the BApp Store provides a curated collection of extensions that integrate directly into Burp.

The repository contains hundreds of community-developed tools covering topics such as:

- Authentication
- Authorization
- JWTs
- GraphQL
- APIs
- Active Scanning
- Logging
- Payload Generation
- Parameter Discovery
- Encoding
- Cloud Security
- OAuth
- WebSockets

Whenever possible, prefer extensions from the BApp Store over unofficial sources.

---

# Other Extension Sources

Although the BApp Store should be your first choice, some extensions are distributed elsewhere.

Common locations include:

- GitHub
- Individual researcher repositories
- Security conference releases
- PortSwigger research blog

Before installing third-party extensions:

- Review the source code when possible.
- Verify the project's reputation.
- Check whether it is actively maintained.
- Avoid abandoned projects.

Remember that Burp extensions execute inside Burp itself.

Treat them with the same level of trust you would give any software running on your workstation.

---

# Updating Burp Suite

Burp receives frequent updates.

These updates commonly include:

- New features
- Security fixes
- Performance improvements
- UI improvements
- New BApp compatibility
- Bug fixes

Keeping Burp updated is highly recommended.

---

# Updating Extensions

Extensions also evolve.

Developers frequently release:

- Bug fixes
- Compatibility updates
- New features
- API changes

Regularly check for extension updates through the BApp Store.

---

# Installing FoxyProxy (Firefox)

Although Burp Browser is excellent, many professionals prefer using Firefox together with **FoxyProxy**.

FoxyProxy allows proxy settings to be enabled or disabled with a single click instead of manually modifying Firefox's network configuration.

---

## Step 1 - Install FoxyProxy

Open Firefox.

Visit the official Firefox Add-ons website.

Search for:

```
FoxyProxy Standard
```

Install the extension.

After installation, its icon should appear in Firefox's toolbar.

---

## Step 2 - Create a New Proxy

Open FoxyProxy.

Create a new proxy profile.

Configure:

```
Type:
HTTP

Host:
127.0.0.1

Port:
8080
```

These values match Burp Suite's default Proxy Listener.

If you changed Burp's listener configuration, use the corresponding host and port.

Save the configuration.

---

## Step 3 - Enable the Proxy

Click the FoxyProxy icon.

Select the Burp proxy profile.

Firefox will now send all web traffic through Burp Suite.

---

## Step 4 - Install Burp's CA Certificate

If HTTPS traffic is intercepted, Firefox must trust Burp's Certificate Authority.

Open Burp Suite.

Navigate to:

```
Proxy

↓

Options

↓

Import / Export CA Certificate
```

Export the Burp CA certificate.

In Firefox:

```
Settings

↓

Privacy & Security

↓

Certificates

↓

View Certificates

↓

Authorities

↓

Import
```

Import Burp's CA certificate.

Enable trust for websites.

Restart Firefox if necessary.

---

## Step 5 - Verify the Configuration

Open a website while Burp is running.

If everything is configured correctly:

- Burp receives requests.
- Firefox loads the page normally.
- HTTPS pages no longer display certificate warnings.
- Requests appear inside HTTP History.

If the browser cannot load websites:

- Verify FoxyProxy is enabled.
- Verify Burp is running.
- Confirm the Proxy Listener is active.
- Confirm the certificate has been imported correctly.

Most connection problems originate from one of these four issues.

---

# Common Beginner Problems

### Burp receives no traffic

Possible causes:

- FoxyProxy disabled.
- Wrong port.
- Wrong host.
- Proxy Listener stopped.

---

### Browser freezes

Usually:

Intercept is enabled.

The request is waiting inside Burp.

Simply click **Forward**.

---

### HTTPS Certificate Warning

Almost always caused by:

- Missing Burp CA certificate.
- Certificate not trusted.
- Incorrect certificate imported.

---

### Requests Never Reach the Server

Check:

- Intercept.
- Proxy Listener.
- Browser proxy configuration.

---

# Additional Learning Resources

The following resources are strongly recommended for anyone wishing to master Burp Suite.

## PortSwigger Documentation

The official documentation is the most comprehensive reference available.

https://portswigger.net/burp/documentation

---

## PortSwigger Web Security Academy

Arguably the best free web application security training platform available.

https://portswigger.net/web-security

---

## PortSwigger BApp Store

Official extension repository.

https://portswigger.net/bappstore

---

## PortSwigger YouTube Channel

Contains demonstrations, release overviews, and educational material presented by the Burp Suite developers themselves.

https://www.youtube.com/@PortSwigger

---

# Final Notes

Burp Suite is one of the most powerful and comprehensive tools available for web application security testing. It is used daily by penetration testers, bug bounty hunters, application security engineers, and security researchers around the world. While learning its interface may seem intimidating at first, mastering a small number of core modules will allow you to perform the majority of manual web security assessments effectively.

It is important to remember that this document is intended to serve as a practical foundation rather than an exhaustive reference. Burp Suite is an actively developed platform with frequent updates, new modules, and an ever-growing ecosystem of extensions. As your experience grows, you will almost certainly encounter features, workflows, and plugins that are beyond the scope of this guide.

For that reason, regularly consulting the official PortSwigger documentation should become part of your learning process. Many advanced topics, edge cases, and newly released capabilities are documented there long before they appear in third-party tutorials or courses.

Finally, a personal note from the author: compiling this document proved to be considerably more challenging than expected. Even with the assistance of artificial intelligence to review wording, improve readability, and help organize the material, condensing such a vast platform into a single coherent reference required significant research and careful editing. Hopefully, this guide saves you many hours of searching and provides a solid starting point for your journey into web application security.