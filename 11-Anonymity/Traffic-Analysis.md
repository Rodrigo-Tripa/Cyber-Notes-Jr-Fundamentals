# Traffic Analysis

> Traffic analysis studies observable communication patterns rather than the semantic content of the communication. Its objective is to infer properties of a conection, its endpoints, or the activity being performed from metadata such as timing, volume, direction and packet structure.

> **Recomended knowledge:** before reading this note, it is useful to understand the **OSI/TCP-IP models, TCP, IP addressing and routing, packets and frames, DNS, TLS, basic probability and statistics, and the fundamentals of Tor/onion routing**. Familiarity with Wireshark, `tcpdump` or `tshark` will make the practical sections considerably easier. A basic understanding of Python is also useful for the analysi examples

## 1. What Traffic Analysis Actually Observes

Encryption changes what an observer can learn from the **content** of a communication. It does not necessarily remove the observable properties of the communication itself.

Consider an encrypted TCP connection:

```text
Client ──────────────── Server
       encrypted data
```

An observer may not know the plaintext, but can potentially record:

```text
timestamp
direction
packet size
packet count
burst duration
idle periods
flow duration
connection frequency
```

Represent a captured flow as a time-ordered sequence:

```text
F = {(t₁, s₁, d₁), (t₂, s₂, d₂), ..., (tₙ, sₙ, dₙ)}
```

where:

- `tᵢ` = timestamp of observation `i`
    
- `sᵢ` = observed size
    
- `dᵢ` = direction
    

The analyst does not need to recover the plaintext if the sequence itself contains a distinctive pattern.

This produces one of the fundamental principles of traffic analysis:

> **Confidentiality of content does not imply confidentiality of traffic characteristics.**

For anonymity systems, this matters because the observer is often interested not in _what was said_, but in relationships such as:

`Source → Communication Pattern → Destination`

or:

`Observation A → same pattern → Observation B`

The goal of traffic analysis is therefore often **inference**, not decryption.

Tor's design explicitly recognises this limitation. Its low-latency architecture is not intended to protect against an adversary capable of observing both ends of a connection and correlating timing and volume.

---

## 2. Traffic as a Time Series

A useful mathematical abstraction is to treat network activity as a time series.

For a unidirectional flow:

```text
X(t) = amount of traffic observed at time t
```

In practical captures, this may be represented as discrete events:

```text
time     bytes
0.000    517
0.013    517
0.014    1034
0.210    1518
1.734    517
```

The interesting information is often not the individual packet, but the **shape of the sequence**.

For example:

```text
request
████████████
response
██
idle
request
████████████████████
response
████
```

The pattern of bursts and gaps can describe application behaviour.

A web page may generate one characteristic sequence while a video stream generates another. An interactive SSH session produces a very different pattern from a bulk download.

Common traffic features include:

```text
total bytes
total packets
bytes per second
packets per second
flow duration
inter-arrival times
burst sizes
burst duration
direction changes
upstream/downstream ratio
```

The important point is that traffic analysis converts a network trace into a **feature representation**.

That representation can then be analysed statistically or used as input to a classifier.

---

## 3. Packet Size, Direction and Timing

Three properties are especially important in many traffic-analysis problems:

**Size:** how much information is transmitted.

**Direction:** whether data travels toward or away from the observer.

**Timing:** when transmissions occur.

Consider two hypothetical traces:

```text
A:
→ 517
→ 517
→ 1034
← 1518
← 1518
← 517

B:
→ 517
← 1518
→ 517
→ 517
← 1518
```

Even though the payloads are encrypted, the sequences may remain statistically distinguishable.

Direction can be represented numerically:

```text
outgoing = +1
incoming = -1
```

A trace then becomes something similar to:

```text
(+517, +517, +1034, -1518, -1518, -517)
```

From this representation, an analyst can derive higher-level structures such as burst lengths and direction transitions.

Timing provides another dimension.

Define inter-arrival time as:

```text
Δtᵢ = tᵢ - tᵢ₋₁
```

A sequence of inter-arrival times can reveal periodic or bursty behaviour.

Consequently, simply hiding payload contents is insufficient if the application produces a sufficiently distinctive observable pattern.

---

## 4. Flow-Level Features

Packet-level data is often too granular. Analysts therefore aggregate packets into **flows**.

For a flow `F`, useful features may iclude:

```text
duration(F)
bytes_up(F)
bytes_down(F)
packets_up(F)
packets_down(F)
mean_IAT(F)
std_IAT(F)
max_burst(F)
```

A simple Python representation might be:

```python
from dataclasses import dataclass

@dataclass
class Packet:
    timestamp: float
    size: int
    direction: int  # +1 outbound, -1 inbound

def flow_features(packets: list[Packet]) -> dict[str, float]:
    if not packets:
        return {}

    packets = sorted(packets, key=lambda p: p.timestamp)

    duration = packets[-1].timestamp - packets[0].timestamp

    up = [p for p in packets if p.direction > 0]
    down = [p for p in packets if p.direction < 0]

    iat = [
        packets[i].timestamp - packets[i - 1].timestamp
        for i in range(1, len(packets))
    ]

    return {
        "duration": duration,
        "bytes_up": sum(p.size for p in up),
        "bytes_down": sum(p.size for p in down),
        "packets_up": len(up),
        "packets_down": len(down),
        "mean_iat": sum(iat) / len(iat) if iat else 0.0,
    }
```

This code does not attempt to inspect or decrypt application payloads. It extracts metadata from an already captured sequence.

That distinction is central to traffic analysis: **the useful signal may exist entirely outside the plaintext**.

---

## 5. Statistical Inference

Once traffic has been converted into features, the problem becomes one of inference.

Suppose we have an observed trace `T` and possible classes:

```text
C₁ = website A
C₂ = website B
C₃ = website C
```

A classifier attempts to estimate:

```text
P(Cᵢ | T)
```

the probability that trace `T` belongs to class `Cᵢ`.

Using Bayes' theorem:

```text
P(Cᵢ | T) = P(T | Cᵢ) P(Cᵢ) / P(T)
```

This does not require the analyst to know the plaintext.

The trace becomes evidence.

The more distinctive the traffic distribution of a class, the more useful that evidence becomes.

However, statistical inference must be evaluated carefully. A classifier achieving 95% accuracy in a small laboratory dataset does not necessarily mean that the same classifier will achieve 95% accuracy against real Internet traffic.

Dataset construction, class imbalance, temporal drift, background traffic, network congestion and the **open-world problem** can dramatically change performance.

This distinction is particularly important in anonymity research because unrealistic experimental assumptions can make attacks appear considerably stronger than they are in deployment.

---

## 6. Website Fingerprinting

**Website Fingerprinting (WF)** is the problem of inferring which website a user visits from the traffic pattern generated by their connection.

The conceptual attack is:

```text
Known websites
      ↓
collect traces
      ↓
extract features
      ↓
train classifier
      ↓
observe target trace
      ↓
predict website
```

A classifier might learn that different websites produce different combinations of:

```text
packet directions
burst sizes
packet ordering
inter-arrival times
total volume
page-load phases
```

This is particularly relevant to Tor because an observer near the client can potentially observe the encrypted traffic entering the Tor network without seeing the destination in plaintext.

Research has demonstrated that website fingerprinting can work surprisingly well under controlled conditions. A 2022 USENIX study evaluating attacks using genuine Tor traffic found over 95% accuracy when monitoring a small set of five popular websites, while performance dropped below 80% when the monitored set increased to 25 websites in their tested real-world setting.

The critical lesson is not that "Tor can be easily defeated". It is that **traffic patterns can contain information about application-level activity even when content and destination addressing are protected**.

---

## 7. Closed World vs Open World

Traffic-analysis results are strongly affected by the experimental model.

A **closed-world** experiment assumes that the target belongs to a small known set:

```text
{site A, site B, site C, site D}
```

The classifier only needs to decide which member of that set produced the trace.

An **open-world** experiment is more realistic:

```text
Known monitored sites
+
large unknown population
```

The classifier must determine not only _which known site_ was visited, but whether the trace belongs to the monitored set at all.

This dramatically increases difficulty.

Suppose a classifier achieves:

```text
98% accuracy
```

when choosing between five websites.

That number is almost meaningless if the real environment contains hundreds of thousands of possible destinations.

Therefore, serious traffic-analysis research should report more than raw accuracy.

Useful metrics include:

```text
precision
recall
false-positive rate
false-negative rate
confusion matrix
ROC-AUC
top-k accuracy
```

The experimental model must also describe the observation point, dataset generation procedure, background traffic and temporal separation between training and testing.

Without this information, a headline accuracy number can be misleading.

---

## 8. Correlation Attacks

A different problem occurs when an adversary can observe traffic at **two or more points**.

Consider an anonymity network:

```text
Client → Entry → Middle → Exit → Destination
```

An observer at the client side sees:

```text
T_in
```

while another observer near the destination sees:

```text
T_out
```

The attacker attempts to determine whether:

```text
T_in ≈ T_out
```

The comparison can use:

```text
packet timing
packet volume
burst structure
direction
flow duration
rate changes
```

A simple conceptual similarity measure might be:

```text
score(T₁, T₂) =
    α · timing_similarity
  + β · volume_similarity
  + γ · burst_similarity
```

A high score does not automatically prove that two traces are the same communication. It produces evidence.

This distinction becomes crucial under probabilistic inference: the attacker is not necessarily recovering a cryptographic key or breaking encryption. They are estimating whether two observations are statistically related.

Tor's own design literature identifies this as a fundamental limitation of low-latency anonymity. An adversary able to measure both ends of a connection can correlate timing and traffic volume; defeating a sufficiently strong version of this problem generally requires significant padding or latency.

---

## 9. Burst Analysis

Rather than analysing every packet individually, traffic can be divided into **bursts**.

A burst is a period of relatively dense activity separated from another period by an idle or low-activity interval.

For example:

```text
→→→→→→→    ←←
       idle
→→→→→→→→→  ←←←
       idle
→→         ←
```

We can represent a burst using:

```text
(direction, packet_count, byte_count, duration)
```

For example:

```text
(+1, 17 packets, 12640 bytes, 85 ms)
(-1,  4 packets,  3020 bytes, 14 ms)
```

Bursts are useful because application behaviour is often burst-oriented.

A browser loading a page can produce:

```text
request burst
→ response burst
→ additional requests
→ image/script bursts
→ idle
```

An interactive application might produce:

```text
small request
small response
idle
small request
small response
```

Traffic-analysis systems can use these structural differences to recognise application behaviour without inspecting the actual content.

---

## 10. Intersection and Temporal Attacks

Not all attacks operate on a single trace.

An **intersection attack** uses repeated observations to progressively reduce the set of possible users.

Suppose an anonymous service has possible users:

```text
A = {1,2,3,4,5,6,7,8}
```

At time `t₁`, the attacker knows:

```text
A₁ = {1,2,3,4,5}
```

At time `t₂`:

```text
A₂ = {2,3,4,5,6}
```

At time `t₃`:

```text
A₃ = {2,3,4,5}
```

The repeated intersection becomes:

```text
A₁ ∩ A₂ ∩ A₃ = {2,3,4,5}
```

With enough observations, the anonymity set can shrink substantially.

The key insight is that anonymity can deteriorate through **longitudinal observation** even when each individual observation appears ambiguous.

Temporal information therefore matters both within a connection and across weeks or months of activity.

---

## 11. Padding and Cover Traffic

A direct defence against traffic analysis is to alter the observable traffic pattern.

One basic strategy is **padding**: adding bytes or packets that do not contain meaningful application data.

Without padding:

```text
real traffic:
███     █████████      ██
```

With padding:

```text
padded:
██████  ███████████    █████
```

The purpose is to reduce the amount of information an observer can infer from size or timing.

More advanced systems can generate **cover traffic**, producing additional activity even when the application has little or no real data to transmit.

However, padding has costs:

```text
more bandwidth
more CPU
more network load
more battery consumption
more latency
```

There is therefore a fundamental trade-off between:

`anonymity`

and:

`efficiency`

Tor currently implements both connection-level and circuit-level padding mechanisms. Its specification describes connection-level `PADDING` traffic and circuit-level padding state machines designed to obscure particular traffic patterns while controlling overhead.

The Tor protocol also uses fixed-size cells for much of its relay traffic, which reduces the amount of information that can be directly inferred from individual cell sizes.

Padding is therefore not simply "send random bytes". It is an engineering problem involving statistical distributions, state machines, bandwidth constraints and the characteristics of the traffic that must be hidden.

---

## 12. Practical Analysis with PCAP

The most useful way to learn traffic analysis is to work with captures.

A simple `tshark` workflow can extract packet timestamps, lengths and directions:

```bash
tshark -r capture.pcap \
  -T fields \
  -e frame.time_epoch \
  -e frame.len \
  -e ip.src \
  -e ip.dst
```

This produces data that can be converted into a time series.

For example:

```text
timestamp       length    source       destination
1724420000.001  74        10.0.0.10    10.0.0.1
1724420000.014  1514      10.0.0.1     10.0.0.10
1724420000.017  1514      10.0.0.1     10.0.0.10
```

A small Python analysis can then calculate inter-arrival times:

```python
from statistics import mean, stdev

timestamps = [
    1724420000.001,
    1724420000.014,
    1724420000.017,
]

iat = [
    b - a
    for a, b in zip(timestamps, timestamps[1:])
]

print("Mean IAT:", mean(iat))

if len(iat) > 1:
    print("IAT StdDev:", stdev(iat))
```

For larger datasets, it is useful to transform captures into a tabular structure such as:

```text
timestamp | direction | size | iat
```

and then derive features such as:

```text
total_bytes
up_bytes
down_bytes
duration
packet_count
mean_iat
iat_variance
burst_count
max_burst
direction_changes
```

At this stage, visualisation becomes extremely useful.

A simple plot of:

```text
time → bytes
```

can reveal patterns that are difficult to see from raw packet listings.

For responsible research, analysis should begin with **your own captures or explicitly provided datasets**. The objective is to understand the structure of traffic and evaluate privacy properties, not to deanonymise unrelated users.

---

## 13. Traffic Analysis as Machine Learning

Modern traffic analysis can become a machine-learning problem.

The pipeline can be represented as:

```text
PCAP
 ↓
Pre-processing
 ↓
Feature extraction
 ↓
Feature normalisation
 ↓
Training set
 ↓
Model
 ↓
Test trace
 ↓
Prediction
```

A traditional model might use manually engineered features:

```text
Random Forest
SVM
k-NN
Logistic Regression
```

More recent research has also explored deep-learning approaches that operate on sequences of packet directions, timings or other representations.

However, machine learning does not eliminate the fundamental problem of data quality.

A model can learn:

```text
website
```

or accidentally learn:

```text
network condition
capture environment
browser version
dataset artifact
```

This is known as **dataset leakage** or a related form of confounding.

A strong experiment should therefore use:

- Separate training and testing captures
    
- Different sessions
    
- Different network conditions
    
- Temporal separation
    
- Realistic background traffic
    
- Open-world evaluation where appropriate
    

The question is not merely:

> "Can the model classify this dataset?"

It is:

> **"Does the model learn a property of the target traffic that survives when the experimental conditions change?"**

That distinction separates a meaningful security result from a benchmark artifact.

---

## 14. Limits of Traffic Analysis

Traffic analysis is powerful, but it is not omnipotent.

The strength of an attack depends on:

```text
observation position
+
amount of collected data
+
traffic visibility
+
quality of distinguishing features
+
number of possible targets
+
background noise
+
defensive padding
+
network variability
```

A local observer might know that a machine is communicating with Tor but not know the final destination.

A website may know that a request arrived from a Tor exit but not know the original IP.

A researcher monitoring a small set of websites may achieve high website-fingerprinting accuracy.

A global observer may have substantially greater correlation capabilities.

These are different threat models producing different results.

The most important conclusion is therefore not that traffic analysis "breaks anonymity networks".

Rather:

> **An anonymity network can reduce direct attribution while leaving statistical information available to sufficiently capable observers.**

Low-latency anonymity systems deliberately accept some of this trade-off because eliminating all timing and volume information would require substantial changes to the communication model.

This creates a fundamental tension:

```text
Low latency
      ↕
Traffic indistinguishability
      ↕
Bandwidth overhead
```

Improving one dimension often imposes costs on another.

---

## Practical Mental Model

A useful way to reason about a network trace is:

```text
Payload
  │
  ├── hidden by encryption
  │
  ▼
Observable metadata
  │
  ├── time
  ├── size
  ├── direction
  ├── frequency
  ├── duration
  └── structure
  │
  ▼
Feature extraction
  │
  ▼
Statistical inference
  │
  ▼
Possible attribution / classification / correlation
```

The central research problem is therefore:

> **How much information about an activity survives after its content has been encrypted and routed through an anonymity system?**

Traffic analysis studies the answer to that question.

---

## Key Concepts

|Concept|Meaning|
|---|---|
|Traffic Analysis|Inferring information from observable communication characteristics|
|Flow|A logical sequence of related network traffic|
|Inter-Arrival Time|Time between consecutive observations|
|Burst|Temporally concentrated sequence of traffic|
|Traffic Correlation|Comparing observations from multiple locations|
|Website Fingerprinting|Inferring destination/activity from encrypted traffic patterns|
|Closed World|Classification among a predefined small set of targets|
|Open World|Classification with a large unknown population|
|Intersection Attack|Reducing anonymity through repeated observations|
|Padding|Adding data to obscure traffic characteristics|
|Cover Traffic|Generating traffic to make real activity less distinguishable|
|Anonymity Set|Set of plausible origins for an observed activity|

## Core Principle

> **Encryption hides meaning. Traffic analysis studies what remains observable around that meaning.**

A packet does not have to reveal its payload to reveal information.

Timing can reveal structure. Size can reveal volume. Direction can reveal interaction. Bursts can reveal application phases. Repeated observations can reveal behavioural patterns. And when observations from multiple locations can be compared, seemingly harmless metadata can become evidence of correlation.

For anonymity enginering, this means that protecting content is only one part of the problem.

The deeper objective is **traffic analysis resistance**: making different users, destinations and activities as difficult as possible to distinguish from one another without introducing unacceptable latency, bandwidth overhead or system complexity.

## References

Tor Project — Tor Specifications: cell format, flow control and padding mechanisms.

Cherubin, Jansen & Troncoso — _Online Website Fingerprinting: Evaluating Website Fingerprinting Attacks on Tor in the Real World_, USENIX Security 2022.

Tor Project — _Challenges in Deploying Low-Latency Anonymity_.