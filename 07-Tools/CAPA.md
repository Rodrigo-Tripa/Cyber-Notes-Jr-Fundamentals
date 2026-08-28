#tool #malware-analysis #static-analysis #reverse-engineering #mitre-attack

# CAPA

**CAPA (Common Analysis Platform for Artifacts)** is a malware analysis tool designed to identify capabilities present in executable files and other supported artifacts. Rather than requiring the analyst to manually identify every low-level instruction or API call, CAPA applies a collection of detection rules to infer higher-level behaviours from an artifact.

CAPA is primarily useful for **static malware analysis** and triage. It can help an analyst quickly determine what a sample appears capable of doing before proceeding to deeper reverse engineering or dynamic analysis.

## Core Concept

The central concept behind CAPA is the distinction between a program's implementation details and its **capabilities**.

A binary may contain low-level instructions, imported functions, strings, and other technical artifacts. CAPA uses these indicators to identify higher-level behaviours such as:

- Creating or modifying files.
- Communicating over a network.
- Executing commands.
- Manipulating processes.
- Using PowerShell.
- Performing anti-analysis checks.
- Interacting with the Windows Registry.
- Collecting information from the host.

The result provides an analyst with a behavioural overview of the artifact without requiring the entire program to be reverse engineered manually.

## Rule-Based Analysis

CAPA relies on **rules** that describe patterns associated with particular capabilities. These rules allow low-level evidence within an artifact to be mapped to higher-level behavioural conclusions.

This rule-based approach makes CAPA particularly useful during malware triage. An analyst can quickly identify potentially interesting capabilities and then decide which areas require deeper investigation.

CAPA results should therefore be treated as **evidence for further analysis**, rather than absolute proof of malicious intent. A detected capability indicates that the artifact contains characteristics associated with a behaviour; the analyst still needs to understand the context in which that capability is implemented.

## MITRE ATT&CK

CAPA can associate identified behaviours with **MITRE ATT&CK** techniques. This provides a common language for describing adversary behaviours and makes CAPA output useful for threat intelligence, detection engineering, and incident analysis.

For example, a capability associated with process injection can be represented using the corresponding ATT&CK technique, allowing the analyst to move from a technical observation to a standardized behavioural classification.

## Analysis Workflow

CAPA is most useful as an early stage of a broader malware analysis workflow.

An analyst can first perform basic triage to determine the file type and characteristics of a suspicious artifact. CAPA can then be used to identify capabilities and generate hypotheses about the program's behaviour.

Those findings can guide deeper analysis using tools for disassembly, debugging, string analysis, memory analysis, or network inspection. This reduces the amount of time spent investigating irrelevant portions of a binary.

## Static Analysis Context

CAPA does not require the malware to be executed in order to identify many capabilities. This makes it suitable for an initial analysis stage where execution of an unknown sample would introduce unnecessary risk.

Static analysis can reveal useful information without changing the state of the sample or the analysis environment. However, static analysis has limitations: obfuscation, packing, dynamic code generation, encrypted configuration data, and runtime-dependent behaviour can make capabilities difficult or impossible to identify statically.

For this reason, CAPA should generally be considered one component of a broader malware-analysis methodology.

## Limitations

CAPA's results depend on the evidence available to its rules. A capability may be missed if the relevant behaviour is obfuscated, dynamically generated, packed, or implemented in a way that does not match existing rules.

Conversely, identifying a capability does not necessarily prove that the program actively performs that behaviour under every execution path.

CAPA is therefore best used to **form hypotheses and accelerate triage**, with deeper static or dynamic analysis used to validate important findings.

## Related Notes

- [[Defensive-Security]]
- [[Digital Forensics]]
- [[MITRE ATT&CK]]
- [[REMnux]]
- [[FlareVM]]