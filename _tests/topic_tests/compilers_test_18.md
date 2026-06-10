# Topic Test 18 — Compilers (Runtime/Codegen · Optimization & Data-Flow)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Activation record is stored on:
(A) Heap  (B) Stack  (C) Static  (D) Text

**Q2.** [MCQ] Heap allocation is:
(A) Compile-time  (B) LIFO  (C) Dynamic  (D) Read-only

**Q3.** [MCQ] Call-by-reference passes:
(A) Value  (B) Address  (C) Copy  (D) Textual substitution

**Q4.** [MCQ] Call-by-name uses:
(A) Lazy textual substitution  (B) Value copy  (C) Reference  (D) Memoization

**Q5.** [MCQ] Basic block has:
(A) Multiple entries  (B) Single entry/exit  (C) Multiple exits  (D) Loops only

**Q6.** [MCQ] Register allocation is modeled as:
(A) MST  (B) Graph coloring  (C) Bipartite matching  (D) Flow

**Q7.** [MCQ] Spilling means:
(A) Free register  (B) Move register value to memory  (C) Remove instruction  (D) Inline call

**Q8.** [MCQ] Peephole optimization works on:
(A) Whole program  (B) Functions  (C) Small windows of code  (D) Basic blocks

**Q9.** [MCQ] Internal fragmentation is:
(A) Wasted within block  (B) Gap between blocks  (C) Heap-only  (D) Stack-only

**Q10.** [MCQ] Reaching definitions analysis is:
(A) Forward + ∪  (B) Backward + ∪  (C) Forward + ∩  (D) Backward + ∩

**Q11.** [MCQ] Live variables analysis is:
(A) Forward + ∪  (B) Backward + ∪  (C) Forward + ∩  (D) Backward + ∩

**Q12.** [MCQ] Available expressions analysis is:
(A) Forward + ∪  (B) Backward + ∪  (C) Forward + ∩  (D) Backward + ∩

**Q13.** [MCQ] CSE optimization uses:
(A) Reaching defs  (B) Live vars  (C) Available expressions  (D) Very busy

**Q14.** [MCQ] DCE optimization uses:
(A) Reaching defs  (B) Live vars  (C) Available expressions  (D) Very busy

**Q15.** [MCQ] SSA φ-function placed at:
(A) Function entry  (B) Loop body  (C) Control-flow merges  (D) Function exit

---

## Section B — 2 marks each

**Q16.** [MCQ] Pick the heap GC method that handles cycles:
(A) Reference counting  (B) Mark-sweep  (C) Direct  (D) Compile-time

**Q17.** [MCQ] In `swap(a, a)` with call-by-reference:
(A) Swaps a with itself  (B) Crashes  (C) Modifies a  (D) Same as call-by-value

**Q18.** [NAT] Strength reduction: replace `i * 16` with `i << ____`

**Q19.** [MCQ] Loop-invariant code motion:
(A) Move into loop  (B) Move out of loop  (C) Replicate inside  (D) Delete

**Q20.** [MCQ] Forward + Intersection analysis identifies:
(A) Reaching definitions  (B) Live variables  (C) Available expressions  (D) Constants only

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | direct |
| 2 | (C) | direct |
| 3 | (B) | direct |
| 4 | (A) | direct |
| 5 | (B) | direct |
| 6 | (B) | direct |
| 7 | (B) | direct |
| 8 | (C) | direct |
| 9 | (A) | direct |
| 10 | (A) | direct |
| 11 | (B) | direct |
| 12 | (C) | direct |
| 13 | (C) | direct |
| 14 | (B) | direct |
| 15 | (C) | direct |
| 16 | (B) | mark-sweep handles cycles |
| 17 | (A) | direct |
| 18 | 4 | 2⁴=16 |
| 19 | (B) | direct |
| 20 | (C) | direct |

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
