# Topic Test 23 — Networks (Layers/Physical/Data Link · LAN/Switching/MAC)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Number of OSI layers:
(A) 4  (B) 5  (C) 6  (D) 7

**Q2.** [MCQ] OSI layer 4:
(A) Network  (B) Transport  (C) Session  (D) Application

**Q3.** [MCQ] PDU at network layer:
(A) Segment  (B) Packet  (C) Frame  (D) Bit

**Q4.** [MCQ] PDU at data link layer:
(A) Segment  (B) Packet  (C) Frame  (D) Bit

**Q5.** [MCQ] CRC is for:
(A) Encoding  (B) Encryption  (C) Error detection  (D) Routing

**Q6.** [MCQ] Manchester encoding:
(A) Embeds clock  (B) NRZ-like  (C) Better than NRZ for noise  (D) None

**Q7.** [MCQ] Stop-and-wait efficiency formula:
(A) 1/(1+a)  (B) 1/(1+2a)  (C) 1/(2+a)  (D) 1/2a

**Q8.** [MCQ] GBN max window for k-bit seq#:
(A) 2^k  (B) 2^k − 1  (C) 2^(k−1)  (D) 2^(k+1)

**Q9.** [MCQ] SR max window for k-bit seq#:
(A) 2^k  (B) 2^k − 1  (C) 2^(k−1)  (D) 2^(k+1)

**Q10.** [MCQ] MAC address bits:
(A) 32  (B) 48  (C) 64  (D) 128

**Q11.** [MCQ] Pure ALOHA max throughput:
(A) 18.4%  (B) 36.8%  (C) 50%  (D) 100%

**Q12.** [MCQ] Slotted ALOHA max throughput:
(A) 18.4%  (B) 36.8%  (C) 50%  (D) 63.2%

**Q13.** [MCQ] Switch operates at:
(A) Layer 1  (B) Layer 2  (C) Layer 3  (D) Layer 4

**Q14.** [MCQ] ARP maps:
(A) IP → port  (B) MAC → IP  (C) IP → MAC  (D) Hostname → IP

**Q15.** [MCQ] STP purpose:
(A) Encryption  (B) Loop prevention  (C) Routing  (D) ARP cache

---

## Section B — 2 marks each

**Q16.** [NAT] BDP for 100 Mbps and 50 ms RTT = `____` bits

**Q17.** [MCQ] Sliding window for full utilization (a = 4):
(A) 5  (B) 9  (C) 4  (D) 8

**Q18.** [MCQ] Min Ethernet frame for 1 Gbps, 200 m segment, signal speed 2×10⁸ m/s:
(A) 100 bits  (B) 200 bits  (C) 1000 bits  (D) 2000 bits

**Q19.** [MCQ] # collision domains for 8-port switch with 8 hosts:
(A) 1  (B) 4  (C) 8  (D) 16

**Q20.** [MCQ] Hamming code (n, k): correct 1-bit error if:
(A) n ≥ 2^k − k − 1  (B) 2^k ≥ n + k + 1  (C) k ≥ 2^n  (D) n + k ≥ 2

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (D) | direct |
| 2 | (B) | direct |
| 3 | (B) | direct |
| 4 | (C) | direct |
| 5 | (C) | direct |
| 6 | (A) | direct |
| 7 | (B) | direct |
| 8 | (B) | direct |
| 9 | (C) | direct |
| 10 | (B) | direct |
| 11 | (A) | direct |
| 12 | (B) | direct |
| 13 | (B) | direct |
| 14 | (C) | direct |
| 15 | (B) | direct |
| 16 | 5000000 (5 Mb) | 100·10⁶ × 0.05 |
| 17 | (B) 9 | W = 1+2a = 9 |
| 18 | (D) 2000 bits | 2·10⁹ × 10⁻⁶ |
| 19 | (C) 8 | 1 per port |
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
- < 18 → re-do PYQs of both topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
