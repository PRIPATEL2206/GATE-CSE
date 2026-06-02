# Topic Test 03 — Linear Algebra (Matrices · Linear Equations · Eigenvalues)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] det of `[[3,4],[2,5]]` = ?
(A) 7  (B) 23  (C) 15  (D) 8

**Q2.** [MCQ] A is 5×5 with det(A) = 4. det(2A) = ?
(A) 8  (B) 32  (C) 64  (D) 128

**Q3.** [MCQ] det(adj(A)) for A 4×4 with det(A) = 3:
(A) 9  (B) 27  (C) 81  (D) 3

**Q4.** [NAT] Trace of `[[1,2,3],[4,5,6],[7,8,9]]` = `____`

**Q5.** [MCQ] (AB)⁻¹ = ?
(A) A⁻¹B⁻¹  (B) B⁻¹A⁻¹  (C) (BA)⁻¹  (D) AB

**Q6.** [MCQ] A is skew-symmetric of order 5. det(A) = ?
(A) 0  (B) 1  (C) ±1  (D) cannot be determined

**Q7.** [MCQ] If rank(A) = rank([A|b]) < n, the system Ax = b has:
(A) unique solution  (B) no solution  (C) infinite solutions  (D) trivial only

**Q8.** [NAT] A is 4×6 matrix of rank 3. Dim of null space = `____`

**Q9.** [MCQ] Vectors (1,2,3), (4,5,6), (7,8,9) span:
(A) ℝ³  (B) a 1-D space  (C) a 2-D space  (D) {0}

**Q10.** [MCQ] Eigenvalues of `[[5,0,0],[0,3,0],[0,0,2]]` are:
(A) 5,3,2  (B) 0,0,0  (C) 1,1,1  (D) 10,6,4

**Q11.** [MCQ] A is 3×3 with eigenvalues 1, 2, 3. Then det(A) is:
(A) 6  (B) 0  (C) 1  (D) 5

**Q12.** [MCQ] A is symmetric. Eigenvalues are:
(A) all real  (B) all complex  (C) all positive  (D) on unit circle

**Q13.** [MCQ] If A² = A and A is 3×3 with rank 2, eigenvalues of A:
(A) 0, 0, 1  (B) 1, 1, 0  (C) 1, 1, 1  (D) 0, 1, 2

**Q14.** [NAT] A 2×2 matrix has tr = 5, det = 6. Sum of eigenvalues × product of eigenvalues = `____`

**Q15.** [MCQ] LU decomposition with L lower-triangular (1's on diag) of A = `[[2,4],[1,3]]`:
(A) L=`[[1,0],[0.5,1]]`, U=`[[2,4],[0,1]]`
(B) L=`[[1,0],[1,1]]`, U=`[[2,4],[0,−1]]`
(C) L=`[[1,0],[2,1]]`, U=`[[1,2],[0,−1]]`
(D) L=`[[1,0],[0.5,1]]`, U=`[[2,4],[0,2]]`

---

## Section B — 2 marks each

**Q16.** [MCQ] Find k for which the system has no solution:
x + 2y = 3, 2x + 4y = k.
(A) k = 6 only  (B) k ≠ 6  (C) k = 0  (D) all k

**Q17.** [NAT] A is 3×3 with eigenvalues 1, 2, 3. Trace of A² = `____`

**Q18.** [MCQ] Number of LI eigenvectors of `[[3,1,0],[0,3,1],[0,0,3]]`:
(A) 1  (B) 2  (C) 3  (D) 0

**Q19.** [MCQ] A is invertible 4×4. The eigenvalues of A⁻¹ are:
(A) reciprocals of eigenvalues of A
(B) negatives of eigenvalues of A
(C) squares of eigenvalues of A
(D) same as A

**Q20.** [MCQ] For the system: x + y + z = 0, x − y + αz = 0, 2x + αy + z = 0, what is the condition for non-trivial solutions?
(A) α = 1 only  (B) α = 1 or α = −2  (C) α = 0  (D) any α

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (A) 7 | 15 − 8 = 7 |
| 2 | (D) 128 | 2⁵ · 4 |
| 3 | (B) 27 | det(adj A) = det(A)^(n−1) = 3³ |
| 4 | 15 | 1+5+9 |
| 5 | (B) | reverse rule |
| 6 | (A) 0 | odd order skew-symm singular |
| 7 | (C) | infinite |
| 8 | 3 | 6 − 3 = 3 |
| 9 | (C) 2-D | row 3 = 2·row 2 − row 1 |
| 10 | (A) 5,3,2 | diagonal |
| 11 | (A) 6 | product |
| 12 | (A) all real | spectral |
| 13 | (B) 1,1,0 | idempotent, rank 2 |
| 14 | 30 | 5 · 6 |
| 15 | (A) | direct elimination |
| 16 | (B) k ≠ 6 | rank(A)=1, rank([A\|b])=2 unless k=6 |
| 17 | 14 | 1+4+9 |
| 18 | (A) 1 | (A−3I) has rank 2; nullity 1 |
| 19 | (A) | A⁻¹ has eigenvalues 1/λ |
| 20 | (B) | det = 0 ⇒ (α−1)(α+2) = 0 |

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
