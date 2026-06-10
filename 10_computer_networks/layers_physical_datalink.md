# Layered Model, Physical & Data Link Layer

> Subject: Computer Networks
> GATE weight: **2–4 marks** every year. OSI/TCP-IP layers, framing, error detection, flow/error control, ARQ.

---

## 1. Concept Explanation

### 1.1 Why Layers?

Networking is complex; layering breaks it into manageable pieces. Each layer:
- Provides services to layer above.
- Uses services from layer below.
- Has well-defined interfaces.

### 1.2 OSI Model (7 Layers)

| # | Layer | Function |
|---|---|---|
| 7 | Application | User-facing protocols (HTTP, FTP, SMTP) |
| 6 | Presentation | Encoding/encryption (TLS, JPEG) |
| 5 | Session | Manages sessions, dialog control |
| 4 | Transport | End-to-end (TCP, UDP) |
| 3 | Network | Routing (IP, ICMP) |
| 2 | Data Link | Frames, MAC (Ethernet, ARP) |
| 1 | Physical | Bits, signaling, hardware |

### 1.3 TCP/IP Model (5/4 Layers)

| # | Layer | OSI Equivalent |
|---|---|---|
| 5 | Application | 5-7 |
| 4 | Transport | 4 |
| 3 | Network (Internet) | 3 |
| 2 | Data Link / Network Access | 2 |
| 1 | Physical | 1 |

### 1.4 Encapsulation

Each layer adds a header (and possibly trailer) to data.

```
Application: data
Transport:   [TCP hdr | data]
Network:     [IP hdr | TCP hdr | data]
Data Link:   [Frame hdr | IP hdr | TCP hdr | data | Frame trailer]
Physical:    bits
```

### 1.5 PDU (Protocol Data Unit)

| Layer | PDU |
|---|---|
| Application | Message |
| Transport | Segment (TCP) / Datagram (UDP) |
| Network | Packet / Datagram |
| Data Link | Frame |
| Physical | Bits |

### 1.6 Physical Layer

Concerns:
- **Signal encoding:** NRZ, Manchester, Differential.
- **Modulation:** AM, FM, PSK, FSK, QAM.
- **Multiplexing:** TDM, FDM, WDM, CDMA.
- **Transmission media:** twisted pair, coax, fiber, wireless.
- **Bandwidth, throughput, latency.**

### 1.7 Encoding Schemes

| Scheme | Description |
|---|---|
| **NRZ** | High = 1, Low = 0; no clock recovery |
| **NRZI** | Transition = 1, no transition = 0 |
| **Manchester** | Mid-bit transition; clock embedded |
| **Differential Manchester** | Transition only when bit = 0 |
| **4B/5B** | 4 bits → 5 bits to ensure transitions |

### 1.8 Multiplexing

| Type | Description |
|---|---|
| **TDM (Time Division)** | Each user gets time slot |
| **FDM (Frequency Division)** | Each user gets frequency band |
| **WDM (Wavelength Division)** | Optical fiber |
| **CDMA (Code Division)** | Each user has unique code |

### 1.9 Transmission Modes

| Mode | Description |
|---|---|
| **Simplex** | One direction only |
| **Half-duplex** | Both directions, not simultaneous |
| **Full-duplex** | Both directions simultaneous |

### 1.10 Bandwidth, Throughput, Latency

| Term | Definition |
|---|---|
| **Bandwidth** | Max data rate (bps) |
| **Throughput** | Actual data rate |
| **Latency / Delay** | Time for data to cross network |

**Components of latency:**
- Propagation delay = distance / signal speed.
- Transmission delay = packet size / bandwidth.
- Queuing delay.
- Processing delay.

### 1.11 Bandwidth-Delay Product (BDP)

`BDP = bandwidth × RTT`

Represents data "in flight"; determines optimal window sizes.

### 1.12 Data Link Layer Functions

- **Framing:** divide bit stream into frames.
- **Error detection / correction.**
- **Flow control.**
- **Medium access control (MAC):** in shared media.

### 1.13 Framing Methods

| Method | Description |
|---|---|
| **Character count** | Length field |
| **Byte stuffing** | Special start/end bytes; escape character |
| **Bit stuffing** | Special bit pattern; insert 0 after k 1's |
| **Physical layer coding violations** | Use illegal signal as delimiter |

### 1.14 Error Detection

| Method | Description |
|---|---|
| **Parity** | Single bit; detect 1-bit error |
| **Two-dimensional parity** | Multi-bit detection + correction |
| **Checksum** | Modular sum (used in Internet protocols) |
| **CRC (Cyclic Redundancy Check)** | Polynomial division; very effective |

### 1.15 CRC

Treat data as polynomial. Use generator polynomial G(x).
- Append n zeros to data (n = degree of G).
- Compute remainder of division by G.
- Append remainder.

Receiver checks: divide received by G; remainder should be 0.

**Detects:** all single-bit errors, double errors (if G has factor x+1), burst errors up to length n.

### 1.16 Hamming Code (Error Correction)

For n bits with k parity bits, can correct 1-bit error if `2^k ≥ n + k + 1`.

**Hamming(7,4):** 4 data + 3 parity bits; corrects 1-bit error.

### 1.17 Flow Control

Prevents sender from overwhelming receiver.

| Method | Description |
|---|---|
| **Stop-and-Wait** | Send 1 frame; wait for ACK |
| **Sliding Window** | Send up to window size; ACK individual frames |
| **Go-Back-N** | Retransmit from N on error |
| **Selective Repeat** | Retransmit only erroneous frames |

### 1.18 Stop-and-Wait Efficiency

`Efficiency = T_t / (T_t + 2·T_p)` = 1 / (1 + 2a)

Where:
- T_t = transmission time.
- T_p = propagation time.
- a = T_p / T_t.

For long links or small frames, efficiency ≈ 1/(1+2a) is poor.

### 1.19 Sliding Window Efficiency

For window size W:
`Efficiency = min(1, W / (1 + 2a))`

To fully utilize: W ≥ 1 + 2a.

### 1.20 Sequence Number Bits

For window size W:
- **Stop-and-Wait:** 1 bit.
- **Go-Back-N:** ≥ ⌈log₂(W+1)⌉ bits; window ≤ 2^k − 1.
- **Selective Repeat:** ≥ ⌈log₂(2W)⌉ bits; window ≤ 2^(k−1).

### 1.21 Error Control via ARQ

| Type | Description |
|---|---|
| **Stop-and-Wait ARQ** | Retransmit on timeout |
| **Go-Back-N ARQ** | NAK or timeout → retransmit from lost |
| **Selective Repeat ARQ** | Retransmit only specific |

### 1.22 Piggybacking

ACK piggybacks on outgoing data frame to save bandwidth.

### 1.23 HDLC Frame Format

```
| Flag | Address | Control | Data | FCS | Flag |
```

Used in WAN.

### 1.24 PPP (Point-to-Point Protocol)

Common WAN protocol with HDLC-like framing + LCP / NCP.

> **Summary:** OSI = 7 layers. Each layer adds header. Physical: signaling. Data link: framing, error detection (parity/CRC/Hamming), flow control (stop-wait, sliding window). Stop-and-wait efficiency = 1/(1+2a). Sliding window: utilize via W ≥ 1+2a.

---

## 2. Important Points

- **OSI 7 layers; TCP/IP 5 (or 4)** layers.
- **Encapsulation** at each layer.
- **PDU naming:** segment / packet / frame / bits.
- **NRZ:** simple but no clock recovery.
- **Manchester:** clock embedded.
- **TDM** = time slots; **FDM** = frequency bands.
- **Bandwidth-Delay Product** = data in flight.
- **CRC** detects burst errors effectively.
- **Hamming** corrects 1-bit error.
- **Stop-and-wait efficiency:** 1/(1+2a).
- **Sliding window:** W frames in flight.
- **Go-Back-N** retransmits from error frame; **Selective Repeat** retransmits specific.
- **GBN window ≤ 2^k − 1; SR window ≤ 2^(k−1).**
- **Piggybacking** combines ACK with data.

---

## 3. Short Notes

```
OSI MODEL (7 layers)
 7 application
 6 presentation
 5 session
 4 transport
 3 network
 2 data link
 1 physical

TCP/IP (5)
 application / transport / network / data link / physical

PDU
 message / segment / packet / frame / bits

ENCODING
 NRZ, NRZI, Manchester, Differential Manchester, 4B/5B

MULTIPLEXING
 TDM, FDM, WDM, CDMA

TRANSMISSION MODES
 simplex / half-duplex / full-duplex

DELAY
 propagation = distance / speed
 transmission = packet / bandwidth
 + queuing + processing

BDP = bandwidth × RTT

DATA LINK FUNCTIONS
 framing / error / flow / MAC

FRAMING
 character count / byte stuff / bit stuff / coding violations

ERROR DETECTION
 parity / 2D parity / checksum / CRC

CRC
 polynomial division
 burst errors detected

HAMMING (n,k): correct 1-bit error if 2^k ≥ n+k+1

FLOW CONTROL
 stop-and-wait / sliding window / GBN / SR

STOP-AND-WAIT
 efficiency = 1 / (1 + 2a)
 a = T_p / T_t

SLIDING WINDOW
 efficiency = min(1, W/(1+2a))
 W ≥ 1+2a for full utilization

SEQ # BITS
 GBN: W ≤ 2^k − 1
 SR: W ≤ 2^(k−1)

PIGGYBACKING: ACK on data

HDLC: standard frame format
PPP: WAN
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | OSI 7 layers in order | ✅✅✅ |
| 2 | TCP/IP 5 layers | ✅✅ |
| 3 | Stop-and-wait efficiency = 1/(1+2a) | ✅✅✅ |
| 4 | Sliding window efficiency: W/(1+2a) | ✅✅ |
| 5 | GBN window: 2^k − 1 | ✅✅ |
| 6 | SR window: 2^(k−1) | ✅✅ |
| 7 | BDP = BW × RTT | ✅✅ |
| 8 | Propagation = distance / speed | ✅ |
| 9 | Transmission = packet / bandwidth | ✅ |
| 10 | Hamming: 2^k ≥ n+k+1 | ✅ |
| 11 | CRC for burst error detection | ✅ |
| 12 | Manchester encoding embeds clock | ✅ |
| 13 | TDM time, FDM frequency | ✅ |

### Tricks

- **For S&W efficiency:** compute a = T_p / T_t first.
- **For sliding window utilization:** W ≥ 1 + 2a.
- **For sequence # bits:** use formula based on window protocol.
- **For BDP:** convert all to consistent units (bits, seconds).
- **CRC always assumed to detect burst ≤ degree.**

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Number of OSI layers:
**Solution.** 7.

### Q2. (GATE CSE 2014)
Bandwidth-delay product:
**Solution.** Bandwidth × RTT (or one-way delay sometimes).

### Q3. (GATE CSE 2018)
Stop-and-wait efficiency for a = 1:
**Solution.** 1/(1 + 2·1) = 1/3.

### Q4. (GATE CSE 2008)
GBN window for 3-bit sequence number:
**Solution.** Max window = 2³ − 1 = 7.

### Q5. (GATE CSE 2010)
SR window for 4-bit sequence number:
**Solution.** Max window = 2⁴⁻¹ = 8.

### Q6. (GATE CSE 2015)
Hamming(7,4) corrects:
**Solution.** 1-bit error.

### Q7. (GATE CSE 2013)
Manchester encoding:
**Solution.** Embeds clock via mid-bit transition.

### Q8. (GATE CSE 2007)
Bit stuffing pattern:
**Solution.** Insert 0 after k consecutive 1's (e.g., 5 in HDLC).

### Q9. (GATE CSE 2003)
PDU at network layer:
**Solution.** Packet (datagram).

### Q10. (GATE CSE 2009)
Sliding window full utilization:
**Solution.** W ≥ 1 + 2a.

### Q11. (GATE CSE 2019)
TDM vs FDM:
**Solution.** Time slots vs frequency bands.

### Q12. (GATE CSE 2020)
Layer 4 in OSI:
**Solution.** Transport.

### Q13. (GATE CSE 2021)
CRC generator polynomial degree n detects:
**Solution.** Burst errors of length ≤ n.

### Q14. (GATE CSE 2016)
Stop-and-wait with bandwidth 1 Mbps, propagation 1 ms, frame 1000 bits. Efficiency?
**Solution.** T_t = 1 ms; T_p = 1 ms; a = 1; eff = 1/3.

### Q15. (GATE CSE 2011)
Selective Repeat advantage over GBN:
**Solution.** Retransmits only erroneous frames.

---

## 6. Practice Questions (20+)

### Easy

**P1.** OSI layer 1 name.

**P2.** OSI layer 7 name.

**P3.** PDU at data link.

**P4.** Define bandwidth.

**P5.** Define BDP.

**P6.** TDM vs FDM.

**P7.** Stop-and-wait efficiency formula.

**P8.** Sliding window protocol types.

**P9.** GBN sequence number constraint.

**P10.** SR sequence number constraint.

### Medium

**P11.** Compute S&W efficiency for BW=10 Mbps, distance=1000km, speed=2×10⁸ m/s, frame=1000 bits.

**P12.** Compute sliding window efficiency for W=8, a=2.

**P13.** Required W for 1+2a utilization.

**P14.** Bit stuff data 011111011110.

**P15.** Apply CRC for given data and generator.

**P16.** Hamming code: detect/correct error.

**P17.** Compute BDP for 100 Mbps, 50 ms RTT.

**P18.** Frame pdU sizes through layers.

**P19.** Manchester vs NRZ trade-off.

**P20.** Transmission mode for radio call.

### Hard

**P21.** Apply CRC step-by-step for given data and CRC-8.

**P22.** Simulate GBN with errors.

**P23.** Simulate SR with errors.

**P24.** Compute sequence number bits for given window.

**P25.** Calculate optimal window for given BDP.

**P26.** Compare TDM vs CDMA capacity.

**P27.** Diagnose layer responsible for given problem.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | physical | direct |
| P2 | application | direct |
| P3 | frame | direct |
| P4 | max data rate | direct |
| P5 | BW × RTT | direct |
| P6 | time vs frequency | direct |
| P7 | 1/(1+2a) | direct |
| P8 | S&W, GBN, SR | direct |
| P9 | 2^k − 1 | direct |
| P10 | 2^(k−1) | direct |
| P11 | T_t = 1000/10⁷ = 0.1 ms; T_p = 5 ms; a = 50; eff ≈ 0.0099 | direct |
| P12 | min(1, 8/5) = 1 | direct |
| P13 | W ≥ 1 + 2a | direct |
| P14 | insert 0 after 5 1's | direct |
| P15 | trace polynomial division | direct |
| P16 | parity check | direct |
| P17 | 5 Mb in flight | direct |
| P18 | header added at each layer | direct |
| P19 | clock embedded vs simpler | direct |
| P20 | half-duplex (walkie-talkie) | direct |
| P21 | trace | direct |
| P22 | trace | direct |
| P23 | trace | direct |
| P24 | log₂ formula | direct |
| P25 | match BDP | direct |
| P26 | sum vs interference | direct |
| P27 | analysis | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | OSI = TCP/IP | Different layers. |
| 2 | Layer 5/6/7 in TCP/IP separated | Combined as application. |
| 3 | Stop-and-wait efficient | Only if a small. |
| 4 | GBN window = 2^k | Should be 2^k − 1. |
| 5 | SR window = 2^k − 1 | Should be 2^(k−1). |
| 6 | Manchester = NRZ | Different. |
| 7 | CRC corrects errors | Detects only. |
| 8 | Hamming detects 2-bit | Only corrects 1-bit; detects 2-bit. |
| 9 | TDM = FDM | Different. |
| 10 | Latency = bandwidth | Different metrics. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Which layer does X" | OSI 7-layer matrix. |
| "Stop-and-wait efficiency" | 1/(1+2a). |
| "Sliding window utilization" | W/(1+2a). |
| "Window size for k-bit seq#" | GBN 2^k−1; SR 2^(k−1). |
| "BDP" | BW × RTT. |
| "Encoding scheme" | Manchester / NRZ / 4B5B. |
| "Multiplexing" | TDM / FDM / CDMA. |
| "Error detection" | Parity / Checksum / CRC. |
| "Error correction" | Hamming. |
| "PDU" | Layer-specific name. |

---

## 9. Quick Revision

```
OSI 7 LAYERS (top → bottom)
 application / presentation / session /
 transport / network / data link / physical

TCP/IP 5 layers: combine top 3 → application

PDU: message / segment / packet / frame / bits

ENCODING
 NRZ, NRZI, Manchester (clock), Differential, 4B/5B

MULTIPLEXING: TDM / FDM / WDM / CDMA

DELAY: propagation + transmission + queuing + processing
 BDP = BW × RTT

DATA LINK
 framing: char count / byte stuff / bit stuff / coding violation
 error: parity / checksum / CRC
 correction: Hamming
 flow: stop-and-wait / sliding window
 ARQ: GBN, SR

EFFICIENCY
 S&W: 1/(1+2a) where a = T_p/T_t
 sliding window: min(1, W/(1+2a))
 W ≥ 1+2a for full

SEQ #
 GBN: W ≤ 2^k − 1
 SR: W ≤ 2^(k−1)

PIGGYBACKING

HDLC, PPP
```
