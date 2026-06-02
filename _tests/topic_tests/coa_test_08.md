# Topic Test 08 — COA (Machine Instructions & Addressing · ALU/Datapath/Control)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Postfix of `(A + B) * (C − D)`:
(A) AB+CD−*  (B) AB+*CD−  (C) +AB*−CD  (D) ABCD+−*

**Q2.** [MCQ] # memory accesses in indirect addressing for an operand:
(A) 0  (B) 1  (C) 2  (D) 3

**Q3.** [MCQ] # of bits to specify a register in a 32-register file:
(A) 4  (B) 5  (C) 6  (D) 32

**Q4.** [NAT] An ISA supports 200 instructions. Min opcode bits = `____`

**Q5.** [MCQ] RISC processors typically use:
(A) Fixed-length instructions  (B) Variable-length  (C) Both equally  (D) Neither

**Q6.** [MCQ] PC-relative addressing supports:
(A) Self-modifying code  (B) Position-independent code  (C) Direct memory  (D) Indirect memory

**Q7.** [NAT] In a little-endian system, 4-byte word `0xAABBCCDD` stored at address 0. Byte at address 0 = `0x____`

**Q8.** [MCQ] Stack-based machines use:
(A) 0-address  (B) 1-address  (C) 2-address  (D) 3-address

**Q9.** [MCQ] CPU time formula:
(A) N + CPI + T  (B) N · CPI · T  (C) N / (CPI · T)  (D) CPI / N

**Q10.** [MCQ] Average CPI: 50% ALU(1), 30% Load(2), 20% Branch(3):
(A) 1.5  (B) 1.7  (C) 2.0  (D) 1.6

**Q11.** [MCQ] Amdahl's law: 80% parallelizable, infinite cores. Max speedup?
(A) 2  (B) 5  (C) 10  (D) ∞

**Q12.** [MCQ] Hardwired control is:
(A) Slower than microprogrammed  (B) Faster but less flexible  (C) Always cheaper  (D) Variable speed

**Q13.** [MCQ] Booth's algorithm handles:
(A) Signed multiplication  (B) Unsigned multiplication  (C) Floating-point  (D) Division

**Q14.** [NAT] CPU at 2 GHz, CPI=2.5, executes 10⁹ instructions. Time = `____` seconds

**Q15.** [MCQ] Single-cycle CPU clock period equals:
(A) Sum of stage delays  (B) Longest instruction's delay  (C) Average delay  (D) Shortest delay

---

## Section B — 2 marks each

**Q16.** [MCQ] Postfix evaluation `7 8 + 3 *` = ?
(A) 21  (B) 30  (C) 45  (D) 24

**Q17.** [MCQ] A computer has 4 GB byte-addressable memory. # address lines?
(A) 16  (B) 24  (C) 32  (D) 64

**Q18.** [NAT] Microprogram with 256 instructions × 24 bits each. Control memory = `____` bits

**Q19.** [MCQ] Speedup if 70% of program is sped up by 2x (Amdahl):
(A) 1.43  (B) 1.54  (C) 1.67  (D) 2.00

**Q20.** [MCQ] CPU-A: 500 MHz, CPI=1.5; CPU-B: 1 GHz, CPI=4. For same N instructions, faster?
(A) A by 4×  (B) B by 1.33×  (C) A by 1.33×  (D) Equal

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (A) | precedence |
| 2 | (C) 2 | indirect |
| 3 | (B) 5 | log₂ 32 |
| 4 | 8 | ⌈log₂ 200⌉ |
| 5 | (A) | RISC |
| 6 | (B) | PC-rel |
| 7 | DD | LSB at low addr |
| 8 | (A) | stack machine |
| 9 | (B) | direct |
| 10 | (B) 1.7 | 0.5+0.6+0.6 |
| 11 | (B) 5 | 1/0.2 |
| 12 | (B) | direct |
| 13 | (A) | signed |
| 14 | 1.25 | 10⁹ × 2.5 / 2×10⁹ |
| 15 | (B) | direct |
| 16 | (C) 45 | 7+8=15; 15·3=45 |
| 17 | (C) 32 | 4 GB = 2³² bytes |
| 18 | 6144 | 256·24 |
| 19 | (B) 1.54 | 1/(0.3 + 0.7/2) = 1/0.65 |
| 20 | (C) | A: T = 1.5/(0.5G) = 3 ns; B: 4/1G = 4 ns; A faster by 4/3 ≈ 1.33× |

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
