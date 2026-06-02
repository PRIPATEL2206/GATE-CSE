# Topic Test 12 — Algorithms (Asymptotics & Recurrences · Searching/Sorting/Selection)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] T(n) = 2T(n/2) + n is:
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(2ⁿ)

**Q2.** [MCQ] T(n) = T(n−1) + 1:
(A) Θ(log n)  (B) Θ(n)  (C) Θ(n log n)  (D) Θ(n²)

**Q3.** [MCQ] Tower of Hanoi:
(A) Θ(n)  (B) Θ(n²)  (C) Θ(n log n)  (D) Θ(2ⁿ)

**Q4.** [MCQ] Big-O upper bound notation:
(A) ≥  (B) ≤  (C) =  (D) <

**Q5.** [NAT] log₂ 1024 = `____`

**Q6.** [MCQ] Comparison sort lower bound:
(A) Ω(n)  (B) Ω(log n)  (C) Ω(n log n)  (D) Ω(n²)

**Q7.** [MCQ] Worst case of quicksort:
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(2ⁿ)

**Q8.** [MCQ] Best case of insertion sort:
(A) O(1)  (B) O(n)  (C) O(n log n)  (D) O(n²)

**Q9.** [MCQ] Mergesort in-place?
(A) Yes  (B) No  (C) Only with extra trick  (D) Depends on input

**Q10.** [MCQ] Counting sort time:
(A) O(n)  (B) O(n+k)  (C) O(n log n)  (D) O(k)

**Q11.** [MCQ] Stable sort: pick one:
(A) Quick  (B) Heap  (C) Selection  (D) Merge

**Q12.** [MCQ] In-place: pick one:
(A) Merge  (B) Counting  (C) Heap  (D) Radix

**Q13.** [MCQ] Binary search on n elements:
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q14.** [NAT] Find min comparisons for binary search worst case on 64 elements = `____`

**Q15.** [MCQ] QuickSelect average:
(A) O(log n)  (B) O(n)  (C) O(n log n)  (D) O(n²)

---

## Section B — 2 marks each

**Q16.** [MCQ] T(n) = 4T(n/2) + n²:
(A) Θ(n²)  (B) Θ(n² log n)  (C) Θ(n³)  (D) Θ(n^log₂4)

**Q17.** [NAT] T(n) = 7T(n/2) + n². Exponent in Θ(n^x) = `____` (round to 2 decimals)

**Q18.** [MCQ] T(n) = 2T(n−1) + 1, T(0) = 0. Solution:
(A) n − 1  (B) 2ⁿ − 1  (C) n²  (D) log n

**Q19.** [MCQ] Sort 1 million 32-bit integers — best practical algorithm?
(A) Bubble  (B) Selection  (C) Radix sort  (D) Insertion

**Q20.** [MCQ] Lower bound for finding median of n elements?
(A) Ω(1)  (B) Ω(log n)  (C) Ω(n)  (D) Ω(n log n)

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) Θ(n log n) | Master case 2 |
| 2 | (B) Θ(n) | sum 1 to n |
| 3 | (D) Θ(2ⁿ) | 2T(n−1)+1 |
| 4 | (B) ≤ | direct |
| 5 | 10 | 2¹⁰ |
| 6 | (C) Ω(n log n) | direct |
| 7 | (C) O(n²) | direct |
| 8 | (B) O(n) | adaptive |
| 9 | (B) No | needs O(n) aux |
| 10 | (B) O(n+k) | direct |
| 11 | (D) Merge | direct |
| 12 | (C) Heap | direct |
| 13 | (B) O(log n) | direct |
| 14 | 6 | log₂ 64 |
| 15 | (B) O(n) | direct |
| 16 | (B) Θ(n² log n) | log₂4=2; Master case 2 |
| 17 | 2.81 | log₂ 7 ≈ 2.807 |
| 18 | (B) 2ⁿ − 1 | direct |
| 19 | (C) Radix sort | linear time |
| 20 | (C) Ω(n) | direct (median-of-medians achieves O(n)) |

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
