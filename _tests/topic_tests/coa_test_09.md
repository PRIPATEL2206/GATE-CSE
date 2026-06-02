# Topic Test 09 — COA (Pipelining · Memory Hierarchy · I/O & DMA)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] In a 5-stage pipeline, ideal cycles for 100 instructions:
(A) 100  (B) 104  (C) 105  (D) 500

**Q2.** [MCQ] Asymptotic speedup of k-stage pipeline:
(A) 1  (B) 2  (C) k  (D) k²

**Q3.** [MCQ] Load-use hazard penalty in classic MIPS:
(A) 0  (B) 1  (C) 2  (D) 3

**Q4.** [MCQ] WAW hazard occurs in:
(A) In-order pipelines  (B) Out-of-order  (C) Both  (D) Neither

**Q5.** [MCQ] Forwarding eliminates:
(A) All hazards  (B) Most RAW (not load-use)  (C) Branch hazards  (D) Structural hazards

**Q6.** [NAT] Speedup of pipelining for 1000 instructions in 5-stage = `____` (round to 2 decimals)

**Q7.** [MCQ] Cache: 16 KB, block 64 B. # of cache lines:
(A) 64  (B) 128  (C) 256  (D) 1024

**Q8.** [MCQ] EAT for hit rate 95%, t_h = 1 ns, t_m = 100 ns:
(A) 1 ns  (B) 5 ns  (C) 5.95 ns  (D) 6 ns

**Q9.** [MCQ] Belady's anomaly applies to:
(A) LRU  (B) FIFO  (C) Optimal  (D) LFU

**Q10.** [MCQ] Write-through with no-write-allocate is paired because:
(A) Reduces complexity  (B) Improves speed  (C) Requires dirty bit  (D) Avoids cache pollution

**Q11.** [NAT] # of tag bits for 32-bit address, cache 32 KB, 4-way SA, block 64 B = `____`

**Q12.** [MCQ] DMA mode that holds bus until done:
(A) Cycle-stealing  (B) Transparent  (C) Burst  (D) Round-robin

**Q13.** [MCQ] Memory-mapped I/O uses:
(A) Special IN/OUT instructions  (B) Standard load/store  (C) Both  (D) Neither

**Q14.** [MCQ] NMI is:
(A) Maskable  (B) Non-maskable  (C) Software-only  (D) Polled-only

**Q15.** [MCQ] Vectored interrupt:
(A) Polled scan  (B) Direct ISR address  (C) Daisy-chain  (D) Random

---

## Section B — 2 marks each

**Q16.** [MCQ] Pipeline 5-stage, 30% branches with 20% misprediction (penalty 2). Effective CPI?
(A) 1.0  (B) 1.12  (C) 1.20  (D) 1.40

**Q17.** [NAT] Two-level: L1 hit 90%, L1 = 1 ns, L2 hit 80%, L2 = 10 ns, main = 100 ns. EAT = `____` ns

**Q18.** [MCQ] Cache: 8 KB, 16 B blocks, 32-bit address. Direct-mapped. # bits for tag:
(A) 18  (B) 19  (C) 20  (D) 21

**Q19.** [MCQ] DMA transfer 1 GB at 200 MB/s plus 100 µs setup. Time?
(A) ≈ 5 s  (B) ≈ 5.0001 s  (C) ≈ 200 ms  (D) ≈ 1 s

**Q20.** [MCQ] In a daisy-chained interrupt system, priority is determined by:
(A) Software  (B) Position in chain  (C) Round-robin  (D) Random

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) 104 | N + k − 1 |
| 2 | (C) k | direct |
| 3 | (B) 1 | irreducible |
| 4 | (B) | OoO needs renaming |
| 5 | (B) | direct |
| 6 | 4.98 | 5000/1004 ≈ 4.98 |
| 7 | (C) 256 | 16K/64 |
| 8 | (C) 5.95 ns | 1 + 0.05·100 |
| 9 | (B) FIFO | direct |
| 10 | (A) | typical pairing |
| 11 | 19 | offset=6, sets=128, index=7, tag=32−6−7=19 |
| 12 | (C) Burst | direct |
| 13 | (B) | direct |
| 14 | (B) | direct |
| 15 | (B) | direct |
| 16 | (B) 1.12 | 1 + 0.3·0.2·2 = 1.12 |
| 17 | 4 | 1 + 0.1·(10 + 0.2·100) = 1 + 3 = 4 |
| 18 | (B) 19 | offset=4, sets=512, index=9, tag=32−4−9=19 |
| 19 | (A) ≈ 5 s | 1024 MB / 200 MB/s = 5.12 s + 100 µs ≈ 5.12 s |
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
