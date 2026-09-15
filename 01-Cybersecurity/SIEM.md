#defensive-security #siem #soc #logging #monitoring #incident-response

# SIEM

**SIEM (Security Information and Event Management)** is a security technology used to collect, centralize, normalize, correlate, search, and analyze security-relevant data from multiple sources.

NIST describes SIEM software as providing centralized logging capabilities for different log types and describes a SIEM tool as an application capable of gathering security data from information-system components and presenting that data as actionable information through a single interface.

The primary purpose of a SIEM is not simply to store logs. Its value comes from transforming distributed events into information that can support **detection, investigation, monitoring, and response**.

## Why SIEM Exists

Modern environments generate enormous quantities of security-relevant events.

A single organization may have logs originating from:

- Windows and Linux systems.
- Firewalls.
- IDS/IPS sensors.
- Web servers.
- Databases.
- Authentication systems.
- Cloud infrastructure.
- Endpoint security platforms.
- Applications.
- Network devices.
- Identity providers.

Analysing these sources independently makes it difficult to reconstruct what happened during an attack.

A SIEM provides a centralized location where events can be collected and correlated, allowing analysts to reason about activity across the environment rather than treating every log source as an isolated system.

## Core SIEM Functions

### Log Collection

The SIEM receives security-relevant data from different systems and technologies.

Depending on the environment, this may involve agents, APIs, network protocols, cloud integrations, collectors, or direct log forwarding.

The objective is to bring relevant telemetry into a common analytical environment.

### Normalization

Different systems represent similar events using different formats.

For example, an authentication event from Windows, Linux, a cloud identity provider, and a web application may contain equivalent concepts but use different field names and structures.

Normalization maps these events into a more consistent representation, making cross-source analysis possible.

### Event Correlation

Correlation is one of the most important SIEM capabilities.

A single event may appear harmless when viewed independently. A sequence of related events can reveal an attack.

For example:

```text
Failed login attempts
        ↓
Successful authentication
        ↓
Privilege change
        ↓
Suspicious process execution
        ↓
Outbound network connection
````

The SIEM can correlate these events and provide analysts with a higher-level representation of potentially malicious activity.

NIST's Cybersecurity Framework implementation guidance specifically identifies SIEM as a mechanism for aggregating and correlating information from multiple sources during continuous monitoring.

### Detection and Alerting

SIEM platforms can generate alerts when events satisfy predefined detection logic.

Detection logic can be based on:

* Event patterns.
* Thresholds.
* Sequences.
* Statistical anomalies.
* Known indicators of compromise.
* Authentication behaviour.
* Network activity.
* Threat intelligence.
* Correlations across multiple systems.

An alert should provide enough context for an analyst to determine whether the observed behaviour represents a genuine security issue.

### Search and Investigation

Analysts need to search historical events to investigate suspicious activity.

A SIEM allows analysts to query collected data using fields such as:

* Source IP.
* Destination IP.
* Username.
* Hostname.
* Timestamp.
* Process.
* Event type.
* Authentication result.
* File hash.
* Domain.
* URL.

This makes it possible to investigate activity across multiple systems without manually accessing each log source.

## SIEM Data Sources

The quality of a SIEM depends heavily on the quality and coverage of its telemetry.

Important sources can include:

**Endpoint telemetry** provides information about processes, files, authentication, system changes, and other activity occurring on hosts.

**Network telemetry** provides visibility into connections, protocols, addresses, ports, and network behaviour.

**Authentication and identity telemetry** provides information about logins, failed authentication, privilege changes, account modifications, and identity-related events.

**Application logs** can expose suspicious requests, errors, authentication activity, and application-specific security events.

**Security controls** such as firewalls, IDS/IPS, EDR platforms, and email security systems can contribute security-specific detections.

**Cloud telemetry** provides visibility into API calls, identity activity, configuration changes, and cloud resource access.

## SIEM and the SOC

A SIEM is closely associated with the **Security Operations Centre (SOC)**.

A typical relationship is:

```text
Data Sources
     ↓
Collection
     ↓
Normalization
     ↓
Correlation / Analysis
     ↓
Detection
     ↓
Alert
     ↓
SOC Analyst
     ↓
Investigation
     ↓
Response
```

The SIEM provides the analytical and visibility layer, while analysts provide human interpretation and decision-making.

A SIEM does not replace a SOC analyst. An alert still requires context, validation, prioritization, and often investigation across additional systems.

Related concept: [[Defensive-Security]].

## Detection Engineering

A SIEM becomes significantly more valuable when its detection logic is designed around the environment being monitored.

A generic rule might detect a large number of failed authentication attempts, while a more useful detection could correlate failed attempts with a subsequent successful login from the same source followed by suspicious activity.

Effective detection engineering therefore requires understanding:

* The normal behaviour of the environment.
* Available telemetry.
* Attack techniques.
* Relevant assets.
* Identity relationships.
* Expected administrative activity.
* The consequences of false positives and false negatives.

Detection rules should be continuously evaluated and improved.

## False Positives and False Negatives

SIEM detection is subject to two major classes of error.

A **false positive** occurs when legitimate activity is incorrectly identified as malicious.

A **false negative** occurs when malicious activity is not detected.

Excessive false positives create alert fatigue and can cause analysts to ignore or overlook important alerts. Excessive false negatives create blind spots where attacks remain undetected.

Good SIEM engineering therefore aims for useful, contextualized detections rather than simply maximizing the number of alerts.

## SIEM and Incident Response

SIEM systems are particularly valuable during incident response because they provide historical context.

An analyst investigating a compromised host may use SIEM data to determine:

* When suspicious activity began.
* Which account was involved.
* Which systems were accessed.
* What authentication events occurred.
* Whether similar activity occurred elsewhere.
* Which network connections were established.
* Whether the activity continued after containment.

This makes SIEM an important source of evidence during incident investigation, although it should not be considered the only source of forensic evidence.

Related concepts: [[Digital-Forensics]], [[Incident-Response]], [[Defensive-Security]].

## Threat Intelligence

Threat intelligence can enrich SIEM analysis by providing additional context about indicators and adversary behaviour.

Examples include:

* Malicious IP addresses.
* Malicious domains.
* File hashes.
* Known command-and-control infrastructure.
* Malware families.
* MITRE ATT&CK techniques.

Threat intelligence should not be treated as automatically authoritative. Indicators can become outdated, be shared incorrectly, or overlap with legitimate infrastructure. Context and validation remain necessary.

## SIEM Limitations

A SIEM does not automatically provide complete visibility.

If a system does not generate relevant telemetry, or if that telemetry is not collected, the SIEM cannot reconstruct events that were never observed.

Other limitations include:

* High data volume.
* Storage costs.
* Incomplete telemetry.
* Poorly configured log sources.
* Excessive false positives.
* Detection blind spots.
* Time synchronization problems.
* Incorrect parsing or normalization.
* Poorly designed detection rules.

A SIEM therefore depends on good logging, time synchronization, asset visibility, detection engineering, operational processes, and skilled analysts.

## SIEM as Part of Defensive Architecture

SIEM should be considered one component of a larger defensive ecosystem rather than a complete security solution.

A mature environment may combine:

```text
Endpoints
   ↓
EDR / OS Logs

Network
   ↓
Firewall / IDS / Network Telemetry

Identity
   ↓
Authentication / Directory Logs

Applications
   ↓
Application / Web Logs

Cloud
   ↓
Cloud Audit / Security Logs

          ↓

         SIEM

          ↓

Detection + Correlation

          ↓

         SOC

          ↓

Incident Response
```

The effectiveness of this architecture depends on whether the collected telemetry provides enough context to detect and investigate relevant threats.

## SIEM and Logging

Logging is the foundation upon which SIEM operates.

A SIEM cannot compensate for an environment that does not generate appropriate security events. Logging policies should therefore define what events are collected, how long they are retained, how their integrity is protected, and which events require monitoring or alerting.

This relationship can be summarized as:

**Logging generates evidence.**

**SIEM centralizes and analyzes that evidence.**

**Detection logic turns evidence into alerts.**

**Analysts turn alerts into investigations and decisions.**

## Related Notes

* [[Defensive-Security]]
* [[Logs]]
* [[Incident-Response]]
* [[Digital-Forensics]]
* [[IDS]]
* [[Firewall]]
* [[Cyber-Notes-Jr-Fundamentals/05-Operating-Systems/Active-Directory]]
* [[Windows]]
* [[Cyber-Notes-Jr-Fundamentals/09-Cheatsheets/Linux]]
* [[OWASP-Top-10]]