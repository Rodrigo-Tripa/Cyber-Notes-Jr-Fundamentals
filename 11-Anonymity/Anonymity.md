# Anonymity

> Anonymity is not the absence of identity. It is the inability to reliably associate an action with a specific identity.

## 1. What Is Anonymity?

Anonymity is the property of performing an action without allowing an observer to reliably determine which individual or entity performed it. In computing, this usually means preventing an activity from being linked to a real-world identity, device, account, or previously observed activity

This distinction is important because anonymity is not equivalent to privacy. Privacy concerns **what information is exposed**, while anonymity concerns **whether that information can be attributed to someone**. A message may be completely visible to everyone and still be anonymous if nobody can determine who authored it. Conversely, a private encrypted message may still destroy anonymity if the communication can be reliably associated with a known identity.

Anonimity therefore depends on an observer's ability to establish a relationship:

`Action → Identity`

The objective of an anonymity system is to make this relationship sufficiently difficult or uncertain that the observer cannot confidently perform the attribution.

In practice, absolute anonymity is extremely difficult to achieve. Systems operate within assumptions about the adversary, the network, the software, the hardware, and the user's behaviour. A system can therefore provide anonymity **relative to a threat model**, rather than guaranteeing universal anonymity.

This makes anonymity fundamentally different from a binary security property. A person is not simply "anonymous" or "not anonymous"; anonymity exists within a particular context and against particular observers.

---

## 2. Anonymity, Privacy and Pseudonymity

These concepts are related but describe different properties.

**Privacy** concerns control over information. Encryption, access controls and data minimisation are primarily privacy mechanisms because they restrict who can observe information.

**Anonymity** concerns attribution. The objective is to prevent an action from being reliably associated with a particular identity.

**Pseudonymity** replaces a real identity with another persistent identifier. A pseudonym can hide a person's civil identity while still allowing their actions to be linked together.

For example, suppose a user communicates using the pseudonym `Astra`.

If nobody knows who `Astra` actually is, the user has some degree of pseudonymity. However, if every message can be linked to `Astra`, the activity is not anonymous relative to the pseudonym. An observer may not know the person's name, but can still recognise the same entity repeatedly.

This leads to an important distinction:

`Anonymity → Who performed the action?`

`Pseudonymity → Which pseudonym performed the action?`

`Privacy → What information was exposed?`

A system can therefore provide one property without providing the others. An encrypted account can have strong privacy but weak anonymity. An anonymous publication platform can provide anonymity while exposing the content publicly. A pseudonymous account can provide neither strong anonymity nor complete privacy.

---

## 3. The Anonymity Set

One of the central concepts in anonymity research is the **anonymity set**.

An anonymity set is the group of possible entities that could plausibly have performed a particular action from the perspective of an observer.

Consider a network containing 10,000 users. If an observer can determine that a particular action originated from exactly one user, the effective anonymity set is approximately:

`|A| = 1`

There is effectively no anonymity.

If the observer can determine only that the action originated from one of 10,000 users, the anonymity set is much larger:

`|A| = 10,000`

The larger the plausible set of users, the harder attribution becomes.

However, the size of the set alone is not sufficient. If one member is substantially more likely to have performed the action than the others, the anonymity is weaker than a simple count suggests.

This introduces the concept of **anonymity entropy**. If the observer assigns probabilities to possible identities, the uncertainty can be modelled using information-theoretic entropy:

`H(X) = -Σ p(x) log₂ p(x)`

where `p(x)` represents the probability that identity `x` is responsible for the observed action.

If all candidates are equally likely, uncertainty is maximised. If one candidate has a probability close to 1, uncertainty becomes very small even if many technically possible candidates exist.

An anonymity system therefore tries not merely to create a large population, but to make attribution **ambiguous and difficult to distinguish** within that population.

---

## 4. Unlinkability

Anonymity is not only about hiding an identity. It is also about preventing an observer from linking multiple actions together.

Suppose an anonymous user performs two actions:

`Action A → ?`

`Action B → ?`

If an observer cannot determine whether the same person performed both actions, the actions have some degree of **unlinkability**.

If the observer can determine:

`Action A ≈ Action B → same user`

then anonymity may be weakened even if neither action individually reveals the user's identity.

This is particularly relevant to web tracking. Cookies are an obvious example, but they are only one mechanism. Browser fingerprints, behavioural patterns, timing information, account identifiers and network characteristics can all allow different activities to be correlated.

Anonymity therefore has at least two distinct problems:

**Attribution:** determining who performed an action.

**Linkability:** determining whether multiple actions belong to the same entity.

A system that solves attribution but fails at linkability may still allow a detailed profile to be constructed around an unknown person.

This is why anonymity systems often rely on **identity separation and compartmentalization** rather than simply hiding an IP address.

---

## 5. Anonymity and Metadata

Encryption protects the content of communication, but it does not necessarily conceal its metadata.

Metadata can include:

- Source and destination
    
- Time of communication
    
- Duration
    
- Packet sizes
    
- Frequency
    
- Protocol characteristics
    
- Device information
    
- Language and timezone
    
- Account identifiers
    
- File metadata
    

Consider an encryptted communication channel between two parties. An observer may be unable to read the messages while still observing that communication occurs every day at approximately the same time.

If the observer can independently identify one endpoint, timing and traffic characteristics may provide enough information to correlate the anonymous activity with that known endpoint.

This is the basis of **traffic analysis** and, in stronger adversarial models, **traffic correlation**.

Consequently:

`Encryption ≠ Anonymity`

and:

`Encryption ≠ Metadata Protection`

Strong anonymity requires consideration of both the information contained within communication and the observable characteristics surrounding that communication.

---

## 6. The Human and Endpoint Problem

Anonymity is not exclusively a network property. The endpoint itself can reveal information.

A computer can expose characteristics through its operating system, browser, installed software, fonts, screen configuration, hardware capabilities, language, timezone and other observable properties. When combined, these characteristics can form a **fingerprint** capable of distinguishing one environment from others.

Behaviour can be even more revealing.

Users have recurring patterns in:

- Writing style
    
- Activity schedules
    
- Language
    
- Navigation habits
    
- Software usage
    
- Account selection
    
- Repeated mistakes
    
- Communication patterns
    

This creates an important principle:

> An anonymous network connection does not guarantee an anonymous endpoint.

The same problem applies to identity reuse. If an otherwise anonymous environment is used to authenticate to a personally identifying account, the network may successfully hide the user's location while the application itself learns the identity.

Anonymity therefore has to be considered across the entire chain:

`User → Device → Operating System → Application → Network → Service`

A weakness at any relevant layer can provide an attribution path.

---

## 7. Threat Models and Limits

There is no universal definition of "anonymous" because anonymity depends on the capabilities of the observer.

A website may only observe HTTP-level information. An Internet Service Provider may observe network connections. A local attacker may observe the physical machine. A sophisticated adversary may possess information from multiple independent sources and attempt to correlate them.

The correct question is therefore not:

> "Is this system anonymous?"

It is:

> "Anonymous against whom, under what conditions, and for how long?"

A useful threat model defines at least:

**Assets:** what identity or activity must remain unlinked.

**Adversary:** who is attempting the attribution.

**Capabilities:** what the adversary can observe, collect or control.

**Attack surface:** which components can leak identifying information.

**Security objective:** what relationship the system must prevent.

**Failure conditions:** what event would allow attribution or correlation.

This approach prevents exaggerated claims. A system might provide strong protection against ordinary web tracking while providing little protection against a powerful adversary capable of global traffic observation.

Anonymity is therefore always relative to assumptions.

---

## 8. Anonymity as a System Property

A useful way to think about anonymity is as a property that emerges from multiple layers rather than from a single tool.

A simplified modell is:

`Identity`  
↓  
`User Behaviour`  
↓  
`Endpoint`  
↓  
`Application`  
↓  
`Network`  
↓  
`Destination`

Each layer can contribute identifying information.

A network anonymity system can reduce information at the network layer. Anti-fingerprinting mechanisms can reduce information exposed by the browser. Amnesic systems can reduce persistent traces on the endpoint. Compartmentalization can reduce linkability between identities. Operational security can prevent the user from voluntarily reconnecting anonymous activity to an identified persona.

The overall anonymity of the system is therefore constrained by its weakest relevant attribution path.

This also explains why there is no single "anonymous computer". There are only systems designed to minimise particular forms of attribution under particular threat models.

The goal of anonymity engineering is consequently not to make a machine magically invisible. It is to **reduce observable information, increase uncertainty, prevent correlation, and maintain separation between identities and activities**.

The following topics build directly upon this foundation: anonymity networks, Tor, browser fingerprinting, metadata leakage, operational security, compartmentalization, amnesic systems and traffic analysis.

---

## Key Concepts

|Concept|Core Question|
|---|---|
|Privacy|What information can be observed?|
|Anonymity|Who performed the action?|
|Pseudonymity|Which persistent identity performed it?|
|Unlinkability|Can separate actions be connected?|
|Anonymity Set|How many entities could plausibly be responsible?|
|Fingerprinting|Can an environment be distinguished from others?|
|Metadata|What information exists outside the content itself?|
|Threat Model|Against whom must anonymity hold?|
|Compartmentalization|Can identities and activities be kept separate?|
|OPSEC|Can user behaviour preserve the intended security properties?|

## Core Principle

> **Anonymity is the reduction of reliable attribution and correlation, not simply the concealment of an IP address.**

A robust anonymity architecture therefore has to consider the user, endpoint, applications, network, destination, metadata and adversary simultaneously.