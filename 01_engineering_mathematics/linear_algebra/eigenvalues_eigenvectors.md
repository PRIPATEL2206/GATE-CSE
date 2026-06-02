# Eigenvalues, Eigenvectors & LU Decomposition

> Subject: Engineering Mathematics → Linear Algebra
> GATE weight: **2–4 marks** every year. Eigenvalue computation, properties, diagonalization.

---

## 1. Concept Explanation

### 1.1 Eigenvalues and Eigenvectors

For a square matrix A (n×n):

`Ax = λx`, where x ≠ 0.

- **λ** is an **eigenvalue**.
- **x** is an **eigenvector** corresponding to λ.

Equivalently `(A − λI)x = 0` has non-trivial solution ⇔ `det(A − λI) = 0`.

### 1.2 Characteristic Polynomial

`p(λ) = det(λI − A)` — a polynomial of degree n.

For 2×2: `p(λ) = λ² − tr(A)·λ + det(A)`.

For 3×3: `p(λ) = λ³ − tr(A)·λ² + (sum of 2×2 principal minors)·λ − det(A)`.

**Roots = eigenvalues.**

### 1.3 Properties of Eigenvalues

| # | Property |
|---|---|
| 1 | Σ λᵢ = tr(A) |
| 2 | ∏ λᵢ = det(A) |
| 3 | Eigenvalues of Aᵀ = eigenvalues of A |
| 4 | Eigenvalues of A⁻¹ = 1/λᵢ |
| 5 | Eigenvalues of Aᵏ = λᵢᵏ |
| 6 | Eigenvalues of (A + cI) = λᵢ + c |
| 7 | Eigenvalues of cA = c·λᵢ |
| 8 | Triangular matrix → eigenvalues = diagonal entries |
| 9 | Symmetric/Hermitian matrix → all eigenvalues real, eigenvectors orthogonal |
| 10 | Skew-symmetric → eigenvalues 0 or pure imaginary |
| 11 | Orthogonal/Unitary → \|λ\| = 1 |
| 12 | Idempotent (A² = A) → λ ∈ {0, 1} |
| 13 | Involutory (A² = I) → λ ∈ {±1} |
| 14 | Nilpotent (Aᵏ = 0) → all λ = 0 |
| 15 | Sum of geometric multiplicities ≤ algebraic multiplicities |

### 1.4 Eigenvector Properties

- Eigenvectors corresponding to **distinct eigenvalues are linearly independent**.
- For a symmetric matrix, eigenvectors corresponding to distinct eigenvalues are **orthogonal**.
- The **eigenspace** Eλ = null space of (A − λI). dim(Eλ) = **geometric multiplicity** of λ.
- **Algebraic multiplicity** = multiplicity of λ as root of char poly.
- `1 ≤ geom mult ≤ alg mult ≤ n`.

### 1.5 Diagonalization

A matrix A is **diagonalizable** iff there exists an invertible P such that

`P⁻¹ A P = D`, where D = diag(λ₁, …, λₙ).

**Conditions for diagonalizability:**
- A has n linearly independent eigenvectors, **iff** for every λ, geom mult = alg mult.
- Sufficient: A has n distinct eigenvalues (then automatically diagonalizable).
- Symmetric / Hermitian / Normal matrices are always diagonalizable (in fact, by orthogonal/unitary P).

`P = [v₁ | v₂ | … | vₙ]` (columns = eigenvectors).

### 1.6 Computing Powers via Diagonalization

`A = PDP⁻¹  ⇒  Aᵏ = P Dᵏ P⁻¹`

where Dᵏ = diag(λ₁ᵏ, …, λₙᵏ). Useful for fast computation of high powers.

### 1.7 Cayley-Hamilton Theorem

Every n×n matrix A satisfies its characteristic equation: `p(A) = 0`.

**Use 1:** compute Aⁿ in terms of lower powers.
**Use 2:** compute A⁻¹ when A is invertible:
For 2×2: `A² − tr(A)A + det(A)I = 0 ⇒ A⁻¹ = (1/det(A))(tr(A)I − A)`.

### 1.8 LU Decomposition

Factor A = LU where:
- L: lower triangular (1's on diagonal — Doolittle convention)
- U: upper triangular

**Procedure (Doolittle):**
1. Apply Gaussian elimination without row swaps.
2. Multipliers (negated) form L below diagonal.
3. Resulting upper-triangular matrix is U.

**For 2×2:**
`A = [[a,b],[c,d]] = [[1,0],[c/a,1]] · [[a,b],[0,d − bc/a]]`

**Existence:** all leading principal minors of A are non-zero.

**With pivoting:** PA = LU always exists.

### 1.9 Solving Ax = b via LU

1. Decompose A = LU.
2. Solve `Ly = b` (forward substitution).
3. Solve `Ux = y` (backward substitution).

**Cost:** decomposition O(n³); each solve O(n²). Faster than recomputing inverse.

### 1.10 Cholesky Decomposition (for symmetric +ve definite)

A = L Lᵀ where L is lower triangular with positive diagonal. Half the work of LU.

### 1.11 Spectral Theorem

For real symmetric matrix A:
- All eigenvalues real.
- Orthogonal diagonalization: A = Q D Qᵀ where Q orthogonal.
- Eigenvectors of distinct eigenvalues are orthogonal.

### 1.12 Quadratic Forms

`Q(x) = xᵀ A x` (A symmetric).

| Eigenvalues | Type |
|---|---|
| All > 0 | Positive definite |
| All ≥ 0 | Positive semi-definite |
| All < 0 | Negative definite |
| Mixed | Indefinite |

> **Summary:** Eigenvalues solve `det(A−λI)=0`. Memorize the 15 properties — that's where 80% of GATE PYQs live. Diagonalization needs n LI eigenvectors. LU is Gaussian elimination factored; use for solving multiple b.

---

## 2. Important Points

- `Σ λᵢ = tr(A)`; `∏ λᵢ = det(A)` — the two anchor identities.
- For triangular matrices, eigenvalues sit on the diagonal — read them off directly.
- Eigenvalues of A and Aᵀ are identical.
- `Aᵏx = λᵏx` if Ax = λx.
- 0 is an eigenvalue ⇔ A is singular.
- A symmetric matrix is always diagonalizable (orthogonally).
- A matrix with **n distinct eigenvalues** is always diagonalizable.
- Eigenvectors for **distinct** eigenvalues are LI.
- Eigenvectors for the same eigenvalue can span dim ≤ algebraic multiplicity.
- A matrix is invertible ⇔ 0 is not an eigenvalue.
- Algebraic mult ≥ geometric mult always.
- A and B = P⁻¹AP are **similar** — they share eigenvalues, det, trace, char poly.
- **Spectral radius** = max |λᵢ|. Iterative methods converge iff < 1.
- For symmetric A: positive definite ⇔ all leading principal minors > 0 (Sylvester's criterion).
- LU decomposition fails when a pivot is zero; use partial pivoting.
- A · adj(A) = det(A) · I — used to compute A⁻¹.

---

## 3. Short Notes

```
EIGEN
 Ax = λx, x ≠ 0
 char poly: p(λ) = det(λI − A)
 Σ λᵢ = tr(A);  ∏ λᵢ = det(A)
 2×2: λ² − tr·λ + det = 0
 3×3: λ³ − tr·λ² + Σ(2×2 minors)·λ − det = 0

EIGENVALUE PROPERTIES
 A and Aᵀ same eigenvalues
 A⁻¹ has 1/λ
 Aᵏ has λᵏ
 A + cI has λ + c
 cA has c·λ
 triangular: λ = diagonals
 orthogonal: |λ| = 1
 symmetric: λ real, eigenvectors orthogonal
 idempotent (A²=A): λ ∈ {0,1}
 nilpotent (Aᵏ=0): all λ = 0

EIGENVECTOR
 Eλ = N(A − λI)
 geom mult = dim(Eλ)
 1 ≤ geom mult ≤ alg mult ≤ n
 distinct λ → eigenvectors LI

DIAGONALIZATION
 P⁻¹ A P = D
 P = [v₁|v₂|…|vₙ]
 D = diag(λ₁,...,λₙ)
 ⇔ A has n LI eigenvectors
 ⇔ ∀λ: geom = alg mult
 sufficient: n distinct eigenvalues
 always: symmetric, hermitian, normal

POWERS
 Aᵏ = P Dᵏ P⁻¹

CAYLEY-HAMILTON
 p(A) = 0
 use to compute Aⁿ, A⁻¹
 2×2: A² − tr·A + det·I = 0

LU DECOMPOSITION
 A = LU (no pivots) or PA = LU
 L: lower (1 diag), U: upper
 forward solve Ly = b
 backward solve Ux = y
 cost: O(n³) decomp + O(n²) solve
 exists ⇔ leading principal minors ≠ 0

CHOLESKY
 A = LLᵀ
 only for symmetric +ve definite

QUADRATIC FORM
 Q(x) = xᵀAx (A symm)
 +ve def: λ > 0; +ve semi: λ ≥ 0
 Sylvester: leading minors > 0
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | det(A − λI) = 0 | ✅✅✅ |
| 2 | Σ λᵢ = tr(A); ∏ λᵢ = det(A) | ✅✅✅ |
| 3 | 2×2 char eq: `λ² − tr·λ + det = 0` | ✅✅ |
| 4 | A invertible ⇔ 0 ∉ spectrum(A) | ✅ |
| 5 | Eigenvalues of Aᵏ = λᵢᵏ | ✅✅ |
| 6 | Eigenvalues of A⁻¹ = 1/λᵢ | ✅✅ |
| 7 | Eigenvalues of A + cI = λᵢ + c | ✅ |
| 8 | Triangular ⇒ λ = diagonals | ✅✅ |
| 9 | Symmetric ⇒ λ real, eigenvectors orthogonal | ✅✅ |
| 10 | Cayley-Hamilton: p(A) = 0 | ✅ |
| 11 | A = PDP⁻¹ ⇒ Aᵏ = P Dᵏ P⁻¹ | ✅ |
| 12 | n distinct λ ⇒ diagonalizable | ✅✅ |
| 13 | LU exists ⇔ leading principal minors ≠ 0 | ✅ |
| 14 | Cholesky: A = LLᵀ for symm +ve def | ✅ |
| 15 | Spectral radius ρ(A) = max\|λᵢ\| | ✅ |

### Tricks

- **Trace + Determinant** for 2×2 directly gives both eigenvalues:
  λ = (tr ± √(tr² − 4·det)) / 2.
- **For Aᵏ at large k**: diagonalize, raise D, multiply back.
- **Cayley-Hamilton trick:** if char poly is known, plug in matrix — useful for computing high powers without diagonalization.
- **Eigenvalues of block-diagonal:** union of eigenvalues of each block.
- **Eigenvalues of A + cI**: shift by c — use to engineer characteristic polynomial.
- **Power iteration:** compute Aⁿv repeatedly — converges to eigenvector of largest |λ|.
- **Quick LU sanity:** L's diagonal is all 1's; U's diagonal is the pivots.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Eigenvalues of `[[2,1],[1,2]]`:
**Solution.** λ² − 4λ + 3 = 0 ⇒ λ = 1, 3.

### Q2. (GATE CSE 2014)
A is 3×3 with eigenvalues 1, 2, 3. Find tr(A), det(A), tr(A²):
**Solution.** tr = 6, det = 6, tr(A²) = 1 + 4 + 9 = 14.

### Q3. (GATE CSE 2008)
The eigenvalues of a 3×3 matrix are 1, 2, 3. The eigenvalues of A² + 2I are:
**Solution.** λ² + 2 → 3, 6, 11.

### Q4. (GATE CSE 2018)
A is 4×4 orthogonal with det(A) = 1. The product of all eigenvalues is:
**Solution.** ∏ λ = det = 1.

### Q5. (GATE CSE 2013)
Number of LI eigenvectors of `[[2,1],[0,2]]`:
**Solution.** Single eigenvalue 2 with algebraic mult 2; (A − 2I) = `[[0,1],[0,0]]` has rank 1, nullity 1. So 1 LI eigenvector.

### Q6. (GATE CSE 2010)
A is 3×3 symmetric. Number of LI eigenvectors:
**Solution.** Always 3 (symmetric ⇒ diagonalizable).

### Q7. (GATE CSE 2015)
LU decomposition of `[[1,2],[3,4]]`:
**Solution.** L = `[[1,0],[3,1]]`, U = `[[1,2],[0,−2]]`.

### Q8. (GATE CSE 2007)
Eigenvalues of A = `[[1,2,3],[0,4,5],[0,0,6]]`:
**Solution.** Triangular ⇒ 1, 4, 6.

### Q9. (GATE CSE 2012)
Eigenvalues of A⁻¹ where A has eigenvalues 1, 2, 4:
**Solution.** 1, 1/2, 1/4.

### Q10. (GATE CSE 2009)
A is 2×2 with tr = 6, det = 8. Eigenvalues:
**Solution.** λ² − 6λ + 8 = 0 ⇒ λ = 2, 4.

### Q11. (GATE CSE 2003)
Verify Cayley-Hamilton for `[[1,2],[3,4]]`. Char poly?
**Solution.** λ² − 5λ − 2 = 0; A² − 5A − 2I = ?
Compute A² = `[[7,10],[15,22]]`; 5A = `[[5,10],[15,20]]`; 2I = `[[2,0],[0,2]]`.
A² − 5A − 2I = `[[0,0],[0,0]]` ✓.

### Q12. (GATE CSE 2019)
Eigenvalues of a 3×3 magic square (constant row/col/diag sum) include:
**Solution.** Sum is always one eigenvalue (with eigenvector = all-1's).

### Q13. (GATE CSE 2020)
A symmetric matrix has eigenvalues 1, 2, 3. Then A is:
**Solution.** Symmetric with positive eigenvalues ⇒ positive definite.

### Q14. (GATE CSE 2021)
A is similar to B (B = P⁻¹AP). Which is/are equal?
(I) det (II) trace (III) eigenvalues (IV) characteristic polynomial.
**Answer:** All four.

### Q15. (GATE CSE 2016)
A is idempotent, 4×4 with rank 3. Eigenvalues are:
**Solution.** Idempotent ⇒ λ ∈ {0,1}. Rank 3 ⇒ three 1's, one 0.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Find eigenvalues of `[[3,0],[0,5]]`.

**P2.** Find eigenvalues of `[[2,1],[0,2]]`.

**P3.** Trace of A = `[[1,2,3],[4,5,6],[7,8,9]]`.

**P4.** A has eigenvalues 2, 3, 5. det(A) = ?

**P5.** A has eigenvalues 1, 2, 3. Trace of A² = ?

**P6.** Eigenvalues of identity I₅?

**P7.** Find eigenvector of `[[2,0],[0,3]]` for λ = 2.

**P8.** A is symmetric with eigenvalues 1, 4. Are eigenvectors orthogonal?

**P9.** Compute LU of `[[2,4],[3,7]]`.

**P10.** Is `[[0,1],[0,0]]` diagonalizable?

### Medium

**P11.** Find eigenvalues and eigenvectors of `[[4,1],[2,3]]`.

**P12.** A is 3×3 with eigenvalues 1, 1, 2. Diagonalizable?

**P13.** Compute A¹⁰ for A = `[[2,0],[0,3]]`.

**P14.** Verify Cayley-Hamilton for `[[1,1],[0,2]]`.

**P15.** Find LU of `[[1,1,1],[2,3,5],[4,6,8]]`.

**P16.** A symmetric, A² = A. Possible eigenvalues?

**P17.** Show: similar matrices have same characteristic polynomial.

**P18.** A is 4×4 with rank 2. How many zero eigenvalues at minimum?

**P19.** Find eigenvalues of A = `[[1,1],[1,1]]`.

**P20.** Diagonalize A = `[[5,−4],[2,−1]]`.

### Hard

**P21.** Show: an n×n matrix with n distinct eigenvalues is diagonalizable.

**P22.** A is 3×3 idempotent with rank 2. Find tr(A) and det(A).

**P23.** Compute Aⁿ for A = `[[1,1],[1,0]]` (Fibonacci matrix).

**P24.** A is 3×3 with characteristic polynomial λ³ − 6λ² + 11λ − 6. Compute A⁻¹ via Cayley-Hamilton.

**P25.** Show: if A is real symmetric, eigenvectors of distinct eigenvalues are orthogonal.

**P26.** Find the rank of A − 2I where A is the Fibonacci matrix.

**P27.** Compute Cholesky of `[[4,2],[2,3]]`.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 3, 5 | diagonal |
| P2 | 2 (repeated) | upper triangular |
| P3 | 15 | sum of diagonals |
| P4 | 30 | product |
| P5 | 14 | 1+4+9 |
| P6 | 1 (mult 5) | I |
| P7 | (1, 0) | direct |
| P8 | Yes | symmetric |
| P9 | L = `[[1,0],[1.5,1]]`, U = `[[2,4],[0,1]]` | direct |
| P10 | No | nilpotent, single eigenvalue 0 with geom mult 1 |
| P11 | λ = 5, 2; eigenvectors (1,1) and (1,−2) | direct |
| P12 | Maybe — check if geom mult of λ=1 is 2 | conditional |
| P13 | `[[1024,0],[0,59049]]` | diagonal raised |
| P14 | A² − 3A + 2I = 0 ⇒ verify | direct |
| P15 | L, U from elimination — write out | row ops |
| P16 | 0 or 1 | idempotent |
| P17 | det(λI−B) = det(λI − P⁻¹AP) = det(P⁻¹(λI−A)P) = det(λI−A) | direct |
| P18 | 2 zero eigenvalues | rank 2 ⇒ nullity 2 |
| P19 | 0, 2 | tr=2, det=0 |
| P20 | λ = 1, 3; diagonalize | direct |
| P21 | distinct λ → eigenvectors LI → form basis | direct |
| P22 | tr = 2, det = 0 | sum of eigenvalues, λ ∈ {0,1} |
| P23 | Aⁿ = `[[F_{n+1}, Fₙ], [Fₙ, F_{n−1}]]` | Fibonacci |
| P24 | A⁻¹ = (1/6)(A² − 6A + 11I) | C-H |
| P25 | xᵀAy = (Ax)ᵀy = (λx)ᵀy = λ xᵀy; also = xᵀ(λ'y); so (λ−λ') xᵀy = 0; λ ≠ λ' ⇒ xᵀy = 0 | symm proof |
| P26 | Char poly λ²−λ−1; eigenvalues φ, 1−φ; A−2I has eigenvalues φ−2, −φ−1; both ≠ 0 ⇒ rank 2 | shift |
| P27 | L = `[[2,0],[1, √2]]` | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing det(A − λI) and det(λI − A) | They differ by (−1)ⁿ; same roots. |
| 2 | Forgetting algebraic vs geometric multiplicity | Diagonalizable iff geom = alg for **every** eigenvalue. |
| 3 | Saying "eigenvectors are unique" | They're determined up to scaling; can be a whole subspace. |
| 4 | Computing eigenvalues of triangular matrix the hard way | Read off the diagonal. |
| 5 | LU on a matrix needing pivoting | Use PA = LU. |
| 6 | Skipping verification of Cayley-Hamilton | Always plug in. |
| 7 | Forgetting that eigenvectors of A and A + cI are the same | Only eigenvalues shift by c. |
| 8 | Treating A and Aᵀ as having different eigenvalues | They share eigenvalues (different eigenvectors though). |
| 9 | Diagonalizing without checking n LI eigenvectors | Some matrices (defective) cannot be diagonalized. |
| 10 | Computing Cholesky on non-symmetric matrix | Cholesky requires symmetric +ve definite. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Find eigenvalues" | det(A − λI) = 0; for 2×2, use tr/det shortcut. |
| "Sum / product of eigenvalues" | tr(A) and det(A). |
| "Eigenvalues of triangular" | Diagonal entries. |
| "Compute Aⁿ for large n" | Diagonalize: A = PDP⁻¹, Aⁿ = PDⁿP⁻¹. |
| "Symmetric matrix property" | Real eigenvalues, orthogonal eigenvectors, always diagonalizable. |
| "Idempotent / Nilpotent / Involutory" | λ ∈ {0,1} / all 0 / λ ∈ {±1}. |
| "Diagonalizable?" | Check if n LI eigenvectors. |
| "LU decomposition" | Gaussian elimination without pivoting. |
| "Cayley-Hamilton inverse trick" | A · (lower polynomial in A) = some scalar · I. |
| "Quadratic form definiteness" | Sign pattern of eigenvalues / Sylvester. |

---

## 9. Quick Revision

```
Ax = λx (x ≠ 0)
char poly p(λ) = det(λI − A)
Σ λᵢ = tr(A)    ∏ λᵢ = det(A)
2×2: λ² − tr·λ + det = 0

EIGENVALUE PROPERTIES
 A, Aᵀ: same λ
 A⁻¹: 1/λ
 Aᵏ: λᵏ
 A + cI: λ + c
 cA: c·λ
 triangular: diagonals
 symmetric: real, orthogonal eigenvectors
 orthogonal: |λ|=1
 idempotent: λ ∈ {0,1}
 nilpotent: all λ = 0
 involutory: λ ∈ {±1}

DIAGONALIZATION
 P⁻¹ A P = D = diag(λ)
 ⇔ n LI eigenvectors
 ⇔ ∀λ: geom = alg mult
 sufficient: n distinct λ
 always: symmetric, hermitian, normal

CAYLEY-HAMILTON: p(A) = 0
2×2: A² − tr·A + det·I = 0

POWERS: Aᵏ = P Dᵏ P⁻¹

LU
 A = LU (no pivot) or PA = LU
 forward Ly=b, backward Ux=y
 cost O(n³) + O(n²)

CHOLESKY: A = LLᵀ (symm +ve def)

QUADRATIC FORMS
 +ve def : λ > 0
 +ve semi: λ ≥ 0
 Sylvester: leading minors > 0
```
