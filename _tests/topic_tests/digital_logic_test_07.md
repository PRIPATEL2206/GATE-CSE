# Topic Test 07 — Digital Logic (Combinational · Sequential · Minimization & Hazards)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Sum equation for a full adder is:
(A) A·B·Cin  (B) A⊕B⊕Cin  (C) A+B+Cin  (D) A·B+Cin

**Q2.** [MCQ] Number of select lines in a 32:1 MUX:
(A) 4  (B) 5  (C) 6  (D) 32

**Q3.** [MCQ] A 3-to-8 decoder has how many output lines?
(A) 3  (B) 6  (C) 8  (D) 9

**Q4.** [NAT] Number of 2:1 MUXes required to build a 16:1 MUX = `____`

**Q5.** [MCQ] D FF: Q(t) = 0, D = 1. Q(t+1) = ?
(A) 0  (B) 1  (C) Q  (D) Q'

**Q6.** [MCQ] T FF: T = 1, Q = 1. Q(t+1) = ?
(A) 0  (B) 1  (C) X  (D) Z

**Q7.** [MCQ] JK FF: J = K = 1. Behaves as:
(A) Hold  (B) Reset  (C) Set  (D) Toggle

**Q8.** [NAT] Minimum number of FFs for a mod-20 counter = `____`

**Q9.** [MCQ] Number of states in 5-bit Johnson counter:
(A) 5  (B) 10  (C) 16  (D) 32

**Q10.** [MCQ] Number of states in 5-bit ring counter:
(A) 5  (B) 10  (C) 16  (D) 32

**Q11.** [MCQ] Latch is:
(A) Edge-triggered  (B) Level-triggered  (C) Both  (D) Neither

**Q12.** [MCQ] Static-1 hazard is fixed by:
(A) Removing PI  (B) Adding redundant PI  (C) NAND conversion  (D) Decreasing fan-in

**Q13.** [MCQ] Mealy vs Moore output depends on:
(A) State only — Mealy  (B) Inputs only — Moore  (C) State and inputs — Mealy  (D) None

**Q14.** [MCQ] CLA delay for n-bit adder:
(A) O(n)  (B) O(log n)  (C) O(n²)  (D) O(1)

**Q15.** [MCQ] Quine-McCluskey is used for:
(A) Counting gates  (B) Boolean minimization  (C) FF design  (D) Memory mapping

---

## Section B — 2 marks each

**Q16.** [MCQ] A 4-bit ripple-carry adder using FAs each with 2 ns delay. Worst-case delay?
(A) 2 ns  (B) 4 ns  (C) 8 ns  (D) 16 ns

**Q17.** [MCQ] A 4-bit synchronous counter with T FFs counts 0 → 1 → 2 → … → 15. T₃ depends on:
(A) None  (B) Q₀  (C) Q₀Q₁  (D) Q₀Q₁Q₂

**Q18.** [NAT] # of EPIs of F(A,B,C,D) = Σm(0, 2, 5, 7, 8, 10, 13, 15) = `____`

**Q19.** [MCQ] Max clock frequency of a circuit with t_pd = 5, t_comb = 10, t_setup = 2 (all ns):
(A) 50 MHz  (B) 58.8 MHz  (C) 100 MHz  (D) 200 MHz

**Q20.** [MCQ] In an FSM detecting "11" using Mealy machine, minimum # of states:
(A) 1  (B) 2  (C) 3  (D) 4

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | direct |
| 2 | (B) 5 | log₂ 32 |
| 3 | (C) 8 | 2³ |
| 4 | 15 | 2ⁿ − 1 = 15 |
| 5 | (B) 1 | direct |
| 6 | (A) 0 | toggle |
| 7 | (D) Toggle | JK |
| 8 | 5 | ⌈log₂ 20⌉ |
| 9 | (B) 10 | 2n for Johnson |
| 10 | (A) 5 | n for ring |
| 11 | (B) | level-triggered |
| 12 | (B) | redundant PI |
| 13 | (C) Mealy | direct |
| 14 | (B) O(log n) | CLA |
| 15 | (B) | minimization |
| 16 | (C) 8 ns | 4·2 |
| 17 | (D) | T₃ = Q₀Q₁Q₂ |
| 18 | 2 | B'D' and BD |
| 19 | (B) 58.8 MHz | T = 5+10+2 = 17 ns; f = 1/17 ≈ 58.8 MHz |
| 20 | (B) 2 | Mealy needs only 2: idle and "saw 1" |

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
