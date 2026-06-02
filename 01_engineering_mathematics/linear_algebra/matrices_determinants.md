# Matrices & Determinants

> Subject: Engineering Mathematics → Linear Algebra
> GATE weight: **2–4 marks** every year. Determinants, inverse, properties, special matrices.

---

## 1. Concept Explanation

### 1.1 Matrix

A **matrix** is a rectangular array of numbers. `A_{m×n}` has m rows, n columns. `aᵢⱼ` = element at row i, column j.

**Square matrix:** m = n. Order = n.

### 1.2 Special Matrices

| Type | Definition |
|---|---|
| Zero matrix | all entries 0 |
| Identity Iₙ | aᵢᵢ = 1, off-diagonal = 0 |
| Diagonal | aᵢⱼ = 0 for i ≠ j |
| Scalar | diagonal with all diagonal entries equal |
| Upper triangular | aᵢⱼ = 0 for i > j |
| Lower triangular | aᵢⱼ = 0 for i < j |
| Symmetric | A = Aᵀ ⇔ aᵢⱼ = aⱼᵢ |
| Skew-symmetric | Aᵀ = −A ⇔ aᵢⱼ = −aⱼᵢ; diagonal = 0 |
| Hermitian | A = Aᴴ (conjugate transpose) |
| Orthogonal | AᵀA = I, i.e., A⁻¹ = Aᵀ |
| Unitary | AᴴA = I |
| Idempotent | A² = A |
| Nilpotent | Aᵏ = 0 for some k ≥ 1 |
| Involutory | A² = I |
| Singular | det(A) = 0 |
| Non-singular | det(A) ≠ 0 |

### 1.3 Matrix Operations

- **Addition / subtraction:** element-wise; same dimensions.
- **Scalar multiplication:** multiply every entry.
- **Matrix multiplication** `(AB)ᵢⱼ = Σₖ aᵢₖ bₖⱼ`. Defined when cols(A) = rows(B). **Not commutative** in general.
- **Transpose** Aᵀ: swap rows ↔ columns. `(AB)ᵀ = BᵀAᵀ`.
- **Inverse** A⁻¹: A·A⁻¹ = I. Exists iff det(A) ≠ 0.

### 1.4 Determinant

For 2×2: `det = ad − bc` for `[[a,b],[c,d]]`.

For 3×3 (Sarrus / cofactor expansion):
`|A| = a₁₁(a₂₂a₃₃ − a₂₃a₃₂) − a₁₂(a₂₁a₃₃ − a₂₃a₃₁) + a₁₃(a₂₁a₃₂ − a₂₂a₃₁)`.

**General:** Σ over permutations σ of `sgn(σ) · ∏ aᵢ,σ(i)`.

### 1.5 Properties of Determinants

| # | Property |
|---|---|
| 1 | det(Iₙ) = 1 |
| 2 | det(Aᵀ) = det(A) |
| 3 | det(kA) = kⁿ det(A) for n×n |
| 4 | det(AB) = det(A) · det(B) |
| 5 | det(A⁻¹) = 1/det(A) |
| 6 | Swap two rows ⇒ det changes sign |
| 7 | Two equal rows ⇒ det = 0 |
| 8 | Multiply a row by k ⇒ det multiplied by k |
| 9 | Add a multiple of one row to another ⇒ det unchanged |
| 10 | Triangular matrix: det = product of diagonal entries |
| 11 | Block triangular: det = det(A₁₁) · det(A₂₂) |
| 12 | det of orthogonal matrix = ±1 |
| 13 | det of skew-symmetric of odd order = 0 |
| 14 | If A nilpotent ⇒ det(A) = 0 |
| 15 | det(adj(A)) = det(A)^(n−1) |

### 1.6 Adjoint & Inverse

**Cofactor** `Cᵢⱼ = (−1)^(i+j) · Mᵢⱼ` where Mᵢⱼ is the minor.

**Adjoint** `adj(A) = transpose of cofactor matrix`.

**Inverse formula:** `A⁻¹ = (1/det(A)) · adj(A)`.

**Properties:**
- `A · adj(A) = adj(A) · A = det(A) · I`.
- `adj(adj(A)) = det(A)^(n−2) · A`.
- `det(adj(A)) = det(A)^(n−1)`.

### 1.7 Trace

`tr(A) = Σ aᵢᵢ` (sum of diagonal).

| Property |
|---|
| tr(A + B) = tr(A) + tr(B) |
| tr(kA) = k · tr(A) |
| tr(AB) = tr(BA) |
| tr(Aᵀ) = tr(A) |
| tr(A) = sum of eigenvalues |
| det(A) = product of eigenvalues |

### 1.8 Rank (overview — full topic in next file)

**Rank** = max # of linearly independent rows = max # of LI columns. Equal to size of largest non-zero minor.

`rank(A) ≤ min(m, n)`.

### 1.9 Row Echelon & RREF

- **Row Echelon Form (REF):** zeros below leading entries; each leading entry is to the right of the one above.
- **Reduced Row Echelon Form (RREF):** REF + leading entries = 1 + zeros above each leading 1.

Apply **elementary row operations** (swap, scale, replace).

### 1.10 Symmetric & Skew-Symmetric Decomposition

Any square matrix `A = (1/2)(A + Aᵀ) + (1/2)(A − Aᵀ)` — sum of symmetric + skew-symmetric.

### 1.11 Inverse Tricks

For 2×2 `A = [[a,b],[c,d]]`: `A⁻¹ = (1/(ad−bc)) [[d,−b],[−c,a]]`.

**Properties:**
- `(AB)⁻¹ = B⁻¹ A⁻¹` (reverse).
- `(Aᵀ)⁻¹ = (A⁻¹)ᵀ`.
- `(kA)⁻¹ = (1/k) A⁻¹`.

### 1.12 Cayley–Hamilton

Every square matrix A satisfies its own characteristic equation: `p(A) = 0` where `p(λ) = det(λI − A)`.

> **Summary:** Master determinant properties (signs, scaling, swap), inverse via adj/det, Cayley-Hamilton, trace = Σ eigenvalues, det = ∏ eigenvalues. The 15-row property table is the heart of every PYQ.

---

## 2. Important Points

- `det(AB) = det(A) · det(B)`; `det(A + B) ≠ det(A) + det(B)` (a frequent trap).
- A matrix has an inverse ⇔ det(A) ≠ 0 ⇔ rows are LI ⇔ columns are LI.
- For a triangular matrix (upper or lower), determinant = product of diagonals.
- For an orthogonal matrix Q: Qᵀ Q = I, det(Q) = ±1, columns are orthonormal.
- Eigenvalues of triangular matrix = diagonal entries.
- `tr(A) = Σ λᵢ`, `det(A) = ∏ λᵢ`.
- Skew-symmetric matrix of **odd order** is singular (det = 0).
- Every square matrix = symmetric part + skew-symmetric part.
- `(AB)⁻¹ = B⁻¹A⁻¹`; same reverse rule for transpose.
- Rank doesn't change with elementary row operations.
- `rank(AB) ≤ min(rank A, rank B)`.
- Cayley-Hamilton: `Aⁿ` can be reduced to a polynomial in A of degree ≤ n−1.
- For a 2×2: `A² − tr(A)·A + det(A)·I = 0`.
- `det(A − λI) = 0` is the characteristic equation; its roots are the eigenvalues.
- A matrix is **idempotent (A²=A)** iff all eigenvalues are 0 or 1.
- A matrix is **nilpotent** iff all eigenvalues are 0.
- The number of distinct minors of an m×n matrix is `Σ C(m,k) · C(n,k)`.

---

## 3. Short Notes

```
DETERMINANT PROPERTIES (n×n)
 det(I) = 1
 det(Aᵀ) = det(A)
 det(kA) = kⁿ det(A)
 det(AB) = det(A) det(B)
 det(A⁻¹) = 1/det(A)
 swap 2 rows → −det
 row scaled by k → k·det
 row replaced by row + c·other → det unchanged
 triangular → product of diagonals
 block triangular → product of block dets
 orthogonal → ±1
 skew-symm odd order → 0

ADJOINT & INVERSE
 A · adj(A) = det(A)·I
 A⁻¹ = adj(A)/det(A)
 det(adj A) = det(A)^(n−1)
 adj(adj A) = det(A)^(n−2)·A

TRACE
 tr(A) = Σ aᵢᵢ
 tr(AB) = tr(BA)
 tr(A) = Σ λᵢ
 det(A) = ∏ λᵢ

INVERSE 2×2
 A = [[a,b],[c,d]]
 A⁻¹ = (1/(ad−bc))[[d,−b],[−c,a]]

(AB)ᵀ = BᵀAᵀ
(AB)⁻¹ = B⁻¹A⁻¹

CAYLEY-HAMILTON
 p(λ) = det(λI − A) = 0
 ⇒ p(A) = 0
 use to compute Aⁿ

SPECIAL MATRICES
 symmetric: A=Aᵀ
 skew: Aᵀ=−A (diag = 0)
 orthogonal: AᵀA=I
 hermitian: A=Aᴴ
 idempotent: A²=A
 nilpotent: Aᵏ=0
 involutory: A²=I

RANK
 rank ≤ min(m,n)
 unchanged under elementary ops
 rank(AB) ≤ min(rank A, rank B)
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | det(2×2) = ad − bc | ✅✅ |
| 2 | det(kA) = kⁿ det(A) | ✅✅ |
| 3 | det(AB) = det(A)·det(B) | ✅✅ |
| 4 | det(A⁻¹) = 1/det(A) | ✅✅ |
| 5 | det(Aᵀ) = det(A) | ✅ |
| 6 | det(triangular) = ∏ diagonals | ✅✅ |
| 7 | det(orthogonal) = ±1 | ✅ |
| 8 | det(skew-symm of odd order) = 0 | ✅ |
| 9 | A · adj(A) = det(A) · I | ✅ |
| 10 | det(adj A) = det(A)^(n−1) | ✅ |
| 11 | adj(adj A) = det(A)^(n−2) · A | ✅ |
| 12 | (AB)⁻¹ = B⁻¹A⁻¹ | ✅✅ |
| 13 | (AB)ᵀ = BᵀAᵀ | ✅✅ |
| 14 | tr(A) = Σ λᵢ | ✅✅ |
| 15 | det(A) = ∏ λᵢ | ✅✅ |
| 16 | A² − tr(A)·A + det(A)·I = 0 (2×2 Cayley–Hamilton) | ✅ |
| 17 | A⁻¹ formula for 2×2 | ✅✅ |

### Tricks

- **Det shortcut for upper/lower triangular:** product of diagonals — even ignore zeros above/below.
- **Add constant times row to another:** det unchanged. Use to triangulate quickly.
- **Identical rows ⇒ det = 0** — useful inspection.
- **Determinant of block matrices** with zero block: `det(diag(A,B)) = det(A)·det(B)`.
- **For determinant of (A + kI):** find eigenvalues of A; new eigenvalues = λᵢ + k; det = ∏(λᵢ + k).
- **Cayley-Hamilton trick** for higher powers: reduce Aⁿ using `Aⁿ = c₁A^(n−1) + … + cₙI` from char poly.
- **Sum of all minors** = a useful but rare quantity; appears in Vandermonde-like questions.
- **Rotation matrices have det = +1**; reflection has det = −1.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Let A be a 4×4 matrix with determinant 5. Then det(2A) = ?
**Solution.** det(kA) = kⁿ det(A) = 2⁴ · 5 = 80.
**Answer: 80.**

### Q2. (GATE CSE 2014)
The product of all eigenvalues of a 3×3 matrix A is given by:
**Solution.** det(A).

### Q3. (GATE CSE 2016)
Suppose A is a 4×4 matrix with det(A) = 4. Then det(adj(A)) is:
**Solution.** det(adj A) = det(A)^(n−1) = 4³ = 64.

### Q4. (GATE CSE 2013)
Let A be a 3×3 matrix with eigenvalues 1, −1, 2. Then det(A²) = ?
**Solution.** det(A) = 1·(−1)·2 = −2; det(A²) = 4.

### Q5. (GATE CSE 2015)
The trace and determinant of the matrix `[[2,1],[3,4]]` are:
**Solution.** tr = 6; det = 8 − 3 = 5.

### Q6. (GATE CSE 2009)
If A is a non-singular n×n matrix and B = adj(A), then adj(B) = ?
**Solution.** adj(adj A) = det(A)^(n−2) · A.

### Q7. (GATE CSE 2008)
Let A be a 3×3 matrix with rank 2. Then det(A) is:
**Solution.** Rank < 3 ⇒ det = 0.

### Q8. (GATE CSE 2010)
The eigenvalues of an orthogonal matrix have absolute value:
**Solution.** 1.

### Q9. (GATE CSE 2018)
Let A be a 5×5 invertible matrix. The det(A · A⁻¹) = ?
**Solution.** det(I) = 1.

### Q10. (GATE CSE 2020)
The trace of `[[1,2],[3,4]] · [[5,6],[7,8]]` is:
**Solution.** Product = `[[19,22],[43,50]]`. Trace = 19 + 50 = 69. (Or use tr(AB) = tr(BA).)

### Q11. (GATE CSE 2007)
For matrices A, B of order 3, if det(A) = 4 and det(B) = 2, find det(2AᵀB⁻¹):
**Solution.** det(2A^T B^{-1}) = 2³ · det(A) · 1/det(B) = 8 · 4 · 1/2 = 16.

### Q12. (GATE CSE 2003)
A is 3×3 skew-symmetric. Then:
**Answer:** det(A) = 0 (odd order).

### Q13. (GATE CSE 2011)
If A² = A and A ≠ 0, A ≠ I, then det(A) = ?
**Solution.** Idempotent ⇒ eigenvalues 0 or 1; if rank < n, det = 0.

### Q14. (GATE CSE 2019)
For matrix A = `[[a,b],[c,d]]`, A² − tr(A)·A + det(A)·I = ?
**Solution.** = 0 (Cayley-Hamilton 2×2).

### Q15. (GATE CSE 2021)
Trace of A⁻¹ where A has eigenvalues λ₁, λ₂, λ₃:
**Solution.** tr(A⁻¹) = 1/λ₁ + 1/λ₂ + 1/λ₃.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Compute det of `[[3,2],[1,4]]`.

**P2.** A is 3×3, det(A) = 6. Find det(3A).

**P3.** Trace of identity Iₙ.

**P4.** Find inverse of `[[2,1],[1,1]]`.

**P5.** Is `[[0,1],[−1,0]]` symmetric, skew, orthogonal, none?

**P6.** Compute (AB)ᵀ for A = `[[1,2]]`, B = `[[3],[4]]`.

**P7.** A is upper triangular with diagonal entries 1, 2, 3. det(A) = ?

**P8.** Trace of A = `[[1,4,7],[2,5,8],[3,6,9]]`?

**P9.** Show that the matrix `[[1,2],[3,4]]` is non-singular.

**P10.** Find x such that `det([[x,2],[3,4]]) = 0`.

### Medium

**P11.** For A = `[[1,2,3],[0,1,4],[0,0,1]]`, find A⁻¹.

**P12.** Show: if A and B are n×n, then `(AB)⁻¹ = B⁻¹A⁻¹`.

**P13.** A is 4×4, det(A) = 3. Find det(adj(A)) and det(adj(adj(A))).

**P14.** Verify Cayley-Hamilton for A = `[[2,1],[1,2]]`.

**P15.** Find determinant of `[[1,1,1],[a,b,c],[a²,b²,c²]]` (Vandermonde).

**P16.** A is symmetric and orthogonal. What can A² be?

**P17.** Show: tr(AB) = tr(BA).

**P18.** A is 3×3 with eigenvalues 2, 3, 5. Find det(A) and tr(A).

**P19.** A is nilpotent of order 3 (A³ = 0). Eigenvalues of A?

**P20.** Find rank of `[[1,2,3],[2,4,6],[3,6,9]]`.

### Hard

**P21.** Prove det(adj A) = det(A)^(n−1).

**P22.** A is 3×3 idempotent (A² = A). Possible values of det(A)?

**P23.** Compute A^10 for A = `[[1,1],[0,1]]` using a power-of-shear shortcut.

**P24.** A is 3×3 with characteristic polynomial λ³ − 6λ² + 11λ − 6. Find A⁻¹ using Cayley-Hamilton.

**P25.** Compute determinant of `[[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]`.

**P26.** Show: for a 3×3 orthogonal matrix Q, det(Q − I) = 0 if det(Q) = 1 (i.e., Q is a rotation).

**P27.** Find determinant of the n×n matrix with all 1's, except 2's on the diagonal.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 12 − 2 = 10 | direct |
| P2 | 27 · 6 = 162 | 3³ |
| P3 | n | sum of n ones |
| P4 | (1/(2−1))[[1,−1],[−1,2]] = [[1,−1],[−1,2]] | adj/det |
| P5 | Orthogonal & skew-symmetric | Qᵀ = −Q, QᵀQ = I |
| P6 | A·B = [[11]]; (AB)ᵀ = [[11]] | scalar |
| P7 | 6 | product of diagonals |
| P8 | 1+5+9 = 15 | trace |
| P9 | det = −2 ≠ 0 | direct |
| P10 | x = 3/2 | 4x − 6 = 0 |
| P11 | `[[1,−2,5],[0,1,−4],[0,0,1]]` | back-substitution / formula |
| P12 | (AB)(B⁻¹A⁻¹) = A·I·A⁻¹ = I | direct |
| P13 | det(adj A) = 27; det(adj(adj A)) = det(A)^((n−1)²) = 3⁹ | recurrence |
| P14 | A² − tr(A)·A + det(A)·I = A² − 4A + 3I; verify | direct |
| P15 | (b−a)(c−a)(c−b) | Vandermonde |
| P16 | A² = I (involutory) | A=Aᵀ and A·Aᵀ=I ⇒ A²=I |
| P17 | (AB)ᵢᵢ = Σ aᵢⱼ bⱼᵢ; sum over i,j matches (BA)ⱼⱼ | swap order |
| P18 | det = 30, tr = 10 | product / sum |
| P19 | All zero | nilpotent ⇒ all λ=0 |
| P20 | 1 | rows are multiples |
| P21 | A · adj(A) = det(A)·I; take det of both sides | det manipulation |
| P22 | 0 or 1 | eigenvalues 0 or 1 |
| P23 | Aⁿ = `[[1,n],[0,1]]` | shear matrix |
| P24 | A⁻¹ = (1/6)(A² − 6A + 11I) | Cayley-Hamilton |
| P25 | 0 | rows linearly dependent (consecutive) |
| P26 | Q has eigenvalue 1; Q − I singular ⇒ det = 0 | rotation has fixed axis |
| P27 | Use rank-1 update: M = J + I; det = (n+1) | rank-1 + I formula |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | det(A + B) = det(A) + det(B) | False. Determinant is **not** linear in matrices. |
| 2 | det(kA) = k det(A) | False. det(kA) = kⁿ det(A) for n×n. |
| 3 | (AB)⁻¹ = A⁻¹ B⁻¹ | Reverse: B⁻¹ A⁻¹. |
| 4 | (AB)ᵀ = AᵀBᵀ | Reverse: BᵀAᵀ. |
| 5 | Forgetting that det(A) = 0 ⇒ no inverse | Singular ⇔ rank < n. |
| 6 | Using row-swap without sign flip | Each swap negates det. |
| 7 | Treating skew-symm even-order as singular | Even order can be non-singular. |
| 8 | Forgetting orthogonal eigenvalues have \|λ\|=1 | Real orthogonal: λ ∈ {±1, complex on unit circle}. |
| 9 | Treating tr(A·B) ≠ tr(B·A) | Always equal, even when A·B ≠ B·A. |
| 10 | Confusing minor with cofactor | Cofactor = (−1)^(i+j) · minor. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "det(kA)" | kⁿ · det(A). |
| "det(AB)" | det(A) · det(B). |
| "Find det of triangular matrix" | Product of diagonals. |
| "Skew-symmetric, odd order" | det = 0. |
| "A is orthogonal" | det = ±1, eigenvalues on unit circle. |
| "A² = A" (idempotent) | eigenvalues ∈ {0, 1}. |
| "A² = I" (involutory) | eigenvalues ∈ {±1}. |
| "Aᵏ = 0" (nilpotent) | All eigenvalues = 0; det = 0. |
| "Find det of large structured matrix" | Row-reduce or block decomposition. |
| "Compute Aⁿ" | Cayley-Hamilton or diagonalization. |
| "Cofactor / adjoint formula" | adj(A) · A = det(A) · I. |
| "Trace = sum, det = product" | Both refer to eigenvalues. |

---

## 9. Quick Revision

```
det(2×2 [[a,b],[c,d]]) = ad − bc
det(I)=1   det(Aᵀ)=det(A)
det(kA) = kⁿ det(A)
det(AB) = det(A) det(B)
det(A⁻¹) = 1/det(A)

Triangular: det = ∏ diagonal
Orthogonal: det = ±1
Skew-symm odd: det = 0

(AB)⁻¹ = B⁻¹A⁻¹
(AB)ᵀ = BᵀAᵀ

A · adj(A) = det(A) · I
A⁻¹ = adj(A) / det(A)
det(adj A) = det(A)^(n−1)
adj(adj A) = det(A)^(n−2) · A

tr(A) = Σ aᵢᵢ = Σ λᵢ
det(A) = ∏ λᵢ
tr(AB) = tr(BA)

CAYLEY-HAMILTON
 char poly: p(λ) = det(λI − A)
 p(A) = 0
 2×2: A² − tr·A + det·I = 0

SPECIAL
 idempotent A²=A : λ ∈ {0,1}
 involutory A²=I : λ ∈ {±1}
 nilpotent Aᵏ=0  : all λ = 0
 orthogonal QᵀQ=I : |λ|=1
```
