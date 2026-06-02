# Set Theory, Relations & Functions

> Subject: Engineering Mathematics → Discrete Mathematics
> GATE weight: **2–5 marks** every year. Prerequisite for graphs, DBMS FDs, automata equivalence.

---

## 1. Concept Explanation

### 1.1 Set — basics

A **set** is an unordered collection of distinct elements.

- Notation: `A = {1, 2, 3}` or `A = {x | P(x)}` (set-builder).
- Empty set `∅` (or `{}`): unique. `|∅| = 0`. `∅ ⊆ A` for every set A.
- **Cardinality** `|A|` — number of elements.
- **Power set** `P(A)` — set of all subsets. `|P(A)| = 2^|A|`.

### 1.2 Set Operations

| Operation | Symbol | Definition |
|---|---|---|
| Union | A ∪ B | x ∈ A ∨ x ∈ B |
| Intersection | A ∩ B | x ∈ A ∧ x ∈ B |
| Difference | A − B (or A \ B) | x ∈ A ∧ x ∉ B |
| Symmetric Diff | A △ B | (A − B) ∪ (B − A) |
| Complement | Aᶜ or A' | x ∉ A (rel. to universe U) |
| Cartesian product | A × B | { (a,b) : a ∈ A, b ∈ B }. `|A×B| = |A|·|B|`. |

### 1.3 Inclusion–Exclusion

For 2 sets: `|A ∪ B| = |A| + |B| − |A ∩ B|`.

For 3: `|A ∪ B ∪ C| = |A|+|B|+|C| − |A∩B| − |B∩C| − |A∩C| + |A∩B∩C|`.

General: alternating signs over all non-empty intersections.

### 1.4 Relations

A **(binary) relation** R on A × B is a subset of A × B. `(a,b) ∈ R` is written `a R b`.

- Number of relations on A (|A|=n): `2^(n²)`.
- **Domain** of R = {a : ∃b, (a,b) ∈ R}. **Range** = {b : ∃a, (a,b) ∈ R}.

### 1.5 Properties of Relations on a set A

| Property | Definition |
|---|---|
| Reflexive | ∀a ∈ A, (a,a) ∈ R |
| Irreflexive | ∀a ∈ A, (a,a) ∉ R |
| Symmetric | (a,b) ∈ R ⇒ (b,a) ∈ R |
| Antisymmetric | (a,b) ∈ R ∧ (b,a) ∈ R ⇒ a = b |
| Asymmetric | (a,b) ∈ R ⇒ (b,a) ∉ R (irreflexive + antisym) |
| Transitive | (a,b),(b,c) ∈ R ⇒ (a,c) ∈ R |

**Equivalence relation** = reflexive + symmetric + transitive. Partitions A into **equivalence classes**.

**Partial order (POSET)** = reflexive + antisymmetric + transitive.
**Total order** = partial order + comparability (∀a,b: aRb or bRa).

### 1.6 Counting relations

|A|=n. Then:
- Total relations: `2^(n²)`
- Reflexive: `2^(n² − n)` (n diagonal forced T)
- Symmetric: `2^(n(n+1)/2)` (n diagonal + (n²−n)/2 upper triangle)
- Antisymmetric: `2ⁿ · 3^(n(n−1)/2)`  (diagonal free; each off-diag pair has 3 choices: only (a,b), only (b,a), or neither)
- Reflexive + Symmetric: `2^(n(n−1)/2)`
- Equivalence relations: **Bell number Bₙ** (B₁=1, B₂=2, B₃=5, B₄=15, B₅=52)

### 1.7 Closures

The **closure** of R under property P = smallest superset of R that satisfies P.

- Reflexive closure: `R ∪ Δ` where Δ = {(a,a)}.
- Symmetric closure: `R ∪ R⁻¹`.
- Transitive closure (`R⁺`): union of `R, R², R³, …` until no change. Computed via **Warshall's algorithm** (O(n³)).

### 1.8 Functions

A **function** f: A → B is a relation where every a ∈ A is mapped to **exactly one** b ∈ B.

| Type | Definition |
|---|---|
| Injective (one-one) | f(a₁) = f(a₂) ⇒ a₁ = a₂ |
| Surjective (onto) | ∀b ∃a, f(a) = b |
| Bijective | injective + surjective |

**Counting (|A| = m, |B| = n):**
- Total functions: `nᵐ`
- Injective (need m ≤ n): `n!/(n−m)! = P(n, m)`
- Surjective (need m ≥ n): `Σ_{k=0}^{n} (−1)ᵏ C(n,k) (n−k)ᵐ` (Stirling-derived)
- Bijective (need m = n): `n!`

### 1.9 Composition & Inverse

- `(g ∘ f)(x) = g(f(x))`
- `f⁻¹` exists iff f is bijective.
- `(f ∘ g)⁻¹ = g⁻¹ ∘ f⁻¹` (reverse order).

### 1.10 Hasse Diagram & POSETs

For a partial order, the **Hasse diagram** plots elements with edges between cover relations (no transitive shortcuts). Used to find:

- **Maximal / Minimal** elements (no element above / below).
- **Greatest / Least** element (above / below *every* other).
- **Upper / Lower bounds** of a subset; **LUB (sup)** / **GLB (inf)**.
- **Lattice** = POSET where every pair has LUB and GLB.

### 1.11 Pigeonhole Principle

If n+1 objects are placed in n boxes, some box has ≥ 2 objects. Generalized: if N objects in k boxes, some box has ≥ ⌈N/k⌉.

> **Summary:** Master inclusion-exclusion, the 6 relation properties, function counting, equivalence partitions (Bell numbers), and Hasse diagrams. Almost every GATE PYQ on this topic reduces to one of these.

---

## 2. Important Points

- `|P(A)| = 2^|A|`. **Every** set has the empty set as a subset and itself as a subset.
- `A ⊆ B ⇔ A ∪ B = B ⇔ A ∩ B = A`.
- **De Morgan for sets:** `(A ∪ B)ᶜ = Aᶜ ∩ Bᶜ`; `(A ∩ B)ᶜ = Aᶜ ∪ Bᶜ`.
- `A − B = A ∩ Bᶜ`. **Difference is not commutative.**
- A relation can be **both symmetric and antisymmetric** (only when R ⊆ Δ — the diagonal).
- Empty relation on empty set is reflexive, symmetric, antisymmetric, transitive — vacuously.
- The **identity relation** Δ = {(a,a)} is an equivalence relation **and** a partial order.
- Equivalence classes either coincide or are disjoint — they **partition** the set.
- `# equivalence relations on n-set = Bₙ` (Bell number) **= # partitions of an n-set**.
- A function is well-defined ⇔ "vertical line test" — every input has *exactly one* output.
- Composition of injections is injection; composition of surjections is surjection. Composition of bijections is bijection.
- For finite sets of equal size: f injective ⇔ f surjective ⇔ f bijective. (Pigeonhole.)
- **Lattice** ⇒ POSET, but not every POSET is a lattice (must have LUB and GLB for *every* pair).
- For an antisymmetric relation, the diagonal is free → each off-diag *pair* contributes a factor of 3.

---

## 3. Short Notes

```
SETS
 ∅ ⊆ A  for all A
 |P(A)| = 2ⁿ
 |A ∪ B| = |A|+|B|−|A∩B|       (PIE for 2)
 |A ∪ B ∪ C| = Σ|·| − Σ|·∩·| + |A∩B∩C|
 De Morgan: (A∪B)ᶜ=Aᶜ∩Bᶜ ; (A∩B)ᶜ=Aᶜ∪Bᶜ
 A−B = A ∩ Bᶜ
 |A × B| = |A|·|B|

RELATIONS  (|A|=n)
 Total                : 2^(n²)
 Reflexive            : 2^(n²−n)
 Symmetric            : 2^(n(n+1)/2)
 Antisymmetric        : 2ⁿ · 3^(n(n−1)/2)
 Reflexive+Symmetric  : 2^(n(n−1)/2)
 Equivalence          : Bₙ (Bell)   1,2,5,15,52,203,…

PROPERTIES (mnemonic: R-I-S-A-T)
 Reflexive : ∀a (a,a)∈R
 Irrefl    : ∀a (a,a)∉R
 Symm      : aRb ⇒ bRa
 AntiSymm  : aRb∧bRa ⇒ a=b
 Trans     : aRb∧bRc ⇒ aRc
 Equivalence = R + S + T
 Partial Order = R + AS + T
 Total Order = PO + comparable

FUNCTIONS  (f: A→B, |A|=m, |B|=n)
 Total      : nᵐ
 Injective  : n!/(n−m)!     (m ≤ n)
 Surjective : Σ(−1)ᵏ C(n,k)(n−k)ᵐ
 Bijective  : n! (only when m=n)
 Bijective ⇒ inverse exists
 (g∘f)(x) = g(f(x))
 (f∘g)⁻¹ = g⁻¹∘f⁻¹

CLOSURES
 R-closure: R ∪ Δ
 S-closure: R ∪ R⁻¹
 T-closure: Warshall O(n³)

HASSE / LATTICE
 Lattice = POSET with LUB & GLB for every pair.
 Distributive Lattice: a∧(b∨c)=(a∧b)∨(a∧c)
 Boolean Lattice: distributive + complemented

PIGEONHOLE
 N objects, k boxes ⇒ some box has ⌈N/k⌉.
```

---

## 4. Formulas / Tricks

| # | Identity | Memorize Cold? |
|---|---|---|
| 1 | `|P(A)| = 2^|A|` | ✅ |
| 2 | `|A ∪ B| = |A|+|B|−|A∩B|` (PIE-2) | ✅✅ |
| 3 | `|A ∪ B ∪ C| = Σ|·|−Σ|·∩·|+|A∩B∩C|` | ✅✅ |
| 4 | `|A × B| = |A|·|B|` | ✅ |
| 5 | `# relations on n-set = 2^(n²)` | ✅✅ |
| 6 | `# reflexive = 2^(n²−n)` | ✅ |
| 7 | `# symmetric = 2^(n(n+1)/2)` | ✅ |
| 8 | `# antisymmetric = 2ⁿ·3^(n(n−1)/2)` | ✅ |
| 9 | `# equivalence relations = Bₙ` (1,2,5,15,52,...) | ✅✅ |
| 10 | `# functions A→B = nᵐ` | ✅ |
| 11 | `# injective = n·(n−1)·…·(n−m+1)` | ✅ |
| 12 | `# surjective = Σ(−1)ᵏ C(n,k)(n−k)ᵐ` | ✅ |
| 13 | `# bijective on n = n!` | ✅ |
| 14 | `# partitions of n-set = Bₙ` (= equivalence relations) | ✅ |
| 15 | `# permutations with no fixed point (derangements) = !n = n! Σ(−1)ᵏ/k!` | ✅ |

### Tricks

- **"Number of relations" trap:** read carefully — relations *on* A means subsets of A×A (use n²). Relations *from* A *to* B uses |A|·|B|.
- **Equivalence ↔ partition** — same count. If a question asks # ways to partition a set, that's Bₙ.
- **Symmetric AND antisymmetric** — must be a subset of the diagonal — count = 2ⁿ.
- **Reflexive AND irreflexive** — impossible unless A = ∅.
- For "f from A to B is ___" questions, always check m vs n first:
  - injective needs m ≤ n
  - surjective needs m ≥ n
  - bijective needs m = n
- **Quick Stirling-derived shortcut for surjections** when |B| is small:
  - 2 onto: `2ᵐ − 2`
  - 3 onto: `3ᵐ − 3·2ᵐ + 3`
  - 4 onto: `4ᵐ − 4·3ᵐ + 6·2ᵐ − 4`

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2018, 1 mark)
Let N be the set of natural numbers. Consider the binary relation R = {(x,y) | y = x + 5 and x, y ∈ N}. Which of the following is true about R?
(A) Reflexive
(B) Symmetric
(C) Transitive
(D) Anti-symmetric

**Solution.** (1,1)∉R → not reflexive. (1,6)∈R but (6,1)∉R → not symmetric. (1,6),(6,11)∈R but (1,11)∉R (since 11≠1+5) → not transitive. Antisymmetric: (a,b)∈R ⇒ b=a+5; can't have (b,a)∈R. So vacuously antisymmetric.
**Answer: (D).** *(Pattern: vacuous antisymmetry.)*

### Q2. (GATE CSE 2017)
Let R be a relation on the set N of positive integers such that (a,b) ∈ R iff a² + b² is even. Which is correct?
(A) R is reflexive and transitive but not symmetric
(B) Reflexive and symmetric, not transitive
(C) Symmetric and transitive, not reflexive
(D) Equivalence relation

**Solution.** a² + a² = 2a² always even ⇒ reflexive. Symmetric: a² + b² = b² + a² ⇒ symmetric. Transitive: if a² + b² even and b² + c² even, both a, b same parity and b, c same parity → a, c same parity → a²+c² even. Yes ⇒ transitive.
**Answer: (D).** *(Pattern: parity-based equivalence.)*

### Q3. (GATE CSE 2014)
Let X and Y be finite sets and f: X → Y be a function. Which one of the following statements is TRUE?
(A) For any A, B ⊆ X, f(A∪B) = f(A) ∪ f(B)
(B) For any A, B ⊆ X, f(A∩B) = f(A) ∩ f(B)
(C) For any A, B ⊆ X, |f(A∪B)| = |f(A)| + |f(B)|
(D) For any A ⊆ X, B ⊆ Y, f(f⁻¹(B)) = B

**Solution.** (A) ✅ — image distributes over union.
(B) ❌ — can have f(a)=f(b) for a∈A, b∈B with A∩B=∅.
(C) ❌ — overcounts overlap.
(D) ❌ — only ⊆ B in general.
**Answer: (A).** *(Pattern: image-of-union always distributes; intersection doesn't.)*

### Q4. (GATE CSE 2005)
Let A be the set of all non-singular matrices over reals and let * be matrix multiplication. Then
(A) A is closed under *, but ⟨A,*⟩ is not a semigroup
(B) ⟨A,*⟩ is a semigroup but not a monoid
(C) ⟨A,*⟩ is a monoid but not a group
(D) ⟨A,*⟩ is a group but not an abelian group

**Solution.** Closed (product of non-singular is non-singular), associative ⇒ semigroup. Identity I exists ⇒ monoid. Inverse exists for every non-singular ⇒ group. Not commutative ⇒ not abelian.
**Answer: (D).** *(Pattern: structure-test ladder.)*

### Q5. (GATE CSE 2007)
A partial order ≤ on the set S = {a, b, c, d} is shown by the Hasse diagram with cover relations a ≤ b, a ≤ c, b ≤ d, c ≤ d. The number of total orders on S consistent with this partial order (linear extensions) is:
(A) 1 (B) 2 (C) 4 (D) 6

**Solution.** "Diamond" poset. a first, d last; middle two (b, c) in either order ⇒ 2.
**Answer: (B).** *(Pattern: linear extensions of a poset.)*

### Q6. (GATE CSE 2008)
The number of equivalence relations on the set {1, 2, 3, 4} is:
(A) 4 (B) 15 (C) 16 (D) 24

**Solution.** Bell number B₄ = 15.
**Answer: (B).** *(Pattern: Bell number lookup.)*

### Q7. (GATE CSE 2015)
The total number of binary relations on {1, 2, …, n}, that are both reflexive and symmetric, is:
(A) `2^(n(n−1)/2)`  (B) `2^(n²)`  (C) `2^(n(n+1)/2)`  (D) `2ⁿ`

**Solution.** Diagonal forced (reflexive); upper-triangle of size `n(n−1)/2` is free (each entry forces its mirror).
**Answer: (A).** *(Pattern: count-by-property.)*

### Q8. (GATE CSE 2016)
A function f: N⁺ → N⁺ defined as f(n) = (smallest prime factor of n) is:
(A) one-one and onto
(B) one-one but not onto
(C) onto but not one-one
(D) neither one-one nor onto

**Solution.** f(2) = f(4) = 2 ⇒ not one-one. Image = primes ∪ {1?} — actually 1 has no prime factor; convention may exclude 1 from domain. Image = primes only ⇒ not onto N⁺.
**Answer: (D).** *(Pattern: smallest-prime-factor.)*

### Q9. (GATE CSE 2013)
Function f: {0,1}ⁿ → {0,1}ⁿ is bijective iff:
(A) it is one-one
(B) it is onto
(C) (A) or (B)
(D) (A) and (B)

**Solution.** Finite sets of equal size: injective ⇔ surjective ⇔ bijective.
**Answer: (C).** *(Pattern: pigeonhole on equal-finite domains.)*

### Q10. (GATE CSE 2009)
The minimum number of equivalence relations required for the partition {{a,b},{c}} on {a,b,c} is:
(A) 1 (B) 2 (C) 3 (D) 4

**Solution.** Each partition corresponds to **exactly one** equivalence relation.
**Answer: (A).** *(Pattern: partition–equivalence correspondence.)*

### Q11. (GATE CSE 2019)
Suppose Y is distributed uniformly over {1,…,N}. Let X = max(Y, k) for fixed k. The number of distinct values X takes is _.
*(Counts image of a function — `N − k + 1` if k ≤ N else 1.)*

### Q12. (GATE CSE 2003)
Let A and B be sets with |A| = m, |B| = n. Number of one-one functions from A to B (m ≤ n):
**Answer:** `n(n−1)(n−2)…(n−m+1) = n!/(n−m)!`. *(Pattern: P(n,m).)*

### Q13. (GATE CSE 2012)
The number of onto functions from a set of m elements to a set of n elements (m ≥ n) is:
**Answer:** `Σ_{k=0}^{n} (−1)ᵏ C(n,k)(n−k)ᵐ`. *(Pattern: inclusion–exclusion on surjections.)*

### Q14. (GATE CSE 2006)
Let R be a binary relation on A. Define R² = R∘R. R is transitive iff:
(A) R² ⊆ R (B) R ⊆ R² (C) R² = R (D) R ∪ R² = R

**Solution.** (a,c)∈R² means ∃b: (a,b),(b,c)∈R. Transitive demands then (a,c)∈R, i.e., R² ⊆ R.
**Answer: (A).** *(Pattern: transitivity = composition closure.)*

### Q15. (GATE CSE 2021)
The number of distinct minimum spanning trees... *(see graph_theory.md — referenced for cross-topic linkage.)*

---

## 6. Practice Questions (20+)

### Easy

**P1.** |A| = 5. How many subsets does A have? How many proper non-empty subsets?

**P2.** Compute `|A ∪ B|` if `|A| = 30, |B| = 20, |A ∩ B| = 8`.

**P3.** A = {1,2,3}, B = {2,3,4}. Find A − B, B − A, A △ B.

**P4.** Let R on {1,2,3} be {(1,1),(2,2),(3,3)}. Reflexive? Symmetric? Transitive?

**P5.** Determine if `R = {(a,b) : a ≤ b}` on integers is a partial order.

**P6.** How many functions are there from a 3-set to a 4-set?

**P7.** Is the function f(x) = x² from ℝ to ℝ injective? Surjective?

**P8.** Number of equivalence relations on a 3-element set.

**P9.** A 5-element set; how many reflexive relations?

**P10.** State whether `R = {(a,b) : a − b is rational}` on ℝ is an equivalence relation.

### Medium

**P11.** In a class of 60: 25 take Math, 30 Physics, 20 Chem, 10 Math+Phys, 8 Phys+Chem, 5 Math+Chem, 3 all three. How many take none?

**P12.** Number of relations on a 4-set that are symmetric and reflexive.

**P13.** Number of antisymmetric relations on a 3-set.

**P14.** Find the transitive closure of R = {(1,2),(2,3),(3,4)} on {1,2,3,4}.

**P15.** f: ℝ → ℝ, f(x) = (x−1)/(x+1), defined for x ≠ −1. Is f injective? Find f⁻¹.

**P16.** Number of onto functions from a 4-set to a 2-set.

**P17.** Number of onto functions from a 5-set to a 3-set.

**P18.** Show that the relation `R = {(x,y) : x ≡ y (mod 5)}` on ℤ is an equivalence relation. How many equivalence classes?

**P19.** A poset has Hasse diagram: a < b < d, a < c < d. Find LUB({b,c}) and GLB({b,c}).

**P20.** How many partitions of a 5-element set are there?

### Hard

**P21.** Let A = {1,2,…,n}. How many relations on A are both equivalence relations and partial orders?

**P22.** Number of functions f: {1,…,n} → {1,…,n} such that f(f(x)) = x (involutions).

**P23.** Let f: A → B and g: B → A satisfy g ∘ f = id_A. Show f is injective and g is surjective. Are f and g bijections?

**P24.** Number of distinct equivalence relations on {1,2,3,4,5} with exactly 3 equivalence classes.

**P25.** A relation R on a set of size n is reflexive and antisymmetric. Maximum number of pairs in R?

**P26.** Prove: if f: A → B is a bijection then f⁻¹: B → A exists and is unique.

**P27.** Show: any chain in the divisibility poset on {1,2,…,2ⁿ} has length ≤ n + 1.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 32 subsets; 30 proper non-empty | 2⁵ = 32; subtract ∅ and A |
| P2 | 42 | PIE |
| P3 | A−B={1}, B−A={4}, A△B={1,4} | direct |
| P4 | Yes / Yes / Yes (identity) | identity is equivalence + PO |
| P5 | Yes (refl + antisym + trans) | total order in fact |
| P6 | 4³ = 64 | nᵐ |
| P7 | Neither | (−1)²=(1)² ; range = [0,∞) |
| P8 | B₃ = 5 | partitions: 1 single, 3 two-class, 1 three-class — total 5 |
| P9 | 2^(25−5) = 2²⁰ | n²−n with n=5 |
| P10 | Yes (refl, sym, trans on rationals as equiv) | difference is rational |
| P11 | 60 − (25+30+20−10−8−5+3) = 60 − 55 = 5 | 3-set PIE |
| P12 | 2^(C(4,2)) = 2⁶ = 64 | n(n−1)/2 = 6 |
| P13 | 2³·3³ = 216 | 2ⁿ·3^(C(n,2)) |
| P14 | {(1,2),(1,3),(1,4),(2,3),(2,4),(3,4)} | Warshall |
| P15 | Injective on domain. f⁻¹(y) = (1+y)/(1−y) | solve y = (x−1)/(x+1) |
| P16 | 2⁴ − 2 = 14 | total − constant |
| P17 | 3⁵ − 3·2⁵ + 3 = 243 − 96 + 3 = 150 | 3-onto formula |
| P18 | 5 classes | residues 0,1,2,3,4 |
| P19 | LUB = d; GLB = a | diamond |
| P20 | B₅ = 52 | Bell |
| P21 | Only the identity (Δ) qualifies — equiv ∧ PO ⇒ symm ∧ antisymm ⇒ R⊆Δ; reflexive ⇒ R=Δ. So **1**. | both symm + antisym |
| P22 | Σ_{k=0}^{⌊n/2⌋} C(n,2k)·(2k)!/(2ᵏ k!) | involutions count |
| P23 | f injective (g∘f = id), g surjective. Not necessarily bijections (e.g., A=ℕ, B=ℕ, f(n)=2n, g(n)=⌊n/2⌋) | left/right inverse |
| P24 | S(5,3) = 25 | Stirling 2nd kind |
| P25 | Diagonal (n) + at most C(n,2) (one direction per pair) = `n + n(n−1)/2 = n(n+1)/2` | total order |
| P26 | Standard proof: define f⁻¹(b) = unique a with f(a)=b; uniqueness of bijection inverse | bijection ⇒ inverse |
| P27 | Each step at least doubles; max length ⌊log₂ 2ⁿ⌋ + 1 = n + 1 | chain in divisibility |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing "from A to B" with "on A" | "On A" → relations in A×A, count uses n². |
| 2 | Forgetting empty set is a subset of every set | When counting subsets, always include ∅ in 2ⁿ. |
| 3 | Using ∀ with ∧ for "all X are Y" | Always use →. (See `propositional_logic.md`.) |
| 4 | Treating asymmetric = not symmetric | Asymmetric is *strictly* stronger (irreflexive + antisym). |
| 5 | Counting onto without I-E | Use inclusion–exclusion `Σ(−1)ᵏ C(n,k)(n−k)ᵐ`. |
| 6 | Writing `# antisym = 3^(n(n−1)/2)` and forgetting the `2ⁿ` for diagonal | Diagonal is free (each entry T/F). |
| 7 | Symmetric closure ≠ adding all pairs — only mirrors of existing | `R ∪ R⁻¹`. |
| 8 | Treating composition as commutative | `f ∘ g ≠ g ∘ f` in general. |
| 9 | Equivalence class count ≠ size of set | Classes partition; their **count** = number of distinct classes. |
| 10 | Forgetting `(f ∘ g)⁻¹ = g⁻¹ ∘ f⁻¹` (reverse) | "Last on, first off" — like socks/shoes. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Number of relations on n-set with property P" | Use the count table. Memorize 2^(n²), 2^(n²−n), 2^(n(n+1)/2), Bₙ. |
| "Number of equivalence relations" | Bell number Bₙ. |
| "Number of functions from m-set to n-set" | nᵐ. Adjust for inj/surj/bij. |
| "Number of onto functions" | Inclusion–Exclusion: `Σ(−1)ᵏ C(n,k)(n−k)ᵐ`. |
| "Hasse diagram, find LUB/GLB" | Read upward / downward neighbours. |
| "Linear extensions of poset" | Topological sorts of the DAG. |
| "Closure of R under property" | Smallest superset; transitive closure → Warshall. |
| "Equivalence ⇔ partition" question | Bijection between them — same count. |
| "f²(x) = x" | Involutions — combinatorial sum. |
| "Set difference / symmetric difference identity" | Convert using `A − B = A ∩ Bᶜ`, then standard set-algebra. |

---

## 9. Quick Revision

```
|P(A)| = 2ⁿ
|A∪B| = |A|+|B|−|A∩B|     (PIE-2)
|A∪B∪C| = Σ|·|−Σ|·∩·|+|A∩B∩C|
A−B = A ∩ Bᶜ ;  De Morgan: (A∪B)ᶜ=Aᶜ∩Bᶜ

# rels on n-set     = 2^(n²)
# reflexive         = 2^(n²−n)
# symmetric         = 2^(n(n+1)/2)
# antisym           = 2ⁿ · 3^(n(n−1)/2)
# refl+sym          = 2^(n(n−1)/2)
# equiv = # partit  = Bₙ : 1, 2, 5, 15, 52, 203, …

f: A→B (m,n)
# total fns         = nᵐ
# inj  (m≤n)        = n!/(n−m)!
# surj (m≥n)        = Σ(−1)ᵏ C(n,k)(n−k)ᵐ
# bij  (m=n)        = n!

R+S+T = equivalence (partition into classes)
R+AS+T = partial order
Lattice = poset where every pair has LUB & GLB
Symm + Antisym ⇒ R ⊆ Δ
"Some X are Y"  ∃x (X(x) ∧ Y(x))
"All X are Y"   ∀x (X(x) → Y(x))
Pigeonhole: ⌈N/k⌉ in some box
```
