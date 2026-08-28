#web-security #appsec #owasp #vulnerability

# OWASP Top 10

The **OWASP Top 10** is an application security awareness framework maintained by the **Open Worldwide Application Security Project (OWASP)**. It identifies and describes the most critical categories of security risk affecting web applications and APIs, providing developers, security professionals, and organizations with a common vocabulary for discussing application security.

The current edition is **OWASP Top 10:2025**. It should be treated as an awareness and risk-prioritization resource rather than a complete application security standard. OWASP explicitly recommends more comprehensive standards such as the **OWASP Application Security Verification Standard (ASVS)** when detailed, testable security requirements are required.

## OWASP Top 10:2025

The current categories are:

1. **A01:2025 — Broken Access Control**
2. **A02:2025 — Security Misconfiguration**
3. **A03:2025 — Software Supply Chain Failures**
4. **A04:2025 — Cryptographic Failures**
5. **A05:2025 — Injection**
6. **A06:2025 — Insecure Design**
7. **A07:2025 — Authentication Failures**
8. **A08:2025 — Software or Data Integrity Failures**
9. **A09:2025 — Security Logging & Alerting Failures**
10. **A10:2025 — Mishandling of Exceptional Conditions**

[OWASP Top 10:2025](https://owasp.org/Top10/?utm_source=chatgpt.com)

The 2025 edition reflects a stronger emphasis on root causes and modern application ecosystems. **A03: Software Supply Chain Failures** expands the scope previously covered by vulnerable and outdated components to include weaknesses across dependencies, build systems, and software distribution. **A10: Mishandling of Exceptional Conditions** is a new category addressing insecure handling of errors and unexpected application states. **SSRF**, previously a standalone category in 2021, has been incorporated into **A01: Broken Access Control**.

## A01 — Broken Access Control

Broken Access Control occurs when an application fails to correctly enforce what an authenticated or unauthenticated user is permitted to access or perform.

Access control must be enforced on the server for every security-sensitive operation. Client-side restrictions, hidden interface elements, URL obscurity, or user-controlled parameters cannot be considered authorization mechanisms.

Common manifestations include:

* Horizontal privilege escalation.
* Vertical privilege escalation.
* Insecure Direct Object References (IDOR).
* Unauthorized access to administrative functionality.
* Modification of resources belonging to other users.
* Missing or inconsistent authorization checks.
* Server-Side Request Forgery (SSRF) within the 2025 category structure.

The fundamental security principle is **deny by default**: access should only be granted when the application can establish that the requesting identity has the required authorization.

Related concepts: [[Sessions]], [[Cookies]], [[Web-Architecture]].

## A02 — Security Misconfiguration

Security Misconfiguration occurs when an application, server, cloud environment, framework, or supporting component is deployed with insecure settings.

Examples include unnecessary services, exposed administrative interfaces, default credentials, excessive permissions, verbose error messages, insecure headers, outdated components, and improperly configured cloud resources.

Security configuration is not a one-time task. Changes in infrastructure, dependencies, deployment systems, and application functionality can introduce new exposure. Secure configuration therefore requires hardened defaults, least privilege, removal of unnecessary functionality, controlled error handling, and continuous configuration review.

## A03 — Software Supply Chain Failures

Software Supply Chain Failures occur when weaknesses or compromises within software dependencies, development systems, build pipelines, distribution mechanisms, or third-party components affect the security of an application.

Modern applications rarely consist entirely of first-party code. They depend on external libraries, packages, frameworks, container images, build tools, services, and other software components. A compromise anywhere in this chain can propagate into applications that consume the affected component.

Important controls include dependency inventory, provenance verification, dependency updates, integrity verification, secure CI/CD infrastructure, access control, artifact signing, and monitoring of third-party components.

The 2025 edition expanded this category beyond simply using vulnerable or outdated libraries to address broader supply-chain compromise.

## A04 — Cryptographic Failures

Cryptographic Failures occur when sensitive information is insufficiently protected through encryption or when cryptographic mechanisms are implemented incorrectly.

The problem can involve failing to encrypt sensitive data, using obsolete algorithms, poor key management, hard-coded secrets, inadequate randomness, incorrect certificate validation, or inappropriate cryptographic configurations.

Encryption alone is not sufficient. Secure cryptography depends on appropriate algorithms, secure key generation, protected key storage, correct protocol configuration, controlled access to keys, and appropriate key rotation.

Related concepts: [[Cryptography]], [[HTTPS]], [[Data-Encoding]].

## A05 — Injection

Injection occurs when untrusted input is interpreted as part of a command, query, or executable language rather than being treated strictly as data.

Important examples include:

* SQL Injection.
* Command Injection.
* Cross-Site Scripting (XSS).
* LDAP Injection.
* Other interpreter-based injection vulnerabilities.

The fundamental security problem is the failure to maintain a reliable separation between **data and instructions**.

Defensive techniques include parameterized queries, context-aware output encoding, strict input validation, safe APIs, and avoiding unnecessary interpreters.

Related concepts: [[SQL]], [[HTTP]], [[JavaScript]].

## A06 — Insecure Design

Insecure Design describes weaknesses introduced at the architectural or business-logic level rather than merely through implementation errors.

An application can be free of obvious coding vulnerabilities and still be insecure because its workflows, authorization model, recovery mechanisms, or business rules were designed without adequate threat modelling.

Secure design requires explicit security requirements, abuse-case analysis, threat modelling, least privilege, appropriate trust boundaries, and security controls designed around realistic attacker behaviour.

This category is important because some security problems cannot be fixed simply by changing a line of code. The underlying architecture or business process may need to change.

## A07 — Authentication Failures

Authentication Failures occur when an application incorrectly establishes or maintains the identity of a user or service.

Examples include weak authentication mechanisms, username enumeration, weak passwords, unrestricted authentication attempts, insecure session handling, and flawed account recovery or authentication workflows.

Authentication must establish identity reliably before authorization decisions are made. Session management must also preserve that identity securely after authentication.

This creates a direct relationship between authentication and access control:

**Authentication answers "Who are you?"**

**Authorization answers "What are you allowed to do?"**

Related concepts: [[Sessions]], [[Cookies]], [[Active-Directory]].

## A08 — Software or Data Integrity Failures

Software or Data Integrity Failures occur when applications trust software, data, updates, serialized objects, dependencies, or other external components without adequately verifying their integrity or authenticity.

Examples include insecure deserialization, untrusted software updates, compromised dependencies, and application processes that accept modified data without sufficient verification.

Digital signatures, integrity verification, trusted update mechanisms, controlled dependency sources, and secure software delivery pipelines can reduce this risk.

This category is closely related to [[Cryptography]] and [[Software Supply Chain]] concepts.

## A09 — Security Logging & Alerting Failures

Security Logging & Alerting Failures occur when applications do not generate, preserve, monitor, or alert on sufficient security-relevant events.

Useful events can include authentication attempts, authorization failures, account changes, privilege changes, password or MFA modifications, administrative operations, and other actions that could indicate abuse.

Logging without analysis provides limited defensive value. Security-relevant events need appropriate collection, retention, correlation, monitoring, and alerting so that suspicious activity can be identified and investigated.

This category connects directly with [[SIEM]], [[Defensive-Security]], and incident response.

## A10 — Mishandling of Exceptional Conditions

Mishandling of Exceptional Conditions concerns situations where applications fail to safely handle errors, unexpected states, resource exhaustion, invalid input, or abnormal execution conditions.

An application should not assume that operations will always succeed. Failure conditions must be considered part of the normal security model.

Poor exception handling can result in information disclosure, inconsistent authorization states, bypasses, denial of service, corrupted application state, or unexpected execution paths.

Secure handling requires controlled error states, appropriate resource limits, safe failure behaviour, and avoiding the exposure of sensitive implementation details.

## Using the OWASP Top 10

The OWASP Top 10 is most useful as an **awareness and prioritization framework**. It provides a high-level taxonomy that helps developers and security professionals recognize important classes of application security problems.

It should not be interpreted as a checklist proving that an application is secure. OWASP itself recommends the **ASVS** when an organization requires comprehensive and verifiable application security requirements.

A practical application-security workflow can therefore use the Top 10 to establish awareness and identify major risk categories, while using more detailed standards, threat modelling, secure coding practices, testing methodologies, and verification requirements for actual security assurance.

## Related Notes

* [[Web-Architecture]]
* [[HTTP]]
* [[HTTPS]]
* [[Sessions]]
* [[Cookies]]
* [[SQL]]
* [[JavaScript]]
* [[Cryptography]]
* [[SIEM]]
* [[Defensive-Security]]
* [[Offensive-Security]]
