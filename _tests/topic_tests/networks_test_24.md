# Topic Test 24 — Networks (Network · Transport · Application & Security)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] IPv4 address bits:
(A) 16  (B) 32  (C) 64  (D) 128

**Q2.** [NAT] # hosts per /28 = `____`

**Q3.** [MCQ] RIP routing algorithm:
(A) Distance vector  (B) Link state  (C) Path vector  (D) Static

**Q4.** [MCQ] OSPF routing algorithm:
(A) Distance vector  (B) Link state  (C) Path vector  (D) Static

**Q5.** [MCQ] BGP routing algorithm:
(A) Distance vector  (B) Link state  (C) Path vector  (D) Static

**Q6.** [MCQ] ICMP traceroute uses:
(A) Echo  (B) Time exceeded  (C) Dest unreachable  (D) Redirect

**Q7.** [MCQ] TCP 3-way handshake:
(A) SYN, ACK, ACK  (B) SYN, SYN+ACK, ACK  (C) ACK, SYN, FIN  (D) SYN, ACK

**Q8.** [MCQ] UDP header size:
(A) 8 bytes  (B) 12 bytes  (C) 20 bytes  (D) 24 bytes

**Q9.** [MCQ] Slow start cwnd growth:
(A) Linear  (B) Exponential  (C) Constant  (D) Logarithmic

**Q10.** [MCQ] Congestion avoidance cwnd:
(A) Linear  (B) Exponential  (C) Constant  (D) Logarithmic

**Q11.** [MCQ] HTTPS port:
(A) 80  (B) 443  (C) 8080  (D) 22

**Q12.** [MCQ] DNS port:
(A) 22  (B) 53  (C) 80  (D) 443

**Q13.** [MCQ] HTTP method to read:
(A) POST  (B) PUT  (C) GET  (D) DELETE

**Q14.** [MCQ] HTTP status 404:
(A) Server error  (B) Not found  (C) Redirect  (D) Success

**Q15.** [MCQ] TLS provides:
(A) Routing  (B) Confidentiality + integrity + auth  (C) DNS  (D) NAT

---

## Section B — 2 marks each

**Q16.** [NAT] Min frame size for 1 Gbps Ethernet, 200 m segment, signal speed 2×10⁸ m/s = `____` bits

**Q17.** [MCQ] Subnet 192.168.1.0/24 split into /27. # subnets and hosts/subnet:
(A) 4 subnets, 62 hosts  (B) 8 subnets, 30 hosts  (C) 16 subnets, 14 hosts  (D) 2 subnets, 126 hosts

**Q18.** [MCQ] TCP fast retransmit:
(A) After timeout  (B) After 3 duplicate ACKs  (C) After 1 ACK  (D) After RTT

**Q19.** [MCQ] Effective TCP throughput formula:
(A) cwnd × RTT  (B) min(cwnd, rwnd) / RTT  (C) RTT / cwnd  (D) cwnd × MSS

**Q20.** [MCQ] DDoS attack:
(A) Single attacker  (B) Multiple attackers overwhelm target  (C) DNS only  (D) IP-based

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) 32 | direct |
| 2 | 14 | 2^4 − 2 |
| 3 | (A) | direct |
| 4 | (B) | direct |
| 5 | (C) | direct |
| 6 | (B) | direct |
| 7 | (B) | direct |
| 8 | (A) | direct |
| 9 | (B) | direct |
| 10 | (A) | direct |
| 11 | (B) | direct |
| 12 | (B) | direct |
| 13 | (C) | direct |
| 14 | (B) | direct |
| 15 | (B) | direct |
| 16 | 2000 | 2 × 10⁹ × (200/2×10⁸) = 2 × 10⁹ × 10⁻⁶ |
| 17 | (B) 8 subnets, 30 hosts | direct |
| 18 | (B) | direct |
| 19 | (B) | direct |
| 20 | (B) | direct |

---

## Score Sheet

| | Score |
|---|---|
| Section A (15 × 1) | _ /15 |
| Section B (5 × 2)  | _ /10 |
| **Total**          | _ /25 |
| Time used          | _ min |

**Targets:**
- ≥ 22/25 in 25 min → mastery
- 18–21 → revise short notes + pattern recognition
- < 18 → re-do PYQs of all three topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
