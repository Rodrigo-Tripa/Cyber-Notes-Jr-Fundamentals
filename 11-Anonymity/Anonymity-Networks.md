# Anonymity Networks

> An anonymity network is a communication system designed to reduce the ability to associate network activity with the identity or location of the entity generating it.

## 1. The Problem Anonymity Networks Solve

Ordinary Internet communication exposes a fundamental relationship between a user and their network activity.

In a simplified model:

`User → ISP → Internet → Destination`

The destination can often observe the source IP address, while the ISP can observe that the user's connection is communicating with particular infrastructure. Even when application data is encrypted, network-level metadata such as timing, volume and destination may remain observable.

An anonymity network attempts to break or weaken the direct relationship:

`User ↔ Destination`

Instead of allowing the user to communicate directly with the destination, traffic is routed through intermediary infrastructure.

A simplified architecture might look like:

`User → Relay A → Relay B → Destination`

The objective is not necessarily to make the communication invisible. Instead, different participants should possess different pieces of information.

Ideally, the first relay knows where traffic came from but not where it ultimately goes, while the final relay knows where traffic is going but not the original user's network identity.

This principle is commonly described as **distributed knowledge**.

No single intermediary should possess enough information to trivially reconstruct the entire communication relationship.

---

## 2. Proxies, VPNs and Anonymity Networks

Not every intermediary network provides the same anonymity properties.

A **proxy** generally acts as an intermediary between a client and a destination:

`Client → Proxy → Destination`

The destination sees the proxy rather than the client's address. However, the proxy may know both the client and destination.

A **VPN** creates a similar trust relationship at the network level:

`Client → VPN → Internet`

The destination normally sees the VPN's address, while the VPN provider can potentially observe information about the client's connections. The VPN therefore changes **who must be trusted**, but does not inherently eliminate the trusted intermediary.

An anonymity network uses multiple parties and specialised routing mechanisms to reduce the amount of information available to any individual intermediary.

The distinction can therefore be simplified as:

`Proxy → hides source from destination`

`VPN → moves network trust to the VPN provider`

`Anonymity network → distributes knowledge across multiple parties`

This does not mean VPNs or proxies are useless. They solve different problems and can provide valuable privacy or security properties. The important point is that **hiding an IP address is not equivalent to achieving strong anonymity**.

---

## 3. Onion Routing

One of the most important architectures for anonymity networks is **onion routing**.

Instead of sending a message through a single intermediary, the client constructs a path containing multiple relays. The communication is protected in multiple cryptographic layers, conceptually resembling layers of an onion.

Consider a three-relay circuit:

`Client → Guard → Middle → Exit → Destination`

The client prepares the communication so that each relay can remove or process only the layer relevant to its position.

The guard learns the client's network connection and knows the next relay, but should not know the final destination.

The middle relay acts primarily as a forwarding point. It should not know the original client or final destination.

The exit relay communicates with the destination. It knows the destination but should not know the original client's network identity.

The result is **partial knowledge at each hop**.

This architecture is fundamentally different from simply encrypting traffic between the user and one intermediary. The objective is not only confidentiality but also **information separation**.

However, onion routing does not make traffic mathematically impossible to analyse. An adversary capable of observing multiple parts of the network may still attempt to correlate traffic based on timing, volume or other characteristics.

---

## 4. Distributed Trust

The security model of an anonymity network depends heavily on how trust is distributed.

In a conventional connection:

`Client → Server`

the server receives the client's network information and the client directly communicates with the server.

With a single proxy:

`Client → Proxy → Server`

the proxy becomes a central point of trust.

With an onion-routing architecture:

`Client → Relay₁ → Relay₂ → Relay₃ → Server`

knowledge is distributed.

Relay₁ can observe the client.

Relay₃ can observe the destination.

Neither should independently possess complete information about the communication relationship.

This creates an important principle:

> **Anonymity can be strengthened by preventing any single component from obtaining sufficient information to perform attribution.**

The security of the system therefore depends not only on encryption but also on the topology and independence of its participants.

If one entity controls enough strategically positioned infrastructure, it may be able to observe multiple portions of a circuit. This is one reason anonymity networks must consider adversaries that can perform large-scale observation and correlation.

---

## 5. Anonymity Sets and User Populations

Anonymity networks depend on more than routing architecture. They also benefit from having a sufficiently large and diverse population of users.

Suppose an observer sees an activity originating from an anonymity network containing one million possible users. The observer may have difficulty determining which user generated the activity.

However, if only three users are active at the relevant time and the traffic pattern can be associated with one of them, the effective anonymity can become much smaller.

This is related to the **anonymity set** introduced in the previous note.

The network therefore benefits from users becoming difficult to distinguish from one another.

This creates a subtle engineering problem.

A user might attempt to make their configuration highly unusual in the belief that customisation improves privacy. In reality, a unique configuration can reduce the anonymity set by making the user easier to distinguish.

For this reason, anonymity-oriented systems frequently favour **standardisation and uniformity** over unrestricted customisation.

Anonymity is partly a property of the individual system and partly a property of the population in which that system operates.

---

## 6. Tor as an Onion-Routing Network

[Tor](https://www.torproject.org/) is one of the most widely deployed examples of an onion-routing anonymity network.

A typical Tor connection uses a circuit containing multiple relays. In simplified form:

`Client → Guard → Middle → Exit → Internet`

The client establishes cryptographic relationships with the relays and uses the circuit to forward traffic.

The **guard** is the entry point into the Tor network. It knows that the client is connecting to Tor, but it should not learn the final destination from the circuit alone.

The **middle relay** forwards traffic between the other relays and provides another layer of separation.

The **exit relay** is the point from which traffic reaches destinations on the normal Internet. Consequently, the destination generally observes the exit relay rather than the original client.

Tor also supports **onion services**, which allow services to operate within the Tor network without requiring a conventional public exit connection.

Tor is not simply a VPN with three servers. Its architecture is specifically designed around distributed knowledge and resistance to certain forms of traffic attribution.

However, Tor does not automatically make every application anonymous. Applications must be correctly configured, and information exposed at the application or endpoint level can still undermine anonymity.

---

## 7. Limitations and Correlation Attacks

Anonymity networks have fundamental limitations.

Consider:

`User → Anonymity Network → Destination`

If an adversary can observe traffic entering the network and independently observe traffic leaving it, they may compare characteristics such as:

- Timing
    
- Packet or flow sizes
    
- Burst patterns
    
- Frequency
    
- Duration
    
- Direction of traffic
    

If sufficiently distinctive patterns appear on both sides, the adversary may infer that the flows correspond to the same communication.

This is known as **traffic correlation**.

The important consequence is that anonymity networks do not necessarily provide protection against an adversary with sufficiently broad observation capabilities.

There are also more local attacks. A compromised endpoint can reveal information before traffic reaches the anonymity network. A browser fingerprint can identify a particular environment. A reused account can directly associate activity with a known identity. Application-level leaks can bypass the intended routing architecture entirely.

Therefore:

`Anonymity Network ≠ Complete Anonymity`

It is one layer in a larger system.

---

## 8. Design Principles

Several principles repeatedly appear across anonymity-network architectures.

**Distributed knowledge** reduces the amount of information available to any individual intermediary.

**Layered routing** prevents a single relay from directly observing the complete path.

**Population size** increases the number of plausible origins for an observed activity.

**Uniformity** reduces the ability to distinguish individual users through configuration differences.

**Separation of identities** prevents unrelated activities from becoming trivially linkable.

**Resistance to correlation** attempts to make traffic patterns less useful for determining relationships between network observations.

**Minimisation of trust** reduces dependence on a single operator or infrastructure provider.

These principles are more fundamental than any individual implementation. Technologies evolve, but the underlying problem remains the same: an anonymity network must make reliable attribution difficult without requiring every participant to trust a single intermediary.

---

## Core Principle

> **The purpose of an anonymity network is not simply to hide an IP address. It is to distribute knowledge and make the relationship between an entity and its network activity difficult to establish.**

The strongest designs therefore combine multiple mechanisms: layered routing, distributed trust, large anonymity sets, identity separation and resistance to traffic analysis.

Understanding these principles is essential before studying specific systems such as Tor, because the technology becomes much easier to understand once the underlying problem is clear.