# Transport Layer (TCP, UDP, Congestion)

> Subject: Computer Networks
> GATE weight: **3–5 marks** every year. TCP handshake, sliding window, congestion control, UDP.

---

## 1. Concept Explanation

### 1.1 Transport Layer Services

- **End-to-end** delivery (process-to-process).
- **Multiplexing/demultiplexing** via port numbers.
- **Reliability** (TCP).
- **Flow / congestion control** (TCP).

### 1.2 Port Numbers

16 bits → 0 to 65535.

| Range | Use |
|---|---|
| 0–1023 | Well-known (HTTP 80, HTTPS 443, SSH 22, FTP 21) |
| 1024–49151 | Registered |
| 49152–65535 | Dynamic / private |

### 1.3 UDP (User Datagram Protocol)

| Property | Value |
|---|---|
| Connection-oriented | No |
| Reliable | No |
| Header size | 8 bytes |
| Use cases | DNS, DHCP, video streaming, gaming |

**Header:**
```
| Src Port (2) | Dst Port (2) | Length (2) | Checksum (2) |
```

### 1.4 TCP (Transmission Control Protocol)

| Property | Value |
|---|---|
| Connection-oriented | Yes |
| Reliable | Yes |
| Header size | 20–60 bytes |
| Ordered | Yes |
| Use cases | HTTP, FTP, SMTP |

### 1.5 TCP Header

```
| Src Port (2)    | Dst Port (2)    |
| Seq # (4)                          |
| ACK # (4)                          |
| HLen | Reserved | Flags | Window (2) |
| Checksum (2)    | Urgent Ptr (2)   |
| Options + padding (variable)       |
| Data                               |
```

| Flag | Purpose |
|---|---|
| URG | Urgent pointer valid |
| ACK | ACK number valid |
| PSH | Push data |
| RST | Reset connection |
| SYN | Synchronize seq# |
| FIN | Finish |

### 1.6 TCP Connection (3-Way Handshake)

```
Client → Server: SYN, seq=x
Server → Client: SYN+ACK, seq=y, ack=x+1
Client → Server: ACK, ack=y+1
```

### 1.7 TCP Connection Termination (4-Way)

```
A → B: FIN
B → A: ACK
B → A: FIN
A → B: ACK
```

Half-close possible (one direction closed).

### 1.8 TCP Reliability Mechanisms

- **Sequence numbers** (per byte).
- **ACK numbers** (cumulative).
- **Retransmission** on timeout / 3 duplicate ACKs.
- **Checksum** (header + data).

### 1.9 Sliding Window in TCP

Receiver advertises window (rwnd). Sender can send up to rwnd unacknowledged bytes.

### 1.10 TCP Flow Control

Receiver tells sender how much to send via **advertised window**.

### 1.11 TCP Congestion Control

Sender maintains:
- **cwnd** (congestion window).
- **ssthresh** (slow start threshold).

Effective window = `min(cwnd, rwnd)`.

### 1.12 Slow Start

`cwnd` doubles each RTT until ssthresh.
- Initial cwnd = 1 MSS.
- After successful ACK, cwnd += 1 MSS.

Exponential growth.

### 1.13 Congestion Avoidance

After cwnd ≥ ssthresh:
- cwnd += 1 MSS per RTT (linear).

### 1.14 Loss Detection & Recovery

- **Timeout:** ssthresh = cwnd/2; cwnd = 1; restart slow start.
- **3 duplicate ACKs:** ssthresh = cwnd/2; cwnd = ssthresh; **fast retransmit + fast recovery**.

### 1.15 TCP Congestion Control Phases

```
Slow Start (exp) → cwnd = ssthresh →
Congestion Avoidance (linear) →
Loss event → reset based on type
```

### 1.16 TCP Variants

| Variant | Description |
|---|---|
| **TCP Tahoe** | Slow start + AIMD; reset on any loss |
| **TCP Reno** | Adds fast retransmit + fast recovery |
| **TCP NewReno** | Improved fast recovery |
| **TCP Vegas** | Delay-based |
| **TCP Cubic** | Cubic function (Linux default) |
| **BBR** | Bottleneck Bandwidth and RTT (Google) |

### 1.17 TCP Throughput

`Throughput = window / RTT` (window bytes in flight).

For BDP × RTT, use full BDP for max throughput.

### 1.18 RTT Estimation

`EstimatedRTT = (1 − α) · EstimatedRTT + α · SampleRTT`

`DevRTT = (1 − β) · DevRTT + β · |SampleRTT − EstimatedRTT|`

`Timeout = EstimatedRTT + 4 · DevRTT`

Typical α = 0.125, β = 0.25.

### 1.19 Nagle's Algorithm

Reduce small packet flooding:
- Don't send small segment if there's unacknowledged data.
- Send when buffer full or ACK received.

### 1.20 Silly Window Syndrome

Avoid sending tiny segments:
- **Receiver:** wait until window has half MSS or full segment.
- **Sender:** Nagle's algorithm.

### 1.21 TCP vs UDP Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection | Yes | No |
| Reliable | Yes | No |
| Ordered | Yes | No |
| Speed | Slower | Faster |
| Header | 20+ B | 8 B |
| Use | Web, email | DNS, video |

### 1.22 Common GATE Calculations

- **Throughput:** window/RTT.
- **Slow start cwnd:** doubles per RTT.
- **# RTTs to fill BDP:** log₂(BDP / MSS).
- **Time to send N bytes:** depends on cwnd + RTT.

> **Summary:** TCP reliable + connection-oriented (3-way handshake); UDP simple connectionless. TCP uses sliding window, congestion control (slow start + congestion avoidance + fast retransmit/recovery). Effective window = min(cwnd, rwnd).

---

## 2. Important Points

- **TCP** = reliable, connection-oriented; **UDP** = unreliable, connectionless.
- **3-way handshake**: SYN, SYN+ACK, ACK.
- **4-way termination**: FIN/ACK pairs.
- **Sliding window** for flow control.
- **cwnd** for congestion; **rwnd** for flow.
- **Slow start**: exponential cwnd growth.
- **Congestion avoidance**: linear (AIMD).
- **Fast retransmit**: 3 duplicate ACKs.
- **Timeout**: ssthresh = cwnd/2, cwnd = 1.
- **Nagle's algorithm** prevents small segments.
- **Effective throughput** = min(cwnd, rwnd) / RTT.
- **TCP Reno** = Tahoe + fast retransmit + fast recovery.
- **Port numbers** 16 bits.
- **UDP header** = 8 bytes.

---

## 3. Short Notes

```
TRANSPORT LAYER
 end-to-end, mux/demux, port-based

PORT NUMBERS (16 bits)
 well-known: 0-1023 (HTTP 80, HTTPS 443)
 registered: 1024-49151
 dynamic: 49152-65535

UDP
 8-byte header
 connectionless, unreliable
 use: DNS, DHCP, streaming

TCP
 20+ byte header
 connection-oriented, reliable, ordered

TCP HEADER
 src port, dst port, seq #, ack #
 HLen, flags (URG, ACK, PSH, RST, SYN, FIN)
 window, checksum, urgent ptr, options

3-WAY HANDSHAKE: SYN, SYN+ACK, ACK
4-WAY TERMINATION: FIN/ACK pairs

RELIABILITY
 seq + ACK numbers
 retransmit on timeout / 3 dup ACKs
 checksum

SLIDING WINDOW
 effective window = min(cwnd, rwnd)

CONGESTION CONTROL
 slow start: cwnd doubles per RTT until ssthresh
 congestion avoidance: cwnd += 1 MSS per RTT
 timeout: ssthresh = cwnd/2; cwnd = 1; slow start
 3 dup ACKs: ssthresh = cwnd/2; cwnd = ssthresh; fast retrans + recovery

TCP VARIANTS
 Tahoe, Reno, NewReno, Vegas, Cubic, BBR

RTT ESTIMATION
 EstimatedRTT = (1−α)·prev + α·SampleRTT
 DevRTT = (1−β)·prev + β·|Sample − Est|
 Timeout = Est + 4·Dev

NAGLE'S ALGORITHM: prevent small packets
SILLY WINDOW SYNDROME

THROUGHPUT = window / RTT
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | TCP 3-way handshake: SYN, SYN+ACK, ACK | ✅✅✅ |
| 2 | TCP 4-way termination | ✅✅ |
| 3 | UDP header = 8 B; TCP header = 20+ B | ✅✅ |
| 4 | Effective window = min(cwnd, rwnd) | ✅✅ |
| 5 | Slow start: cwnd doubles per RTT | ✅✅ |
| 6 | Congestion avoidance: linear AIMD | ✅✅ |
| 7 | 3 duplicate ACKs → fast retransmit | ✅✅ |
| 8 | Throughput = window / RTT | ✅✅ |
| 9 | Timeout = EstimatedRTT + 4·DevRTT | ✅ |
| 10 | TCP Tahoe vs Reno: + fast recovery | ✅ |
| 11 | Loss → ssthresh = cwnd/2 | ✅ |
| 12 | Port numbers 16 bits | ✅ |

### Tricks

- **For slow start trace:** double cwnd until ssthresh; then linear.
- **For loss event:** distinguish timeout from 3 dup ACKs.
- **For throughput:** ensure window ≥ BDP.
- **For TCP Reno fast recovery:** stay in CA after recovery.
- **For TCP timeout:** uses estimated RTT + 4·dev.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
TCP 3-way handshake count of segments:
**Solution.** 3 (SYN, SYN+ACK, ACK).

### Q2. (GATE CSE 2014)
UDP header size:
**Solution.** 8 bytes.

### Q3. (GATE CSE 2018)
Slow start cwnd at RTT n:
**Solution.** 2^n MSS until ssthresh.

### Q4. (GATE CSE 2008)
Fast retransmit triggered by:
**Solution.** 3 duplicate ACKs.

### Q5. (GATE CSE 2010)
Effective window:
**Solution.** min(cwnd, rwnd).

### Q6. (GATE CSE 2015)
TCP Reno added:
**Solution.** Fast retransmit + fast recovery.

### Q7. (GATE CSE 2013)
Nagle's algorithm purpose:
**Solution.** Reduce small segment overhead.

### Q8. (GATE CSE 2007)
Initial cwnd in slow start:
**Solution.** 1 MSS.

### Q9. (GATE CSE 2003)
Timeout effect on cwnd:
**Solution.** ssthresh = cwnd/2; cwnd = 1; slow start.

### Q10. (GATE CSE 2009)
Throughput = ?
**Solution.** Window / RTT.

### Q11. (GATE CSE 2019)
TCP vs UDP for streaming:
**Solution.** UDP (lower latency).

### Q12. (GATE CSE 2020)
Connection state diagram:
**Solution.** SYN_SENT, ESTABLISHED, FIN_WAIT, etc.

### Q13. (GATE CSE 2021)
3-way handshake SYN+ACK from server:
**Solution.** Acknowledges client's SYN.

### Q14. (GATE CSE 2016)
RTT estimation formula:
**Solution.** EstimatedRTT = (1−α)·prev + α·SampleRTT.

### Q15. (GATE CSE 2011)
Congestion avoidance phase cwnd growth:
**Solution.** Linear (1 MSS per RTT).

---

## 6. Practice Questions (20+)

### Easy

**P1.** TCP vs UDP key difference.

**P2.** UDP header size.

**P3.** TCP connection setup.

**P4.** Slow start growth.

**P5.** Congestion avoidance growth.

**P6.** Effective window formula.

**P7.** RTO formula.

**P8.** Fast retransmit trigger.

**P9.** Nagle's algorithm.

**P10.** Port number range.

### Medium

**P11.** Trace slow start with ssthresh = 8 MSS.

**P12.** Compute throughput for 64 KB window, 100 ms RTT.

**P13.** Apply TCP Reno on loss event.

**P14.** Identify TCP flags in handshake.

**P15.** UDP use case examples.

**P16.** Compute timeout from samples.

**P17.** TCP termination flow.

**P18.** Distinguish flow vs congestion control.

**P19.** Compute time to send 100 KB.

**P20.** Effect of duplicate ACKs.

### Hard

**P21.** Detailed TCP state diagram.

**P22.** Implement sliding window.

**P23.** Compare TCP variants.

**P24.** Analyze BDP-window relation.

**P25.** Detect congestion via metrics.

**P26.** Apply BBR principles.

**P27.** Optimize TCP for high BDP networks.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | reliable vs not | direct |
| P2 | 8 B | direct |
| P3 | 3-way handshake | direct |
| P4 | exponential | direct |
| P5 | linear | direct |
| P6 | min(cwnd, rwnd) | direct |
| P7 | EstimatedRTT + 4·DevRTT | direct |
| P8 | 3 dup ACKs | direct |
| P9 | reduce small segments | direct |
| P10 | 0–65535 | direct |
| P11 | trace | direct |
| P12 | 64KB / 100ms = 640 KB/s | direct |
| P13 | ssthresh = cwnd/2; cwnd = ssthresh | direct |
| P14 | SYN, ACK | direct |
| P15 | DNS, video | direct |
| P16 | apply EWMA formula | direct |
| P17 | FIN/ACK pairs | direct |
| P18 | end-to-end vs network | direct |
| P19 | depends on cwnd | direct |
| P20 | trigger fast retransmit | direct |
| P21 | full state machine | direct |
| P22 | track unACKed | direct |
| P23 | algorithms differ | direct |
| P24 | window ≥ BDP | direct |
| P25 | RTT increase, drops | direct |
| P26 | bandwidth + RTT | direct |
| P27 | scale window | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | UDP reliable | It's not. |
| 2 | TCP unordered | TCP ensures order. |
| 3 | Slow start linear | It's exponential. |
| 4 | Congestion avoidance exponential | Linear. |
| 5 | Nagle's prevents large packets | Prevents small. |
| 6 | Effective window = cwnd always | min with rwnd. |
| 7 | UDP has 20 B header | 8 B. |
| 8 | TCP Reno = Tahoe | Adds fast recovery. |
| 9 | RTO constant | Adapts to RTT samples. |
| 10 | Port 80 = HTTPS | 80 is HTTP. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "TCP handshake" | 3-way SYN/SYN+ACK/ACK. |
| "Reliable transport" | TCP. |
| "Low latency / streaming" | UDP. |
| "Slow start" | Exponential cwnd. |
| "Congestion avoidance" | Linear cwnd. |
| "Fast retransmit" | 3 dup ACKs. |
| "Window-based throughput" | window / RTT. |
| "Effective window" | min(cwnd, rwnd). |
| "Timeout estimation" | EWMA on RTT. |
| "Nagle's algorithm" | Small segment optimization. |

---

## 9. Quick Revision

```
TRANSPORT LAYER: end-to-end + mux/demux

PORTS: 16-bit; well-known 0-1023

UDP
 8 B header
 connectionless / unreliable
 DNS, DHCP, streaming

TCP
 20+ B header
 connection-oriented / reliable / ordered

3-WAY HANDSHAKE: SYN, SYN+ACK, ACK
4-WAY TERMINATION: FIN/ACK pairs

FLAGS: URG, ACK, PSH, RST, SYN, FIN

RELIABILITY: seq + ACK + retransmit + checksum

SLIDING WINDOW
 effective = min(cwnd, rwnd)

CONGESTION CONTROL
 slow start: cwnd doubles
 congestion avoidance: cwnd += 1 MSS / RTT
 timeout: ssthresh = cwnd/2; cwnd = 1; slow start
 3 dup ACKs: ssthresh = cwnd/2; cwnd = ssthresh; fast retransmit/recovery

TCP VARIANTS: Tahoe, Reno, NewReno, Vegas, Cubic, BBR

RTT/RTO
 EstRTT = (1−α)·EstRTT + α·Sample
 DevRTT = (1−β)·DevRTT + β·|Sample − Est|
 RTO = EstRTT + 4·DevRTT

NAGLE'S ALG: avoid small segments

THROUGHPUT = window / RTT
```
