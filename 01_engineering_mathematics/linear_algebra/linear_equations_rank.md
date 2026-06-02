# System of Linear Equations & Rank

> Subject: Engineering Mathematics → Linear Algebra
> GATE weight: **2–3 marks** every year. Rank, consistency, parameter conditions, vector spaces.

---

## 1. Concept Explanation

### 1.1 System of Linear Equations

A system `Ax = b` where `A` is m×n, `x` is n×1, `b` is m×1.

- **Homogeneous:** b = 0 (always has trivial solution x = 0).
- **Non-homogeneous:** b ≠ 0.
- **Augmented matrix:** `[A | b]`.

### 1.2 Rank

**Rank** of a matrix = max number of linearly independent rows (= max LI columns) = order of largest non-zero minor.

| Property |
|---|
| `rank(A) ≤ min(m, n)` |
| Rank unchanged by elementary row/column operations |
| `rank(A) = rank(Aᵀ)` |
| `rank(AB) ≤ min(rank(A), rank(B))` |
| `rank(A + B) ≤ rank(A) + rank(B)` |
| `rank(A) = n` ⇔ A has linearly independent columns ⇔ Ax = 0 has only trivial solution |

### 1.3 Consistency Theorem (Rouché–Capelli)

For `Ax = b` (m equations, n unknowns):

| Case | Behavior |
|---|---|
| `rank(A) ≠ rank([A\|b])` | Inconsistent — no solution |
| `rank(A) = rank([A\|b]) = n` | Unique solution |
| `rank(A) = rank([A\|b]) < n` | Infinitely many solutions (free variables = n − rank) |

For homogeneous `Ax = 0`:
- Always consistent (x = 0 works).
- Non-trivial solution exists ⇔ `rank(A) < n`.
- Number of LI solutions (nullity) = `n − rank(A)`.

### 1.4 Rank-Nullity Theorem

For A: ℝⁿ → ℝᵐ:

`rank(A) + nullity(A) = n`

where **nullity** = dim of null space (kernel) = # of LI solutions to Ax = 0.

### 1.5 Methods to Find Rank

1. **Echelon form:** Row-reduce; rank = # of non-zero rows.
2. **Largest non-zero minor:** rank = order of the largest non-zero minor.
3. **Inspection** for small matrices.

### 1.6 Solving Linear Systems

| Method | When to use |
|---|---|
| **Gaussian elimination** | General — produces echelon form |
| **Gauss-Jordan** | Find RREF directly + inverse |
| **Cramer's rule** | det ≠ 0 and small system |
| **Matrix inversion** | x = A⁻¹b when A is square invertible |
| **LU decomposition** | Multiple b's with same A |

**Cramer's rule:** `xᵢ = det(Aᵢ) / det(A)`, where Aᵢ is A with column i replaced by b.

### 1.7 LU Decomposition

Factor `A = LU` where L is lower triangular (1's on diagonal), U is upper triangular.

- Solve `Ly = b` (forward substitution).
- Then solve `Ux = y` (backward substitution).
- **Existence:** A's leading principal minors all non-zero.
- **PA = LU:** with row pivoting, always exists.

### 1.8 Vector Space (essential basics)

A **vector space** V over a field F satisfies 8 axioms (closure under +, ·, associativity, etc.).

**Subspace:** subset closed under +, scalar mult, contains 0.

**Linear combination:** `c₁v₁ + c₂v₂ + … + cₖvₖ`.

**Span:** set of all linear combinations.

**Linear independence:** no non-trivial combination equals 0.

**Basis:** LI spanning set. **Dimension** = size of any basis.

For ℝⁿ: standard basis `e₁, …, eₙ`; dim = n.

### 1.9 Four Fundamental Subspaces of A (m×n)

1. **Column space C(A)** ⊆ ℝᵐ — spanned by columns; dim = rank(A).
2. **Null space N(A)** ⊆ ℝⁿ — solutions to Ax = 0; dim = nullity(A) = n − rank(A).
3. **Row space C(Aᵀ)** ⊆ ℝⁿ — spanned by rows; dim = rank(A).
4. **Left null space N(Aᵀ)** ⊆ ℝᵐ — solutions to Aᵀy = 0; dim = m − rank(A).

`rank(A) + nullity(A) = n` (rank-nullity).
`C(A) ⊥ N(Aᵀ)` and `C(Aᵀ) ⊥ N(A)` (orthogonal complements).

### 1.10 Geometric Interpretation

| Case | Geometry (in ℝ³) |
|---|---|
| Unique solution | Three planes meeting at one point |
| No solution | Planes inconsistent (e.g., parallel) |
| Infinite solutions | Planes meet on a line or coincide |

### 1.11 Parameter Problems (typical GATE pattern)

Given a parameter k, find values for which:
1. Unique solution exists ⇒ det(A) ≠ 0 (square case).
2. No solution / infinite solutions ⇒ det(A) = 0 + check augmented rank.

**Workflow:** compute det(A) symbolically; set = 0 to find critical k; substitute and check rank.

> **Summary:** Rank determines everything. For Ax=b, compare rank(A) vs rank([A|b]) and n. Memorize Rouché–Capelli + rank-nullity. Master parameter-tuning + LU decomposition.

---

## 2. Important Points

- **Rouché–Capelli** is the deciding rule for consistency.
- For square A (n×n): unique solution ⇔ det(A) ≠ 0 ⇔ rank(A) = n ⇔ A invertible.
- Homogeneous Ax = 0 has non-trivial solution ⇔ det(A) = 0 (square) or rank(A) < n.
- The **null space dimension** = number of free parameters in solution.
- Elementary row operations: swap, scale, add multiple — preserve rank.
- Two systems are **equivalent** (same solutions) iff their augmented matrices are row-equivalent.
- `rank(AB) ≤ min(rank A, rank B)`. Equality often, but **not always**.
- For LU decomposition, U's diagonal elements are pivots.
- **Cramer's rule** is computationally expensive (O(n!)) — use Gauss for n ≥ 4.
- A **non-trivial linear combination** of vectors equals zero ⇔ vectors are linearly dependent.
- A set with more vectors than the dimension is **always linearly dependent**.
- Any LI set in ℝⁿ has size ≤ n.
- Rank of `[A | b]` is rank(A) or rank(A) + 1 — never more.
- The **dimension** of the solution space of Ax=0 = n − rank(A).

---

## 3. Short Notes

```
SYSTEM Ax = b
 m equations, n unknowns
 augmented matrix [A | b]

ROUCHÉ–CAPELLI
 rank(A) ≠ rank([A|b])  →  no solution
 rank(A) = rank([A|b]) = n  →  unique
 rank(A) = rank([A|b]) < n  →  infinite (n − rank free params)

HOMOGENEOUS Ax = 0
 always consistent
 non-trivial sol ⇔ rank(A) < n
 # LI solutions = n − rank(A) = nullity

RANK
 max LI rows = max LI cols
 rank(A) = rank(Aᵀ)
 rank ≤ min(m,n)
 rank(AB) ≤ min(rank A, rank B)
 echelon form: rank = # non-zero rows

RANK-NULLITY
 rank(A) + nullity(A) = n  (cols)

METHODS
 Gauss elimination → REF
 Gauss-Jordan → RREF
 Cramer: xᵢ = det(Aᵢ)/det(A)
 LU: A = LU, solve Ly=b, Ux=y
 PA = LU with row pivoting

FUNDAMENTAL SUBSPACES (A is m×n, rank r)
 C(A) ⊆ ℝᵐ ; dim = r
 N(A) ⊆ ℝⁿ ; dim = n − r
 C(Aᵀ) ⊆ ℝⁿ ; dim = r
 N(Aᵀ) ⊆ ℝᵐ ; dim = m − r

C(A) ⊥ N(Aᵀ); C(Aᵀ) ⊥ N(A)

VECTOR SPACE
 axioms; subspace; LI; basis; dim
 ℝⁿ standard basis e₁,…,eₙ : dim = n

PARAMETER PROBLEMS
 set det(A) = 0
 substitute, compare rank vs aug rank
```

---

## 4. Formulas / Tricks

| # | Formula / Rule | Memorize Cold? |
|---|---|---|
| 1 | Rouché–Capelli (3 cases) | ✅✅✅ |
| 2 | rank(A) + nullity(A) = n | ✅✅ |
| 3 | rank(A) = rank(Aᵀ) | ✅ |
| 4 | rank(AB) ≤ min(rank A, rank B) | ✅ |
| 5 | det(A) ≠ 0 ⇔ rank(A) = n (square) | ✅✅ |
| 6 | Cramer: xᵢ = det(Aᵢ)/det(A) | ✅ |
| 7 | A = LU with U upper, L lower with 1's | ✅ |
| 8 | Homogeneous nontrivial ⇔ rank < n | ✅✅ |
| 9 | dim(C(A)) = dim(C(Aᵀ)) = rank | ✅ |
| 10 | dim(N(A)) = n − rank | ✅ |
| 11 | If A is invertible, x = A⁻¹b | ✅ |
| 12 | Rank from echelon = # of pivots | ✅✅ |
| 13 | LI of {v₁,…,vₖ} ⇔ matrix [v₁ … vₖ] has rank k | ✅ |

### Tricks

- **Quick consistency test:** compute echelon of [A | b]. If a row is `[0 0 … 0 | c]` with c ≠ 0, inconsistent.
- **For parameter k**: set det = 0 to find critical k, then test each.
- **Solution count:** when rank = r and n unknowns, parametric form has `n − r` free variables, so the solution set is `n − r`-dimensional.
- **LU shortcut:** if all pivots come out from Gaussian elimination without row swaps, A = LU directly.
- **Rank from matrix:** count non-zero rows after echelon — done.
- **Rank ≤ 1 special:** A is a rank-1 matrix iff A = uvᵀ (outer product).
- **Linear independence shortcut:** k vectors in ℝⁿ with k > n are automatically dependent.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
The system Ax = b has a unique solution iff:
**Solution.** rank(A) = rank([A|b]) = n. *(Pattern: Rouché–Capelli.)*

### Q2. (GATE CSE 2014)
Find the value of k for which the system has infinitely many solutions:
2x + 3y + 4z = 11
3x + 4y + 5z = 12
4x + 5y + (k)z = 13.

**Solution.** Compute determinant of coefficient matrix and set = 0.
Determinant: |2 3 4; 3 4 5; 4 5 k| = 2(4k−25) − 3(3k−20) + 4(15−16) = 8k−50 − 9k+60 − 4 = −k + 6. Set 0 ⇒ k=6. Verify rank match.
**Answer: k = 6.**

### Q3. (GATE CSE 2018)
Number of LI solutions to Ax = 0 where A is 3×5 with rank 3:
**Solution.** Nullity = 5 − 3 = 2.

### Q4. (GATE CSE 2008)
A is 4×4 with rank 2. The dimension of null space is:
**Solution.** Nullity = 4 − 2 = 2.

### Q5. (GATE CSE 2016)
Consider Ax = b. If rank(A) = 3 and rank([A|b]) = 4 (with n = 5 unknowns), the system has:
**Solution.** Inconsistent — rank(A) ≠ rank([A|b]).

### Q6. (GATE CSE 2013)
Let A be a 3×3 matrix and b ∈ ℝ³. The set of solutions of Ax = b is:
(A) always non-empty
(B) empty if rank(A) < 3
(C) a single point if rank(A) = 3
(D) infinite if rank(A) < rank([A|b])

**Solution.** (C) is correct (rank 3 ⇒ unique solution). (D) is wrong: rank(A) < rank([A|b]) ⇒ no solution.
**Answer: (C).**

### Q7. (GATE CSE 2007)
The vectors v₁ = (1,0,1), v₂ = (0,1,1), v₃ = (1,1,2). Are they LI?
**Solution.** Det of matrix [v₁ v₂ v₃ as cols] = 0 (v₃ = v₁ + v₂). LD.

### Q8. (GATE CSE 2010)
The rank of the matrix `[[1,2,3],[4,5,6],[7,8,9]]` is:
**Solution.** Row 3 = 2·Row 2 − Row 1. Rank = 2.

### Q9. (GATE CSE 2003)
Number of LI solutions of homogeneous system:
3x + 2y − z = 0, 6x + 4y − 2z = 0, 9x + 6y − 3z = 0.
**Solution.** All rows multiples — rank 1; nullity = 3 − 1 = 2 LI solutions.

### Q10. (GATE CSE 2009)
The system x − 2y = 1, 3x − 6y = 3 has:
**Solution.** Rows are multiples (1:3); 1 equation effectively; rank(A) = rank([A|b]) = 1 < 2 ⇒ infinite solutions.

### Q11. (GATE CSE 2015)
LU decomposition of `[[2,3],[4,7]]`:
**Solution.** L = `[[1,0],[2,1]]`, U = `[[2,3],[0,1]]`.

### Q12. (GATE CSE 2019)
Rank of [[1,2,1],[3,−1,2],[1,1,3]]:
**Solution.** Row reduce: R₂ → R₂ − 3R₁ = [0,−7,−1]; R₃ → R₃ − R₁ = [0,−1,2]; R₃ → R₃ − (1/7)R₂ = [0,0,2+1/7]; rank = 3.

### Q13. (GATE CSE 2011)
For what values of α is the system consistent:
x + y + z = 1, x + 2y + 4z = α, x + 4y + 10z = α².
**Solution.** Reduce; find condition. Standard answer: **α = 1 or α = 2**.

### Q14. (GATE CSE 2020)
A is m×n with rank r. The dimension of the column space is:
**Solution.** r.

### Q15. (GATE CSE 2021)
Vectors (1,2), (2,4), (3,6) in ℝ². Maximum size LI subset:
**Solution.** All scalar multiples — only 1 LI vector.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Find rank of `[[1,2],[3,6]]`.

**P2.** Solve x + y = 5, 2x − y = 1.

**P3.** Number of solutions of x + y = 1, 2x + 2y = 2?

**P4.** Number of solutions of x + y = 1, x + y = 2?

**P5.** Are vectors (1,0,0), (0,1,0), (0,0,1) LI?

**P6.** Rank of identity matrix Iₙ?

**P7.** Solve Ax = 0 where A = `[[1,2],[2,4]]`.

**P8.** Apply Cramer's rule: x + 2y = 5, 3x + y = 1.

**P9.** Find dim of null space of A = `[[1,1,1],[1,1,1],[1,1,1]]`.

**P10.** State Rouché–Capelli theorem.

### Medium

**P11.** Find k for which system has unique solution: `2x+ky=3, x+2y=1`.

**P12.** Show: if A is m×n with m < n, then Ax = 0 has non-trivial solution.

**P13.** Compute LU of `[[1,2,3],[2,5,8],[3,7,11]]`.

**P14.** Find rank of `[[1,3,5,7],[2,5,8,11],[3,8,13,18]]`.

**P15.** For what value of λ does (1,1,λ), (1,λ,1), (λ,1,1) become LD?

**P16.** Solve x+y+z = 6, x−y+2z = 5, 2x+y−z = 1.

**P17.** Find general solution of x + 2y − z = 0, 2x + 5y + 2z = 0.

**P18.** Rank of `[[1,1,1],[1,2,4],[1,3,9]]` (Vandermonde 3×3).

**P19.** Show: rank(A·Aᵀ) = rank(A).

**P20.** Find a basis for the null space of A = `[[1,2,1,2],[2,4,3,5]]`.

### Hard

**P21.** Prove rank-nullity theorem.

**P22.** Show that if A is n×n with A² = 0 and A ≠ 0, then rank(A) ≤ n/2.

**P23.** Find conditions on a, b, c for which:
ax + y + z = 0
x + by + z = 0
x + y + cz = 0
has non-trivial solution.

**P24.** Decide consistency: x − y = 0, 2x + y = 3, 3x + 2y = 5.

**P25.** Find value of k such that rank of `[[k,1,1],[1,k,1],[1,1,k]]` is less than 3.

**P26.** Prove: for an m×n matrix A, rank(A) = rank(Aᵀ A) = rank(A Aᵀ).

**P27.** Find the rank of the n×n matrix with all entries 1.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 1 | row 2 is multiple |
| P2 | x = 2, y = 3 | substitution |
| P3 | infinite | rank=rank=1 < 2 |
| P4 | none | rank ≠ aug rank |
| P5 | Yes | standard basis |
| P6 | n | full rank |
| P7 | x = −2t, y = t | rank-1 |
| P8 | x = −3/5, y = 14/5 | Cramer |
| P9 | 2 | rank 1, nullity 3−1=2 |
| P10 | rank(A) vs rank([A\|b]) trichotomy | direct |
| P11 | k ≠ 4 | det = 4 − k ≠ 0 |
| P12 | rank ≤ m < n ⇒ nullity ≥ 1 | rank-nullity |
| P13 | L = `[[1,0,0],[2,1,0],[3,1,1]]`, U = `[[1,2,3],[0,1,2],[0,0,0]]` | row ops |
| P14 | 2 | row 3 = row 1 + row 2 |
| P15 | λ = 1 or λ = −2 | det = (λ−1)²(λ+2) |
| P16 | x=1,y=2,z=3 | unique |
| P17 | (x,y,z) = t(9,−4,1) | parameterize |
| P18 | 3 | Vandermonde with distinct entries |
| P19 | both have same null space ⇒ same rank | direct |
| P20 | basis: (−2,1,0,0), (1,0,−1,1) (or similar) | parameterize free vars |
| P21 | dim(domain) = dim(image) + dim(kernel) | LI completion |
| P22 | A² = 0 ⇒ image of A ⊆ kernel of A; dim(image) ≤ dim(ker) ⇒ rank ≤ nullity ⇒ rank ≤ n/2 | dimension bound |
| P23 | det = 0 condition | parameter |
| P24 | rank(A) = 2, rank([A\|b]) = 2 ⇒ unique x=1, y=1 | check |
| P25 | det = (k−1)²(k+2) = 0 ⇒ k = 1 or −2 | factor |
| P26 | use null spaces equal | direct |
| P27 | 1 | all rows identical |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing rank(A) and rank([A\|b]) order | Augmented rank ≥ matrix rank, never less. |
| 2 | Saying "homogeneous always has unique solution" | x = 0 is always a solution, but **non-trivial** solutions exist when rank < n. |
| 3 | Using Cramer when det = 0 | Cramer requires non-singular A. |
| 4 | Forgetting parameter case | Always set det = 0 first to find critical values. |
| 5 | Counting wrong free variables | # free = n − rank. |
| 6 | Misapplying rank-nullity | rank + nullity = **n** (cols), not m. |
| 7 | Treating dependent system as no solution | Dependent ⇒ infinite solutions, **not** zero. |
| 8 | Ignoring inconsistency from a single bad row | One row `[0…0 \| c]` with c ≠ 0 kills it. |
| 9 | Using LU on a matrix needing pivoting | Use PA = LU when pivots are zero. |
| 10 | Forgetting that 0 is always in null space | Null space is a subspace. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Unique / infinite / no solution?" | Rouché–Capelli on rank vs aug rank vs n. |
| "Find k for solution to exist" | det = 0 critical points + rank check. |
| "Solution space dimension" | n − rank(A). |
| "LI of vectors" | Stack as columns; rank = #vectors? |
| "Vectors span ℝⁿ?" | Stack as columns; rank = n? |
| "LU decomposition" | Gaussian elim without pivoting (or PA = LU). |
| "Cramer's rule" | det(A) ≠ 0; xᵢ = det(Aᵢ)/det(A). |
| "Rank of product" | ≤ min of ranks. |
| "Find basis for null space" | RREF + parameterize free variables. |
| "Find dim of column space" | rank(A). |

---

## 9. Quick Revision

```
ROUCHÉ–CAPELLI (Ax = b)
 rank(A) ≠ rank([A|b]) → no solution
 rank(A) = rank([A|b]) = n → unique
 rank(A) = rank([A|b]) < n → infinite (n−rank free)

HOMOGENEOUS Ax = 0
 always has x = 0
 nontrivial ⇔ rank < n
 # LI sols = n − rank = nullity

RANK
 max LI rows = max LI cols
 rank(A) = rank(Aᵀ)
 rank ≤ min(m,n)
 rank(AB) ≤ min(rank A, rank B)
 echelon: rank = # non-zero rows

RANK-NULLITY
 rank + nullity = n

FUNDAMENTAL SUBSPACES (m×n, rank r)
 C(A) ℝᵐ dim r
 N(A) ℝⁿ dim n−r
 C(Aᵀ) ℝⁿ dim r
 N(Aᵀ) ℝᵐ dim m−r

METHODS
 Gauss → REF
 Gauss-Jordan → RREF
 Cramer: xᵢ = det(Aᵢ)/det(A)
 LU: A = LU
 PA = LU with pivoting

PARAMETER (det=0)
 step 1: det → critical k
 step 2: substitute, compare rank/aug rank

LI shortcut
 k vectors in ℝⁿ, k > n ⇒ LD
```
