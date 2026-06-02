# Topic Test 13 — Algorithms (Greedy · Divide & Conquer · Dynamic Programming)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Greedy criterion for activity selection:
(A) Earliest start  (B) Earliest finish  (C) Shortest duration  (D) Latest start

**Q2.** [MCQ] Greedy works for which knapsack?
(A) 0/1  (B) Bounded  (C) Fractional  (D) Both A and B

**Q3.** [MCQ] Huffman tree: most frequent char gets:
(A) Longest code  (B) Shortest code  (C) Same code  (D) No code

**Q4.** [MCQ] Number of edges in MST of n-vertex connected graph:
(A) n  (B) n−1  (C) n+1  (D) 2n

**Q5.** [MCQ] Kruskal complexity:
(A) O(V²)  (B) O(E log V)  (C) O(E + V)  (D) O(V³)

**Q6.** [MCQ] Strassen exponent:
(A) log₂ 7  (B) log₂ 5  (C) log₂ 6  (D) log₂ 8

**Q7.** [MCQ] Karatsuba exponent:
(A) log₂ 4  (B) log₂ 3  (C) log₂ 2  (D) log₂ 5

**Q8.** [MCQ] Closest pair of points D&C time:
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(n³)

**Q9.** [MCQ] Tower of Hanoi:
(A) Θ(n)  (B) Θ(n²)  (C) Θ(2ⁿ)  (D) Θ(n!)

**Q10.** [MCQ] DP requires:
(A) Optimal substructure only  (B) Overlap only  (C) Both  (D) Neither

**Q11.** [MCQ] 0/1 Knapsack DP time:
(A) O(n)  (B) O(W)  (C) O(nW)  (D) O(n²W)

**Q12.** [NAT] Number of operations in O(n³) MCM for n=4 matrices = `____` (just exponent → write 3)

**Q13.** [MCQ] LCS time:
(A) O(m+n)  (B) O(mn)  (C) O(m log n)  (D) O(min(m,n))

**Q14.** [MCQ] Floyd-Warshall:
(A) O(V²)  (B) O(V³)  (C) O(V·E)  (D) O((V+E) log V)

**Q15.** [MCQ] Bellman-Ford handles:
(A) Negative weights  (B) Only positive  (C) Only zero  (D) Only undirected

---

## Section B — 2 marks each

**Q16.** [MCQ] Activities (start, finish): (1,4), (3,5), (0,6), (5,7), (8,9). Max non-overlapping?
(A) 2  (B) 3  (C) 4  (D) 5

**Q17.** [NAT] LCS length of "ABCBDAB" and "BDCAB" = `____`

**Q18.** [MCQ] T(n) = 7T(n/2) + n². Solution:
(A) Θ(n²)  (B) Θ(n² log n)  (C) Θ(n^log₂7)  (D) Θ(n³)

**Q19.** [MCQ] 0/1 Knapsack: items (w,v) = (1,1), (2,2), (3,5); W=4. Max value?
(A) 5  (B) 6  (C) 7  (D) 8

**Q20.** [MCQ] Coin change {1, 3, 4} for W = 6 — greedy answer vs optimal:
(A) Same (3 coins)  (B) Greedy 3, optimal 2  (C) Greedy 2, optimal 3  (D) Both 4 coins

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | direct |
| 2 | (C) | direct |
| 3 | (B) | direct |
| 4 | (B) n−1 | direct |
| 5 | (B) | direct |
| 6 | (A) log₂ 7 | direct |
| 7 | (B) log₂ 3 | direct |
| 8 | (B) | direct |
| 9 | (C) | direct |
| 10 | (C) | direct |
| 11 | (C) | direct |
| 12 | 3 | exponent |
| 13 | (B) | direct |
| 14 | (B) | direct |
| 15 | (A) | direct |
| 16 | (B) 3 | (1,4)→(5,7)→(8,9) |
| 17 | 4 | "BCAB" or "BDAB" |
| 18 | (C) | n² < n^log₂7 ≈ n^2.81; case 1 |
| 19 | (B) 6 | items 2 and 3 |
| 20 | (B) | greedy 4+1+1 = 3; optimal 3+3 = 2 |

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
