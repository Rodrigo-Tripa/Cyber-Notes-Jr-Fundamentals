# Threat Modeling

> A security system cannot be evaluated without first defining what it is supposed to protect, from whom, and under which conditions.

## 1. What Is Threat Modeling?

Threat modeling is the process of systematically identifying what must be protected, who may attempt to compromise it, what capabilities the adversary possesses, and which conditions could lead to failure.

In anonymity engineering, this is particularly important because the statement _"I want to be anonymous"_ is incomplete. Anonymity is always relative to an observer and its capabilities.

A system that hides a user's IP address from a website may provide useful protection against ordinary web tracking. The same system may provide substantially weaker protection against an Internet Service Provider capable of observing the user's network connections. An adversary capable of observing multiple points of the Internet may have capabilities that are fundamentally different again.

The purpose of threat modeling is therefore to transform a vague security objective into a concrete model:

`Asset → Adversary → Capability → Attack Surface → Security Objective → Failure Condition`

A good threat model does not attempt to defend against every imaginable attacker. It defines realistic assumptions and establishes what the system is, and is not, designed to protect.

---

## 2. Assets and Security Objectives

The first step is identifying what actually needs protection.

In an anonymity context, an asset is not necessarily a file, password or server. It may be the relationship between an action and an identity.

Examples include:

- Real-world identity
    
- Physical location
    
- IP address
    
- Online pseudonym
    
- Relationship between multiple pseudonyms
    
- Browsing activity
    
- Communication metadata
    
- Physical device
    
- Personal documents
    
- Behavioural patterns
    
- Association between activities
    

The security objective must then describe what relationship the system needs to prevent.

For example:

`Activity A ↔ Real Identity`

may need to remain unobservable.

But perhaps:

`Activity A ↔ Activity B`

must also remain unlinkable, even though neither activity individually reveals the real identity.

This distinction matters because protecting one relationship does not automatically protect another.

A system might successfully hide the user's physical location while still allowing a service to identify the user through an account. Similarly, it might hide the identity while allowing an observer to determine that two anonymous activities originated from the same person.

Threat modeling therefore starts with a precise question:

> **What information or relationship must remain hidden from which observer?**

---

## 3. Adversary Models

Different adversaries have different visibility and capabilities.

A **local network observer** may observe traffic between a device and its network infrastructure. Depending on its position, this could include connection destinations, timing, volume and protocol information.

An **Internet Service Provider** can typically observe that a customer is communicating with particular network infrastructure, even when the contents of those communications are encrypted.

A **website or online service** can observe information arriving at its own infrastructure. Depending on the application, this may include IP information, browser characteristics, cookies, account identifiers, behavioural patterns and application-level metadata.

A **platform or tracking ecosystem** may have visibility across multiple websites and applications, allowing seemingly independent activities to be correlated.

A **local attacker** has a different advantage: access to the endpoint itself. Depending on the circumstances, they may inspect files, logs, browser state, cached data, memory, storage or configuration.

A **powerful network adversary** may observe multiple locations within the network and attempt to correlate traffic entering and leaving an anonymity system.

These adversaries should not be treated as interchangeable. A technique that works against one may provide little protection against another.

---

## 4. Adversary Capability

Threat models become useful when adversary capabilities are explicitly defined.

Relevant capabilities include:

**Observation:** the ability to monitor traffic, systems, accounts or public information.

**Collection:** the ability to retain observations over time and construct historical datasets.

**Correlation:** the ability to compare observations from different sources and determine whether they are related.

**Control:** the ability to operate or compromise infrastructure, such as websites, servers or network nodes.

**Identification:** access to external information that maps an observed activity to a real identity.

**Endpoint access:** physical or logical access to the user's device.

**Global visibility:** the ability to observe multiple points of a communication path simultaneously.

The distinction between observation and correlation is particularly important.

An observer may not directly see a user's identity. However, if the observer can compare timing, packet volumes or behavioural characteristics between two locations, it may infer that two apparently separate observations belong to the same communication.

This is one of the fundamental problems faced by anonymity networks.

---

## 5. Attack Surface

The attack surface consists of all components through which identifying information can potentially escape.

For an anonymous computing environment, this can be represented as:

`User`  
↓  
`Hardware`  
↓  
`Operating System`  
↓  
`Applications`  
↓  
`Browser`  
↓  
`Network`  
↓  
`Anonymity System`  
↓  
`Destination`

Every layer can introduce a different class of vulnerability.

The user can reveal identity through behaviour or account reuse.

The operating system can expose persistent identifiers or local traces.

Applications can generate telemetry or network connections outside the intended anonymity path.

The browser can expose fingerprints, cookies, storage and other identifying characteristics.

The network can expose traffic patterns, timing and connection metadata.

The anonymity system can have architectural limitations or vulnerabilities.

The destination can correlate the anonymous activity with information already associated with an identity.

This means that anonymity cannot be evaluated by examining only one layer.

---

## 6. Attack Classes

Several attack classes are particularly relevant to anonymity.

**Direct identification** occurs when an activity explicitly reveals an identity. Logging into a personally identifying account is the simplest example.

**Linkability attacks** attempt to determine whether two activities belong to the same entity. Persistent identifiers, fingerprints and behavioural characteristics can contribute to this.

**Fingerprinting attacks** attempt to distinguish a particular device, browser or environment based on observable characteristics.

**Metadata analysis** extracts information from timestamps, sizes, frequencies, locations and other information surrounding communication.

**Traffic correlation** compares observations from different points in a network. If sufficiently distinctive patterns appear at both ends, an adversary may infer that they belong to the same communication.

**Intersection attacks** observe activity over time and progressively eliminate possible identities based on who could have been active during particular periods.

**Endpoint compromise** bypasses many network-level protections entirely by obtaining information directly from the user's device.

These attacks do not necessarily require breaking encryption. In many cases, the attacker is exploiting information that encryption was never designed to hide.

---

## 7. Security Boundaries and Assumptions

Every threat model contains assumptions.

For example, an anonymity system may assume:

- The endpoint has not been compromised.
    
- The user does not reveal their identity voluntarily.
    
- The software behaves as expected.
    
- The anonymity network contains a sufficiently large user population.
    
- The adversary cannot observe every relevant network link.
    
- The user maintains separation between identities.
    
- The destination does not possess additional identifying information.
    

These assumptions are part of the security model.

If one of them becomes false, the security guarantees may change substantially.

This is why security claims should always be conditional.

Instead of saying:

> "This system makes me anonymous."

A technically meaningful statement would be:

> "This system reduces the ability of this class of observer to associate this activity with my identity, assuming the endpoint is uncompromised and identities are not reused."

The second statement communicates an actual security property and its boundaries.

---

## 8. Threat Modeling as a Continuous Process

A threat model should not be considered a document that is written once and forgotten.

The system changes. Software changes. Network architectures change. New tracking techniques appear. New vulnerabilities are discovered. The user's behaviour changes. An adversary may also acquire new capabilities.

Threat modeling should therefore be iterative:

`Model → Implement → Test → Observe → Reassess → Improve`

Testing is particularly important for anonymity because theoretical protection can differ from practical behaviour.

For example, a system may theoretically route traffic through an anonymity network while a misconfigured application creates a direct connection. A browser may expose characteristics that allow it to be distinguished from the anonymity population. A document may contain metadata that identifies its origin. An account may connect an otherwise anonymous activity to a known identity.

The purpose of testing is therefore not merely to verify that a tool works. It is to determine whether the **entire system satisfies the intended security properties**.

---

## Core Principle

> **There is no meaningful concept of "anonymous" without a defined adversary, observable information, and security objective.**

A strong anonymity architecture begins by defining the relationship that must remain hidden, identifying who might attempt to establish that relationship, determining what information they can observe, and understanding which assumptions the system depends upon.

Only after these questions have been answered does it make sense to select technologies such as Tor, Tails, Whonix, browser anti-fingerprinting mechanisms or compartmentalized environments.

Threat modeling is therefore not an accessory to anonymity engineering. It is the foundation on which the rest of the architecture is built.