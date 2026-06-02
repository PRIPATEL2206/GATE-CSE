# Combinatorics

> Subject: Engineering Mathematics → Discrete Mathematics
> GATE weight: **2–4 marks** every year. Counting + recurrences + generating functions.

---

## 1. Concept Explanation

### 1.1 Counting Principles

- **Sum rule:** A or B (disjoint) ⇒ |A| + |B|.
- **Product rule:** A and then B ⇒ |A| · |B|.
- **Bijection rule:** if there's a bijection A → B, |A| = |B|.

### 1.2 Permutations & Combinations

| Quantity | Formula | Meaning |
|---|---|---|
| `n!` | n · (n−1) · … · 1 | total orderings of n distinct items |
| `P(n, r)` | `n!/(n−r)!` | r-permutations of n distinct |
| `C(n, r)` | `n!/(r!(n−r)!)` | r-subsets of n distinct |
| `C(n, r) = C(n, n−r)` | symmetry | |
| `Σ_{r=0}^n C(n,r) = 2ⁿ` | total subsets | |

**Permutations with repetition** of n items where item i appears `nᵢ` times: `n! / (n₁! n₂! … nₖ!)` (multinomial).

### 1.3 Combinations with Repetition (Stars & Bars)

Number of ways to put n identical objects into k distinct boxes:

`C(n + k − 1, k − 1)`  (also `C(n+k−1, n)`)

Equivalently, # non-negative integer solutions to `x₁ + x₂ + … + xₖ = n`.

For positive integer solutions (each xᵢ ≥ 1): `C(n − 1, k − 1)`.

### 1.4 Pigeonhole Principle

- **Basic:** n+1 objects in n boxes ⇒ some box has ≥ 2.
- **Generalized:** N objects in k boxes ⇒ some box has ≥ ⌈N/k⌉.

### 1.5 Inclusion–Exclusion (PIE)

`|A₁ ∪ … ∪ Aₙ| = Σ|Aᵢ| − Σ|Aᵢ∩Aⱼ| + Σ|Aᵢ∩Aⱼ∩Aₖ| − …`

**Applications:**
- Counting onto functions: `Σ_{k=0}^n (−1)ᵏ C(n,k)(n−k)ᵐ`.
- Counting derangements: `Dₙ = n! Σ_{k=0}^n (−1)ᵏ/k!`.
- Counting integers coprime to N (Euler's φ): `φ(N) = N · Π (1 − 1/p)` over prime p|N.

### 1.6 Binomial Theorem & Identities

`(x + y)ⁿ = Σ_{k=0}^n C(n,k) x^(n−k) yᵏ`

| Identity | Form |
|---|---|
| Pascal | `C(n,k) = C(n−1,k) + C(n−1,k−1)` |
| Sum | `Σ C(n,k) = 2ⁿ` |
| Alternating sum | `Σ (−1)ᵏ C(n,k) = 0` (n ≥ 1) |
| Vandermonde | `C(m+n, r) = Σₖ C(m,k) C(n, r−k)` |
| Hockey-stick | `Σ_{i=r}^n C(i, r) = C(n+1, r+1)` |

### 1.7 Multinomial Theorem

`(x₁ + x₂ + … + xₖ)ⁿ = Σ (n! / (n₁!n₂!…nₖ!)) · x₁^n₁ … xₖ^nₖ`, summed over n₁+…+nₖ = n.

### 1.8 Recurrence Relations

A **recurrence** defines aₙ in terms of earlier terms. Solving:

**Linear homogeneous of order k:**
`aₙ = c₁ a_{n−1} + c₂ a_{n−2} + … + cₖ a_{n−k}`

Characteristic equation: `xᵏ = c₁ x^(k−1) + … + cₖ`.

- Distinct roots r₁, …, rₖ: `aₙ = α₁ r₁ⁿ + … + αₖ rₖⁿ`.
- Repeated root r of multiplicity m: contributes `(α₀ + α₁ n + … + α_{m−1} n^(m−1)) rⁿ`.

**Non-homogeneous:**
`aₙ = (homogeneous solution) + (particular solution)`. Guess particular based on RHS form (polynomial → polynomial; rⁿ → n·rⁿ if r is char root).

### 1.9 Common Sequences

| Name | Formula | Recurrence |
|---|---|---|
| Fibonacci | F₀=0, F₁=1, Fₙ = F_{n−1}+F_{n−2} | r² = r + 1 → φ = (1+√5)/2 |
| Catalan | Cₙ = C(2n,n)/(n+1) | Cₙ = Σ Cᵢ C_{n−1−i} |
| Stirling 2nd | S(n,k) = # partitions of n into k blocks | S(n,k)=k·S(n−1,k)+S(n−1,k−1) |
| Bell | Bₙ = Σ S(n,k) | Bₙ₊₁ = Σ C(n,k) Bₖ |
| Derangements | Dₙ ≈ n!/e | Dₙ = (n−1)(D_{n−1}+D_{n−2}) |

### 1.10 Generating Functions

**OGF:** `A(x) = Σ aₙ xⁿ`. Used to encode sequences as power series.

| Sequence | OGF |
|---|---|
| 1, 1, 1, … | 1/(1−x) |
| 1, x, x², … | 1/(1−x) |
| Cₙ Catalan | (1−√(1−4x))/(2x) |
| C(n,k) (n fixed, varying k) | (1+x)ⁿ |

**Useful operations:**
- Multiplication of GFs ⇔ convolution of sequences.
- Differentiation gives multiplied-by-n sequence.

### 1.11 Catalan Numbers

`Cₙ = C(2n,n)/(n+1)`. Counts:
- # binary trees with n internal nodes
- # ways to triangulate (n+2)-gon
- # balanced parenthesis with n pairs
- # monotonic paths from (0,0) to (n,n) not crossing diagonal
- # non-crossing chord diagrams on 2n points

### 1.12 Stirling & Bell

- `S(n, k)` = partitions of [n] into k non-empty blocks.
- `Bₙ = Σ_{k=1}^n S(n, k)` = total partitions.
- # surjections from m-set to n-set = `n! · S(m, n)`.

### 1.13 Master Theorem (cross-link to Algorithms)

For T(n) = a T(n/b) + f(n):
- If f(n) = O(n^(log_b a − ε)): T = Θ(n^(log_b a)).
- If f(n) = Θ(n^(log_b a)): T = Θ(n^(log_b a) log n).
- If f(n) = Ω(n^(log_b a + ε)): T = Θ(f(n)).

> **Summary:** counting = sum/product/PIE; arrangements = permutations/multinomial; placements = stars-bars; sequences = recurrences/generating functions/Catalan/Stirling/Bell.

---

## 2. Important Points

- `C(n, r) = C(n, n−r)` — symmetry. Use to simplify.
- `Σ C(n,k) = 2ⁿ`, `Σ k·C(n,k) = n·2^(n−1)`, `Σ k²·C(n,k) = n(n+1)·2^(n−2)`.
- # non-neg integer solutions to `Σxᵢ = n`, k variables = `C(n+k−1, k−1)`.
- # positive solutions = `C(n−1, k−1)`.
- # permutations of n with k specific items together: treat as 1 super-item ⇒ `(n−k+1)! · k!`.
- # circular permutations of n distinct: `(n−1)!`. With reflection symmetry (necklaces): `(n−1)!/2`.
- **Derangement count Dₙ** ≈ n!/e ≈ 0.3679 · n!. Recurrence `Dₙ = (n−1)(D_{n−1} + D_{n−2})`.
- **Catalan Cₙ:** 1, 1, 2, 5, 14, 42, 132, 429, …
- **Bell Bₙ:** 1, 1, 2, 5, 15, 52, 203, 877, …
- # surjections m-set → n-set = `n! · S(m, n)`.
- # ways to distribute n distinct balls into k distinct boxes (some empty allowed): `kⁿ`.
- # ways to distribute n identical balls into k distinct boxes: stars-bars.
- # ways to distribute n distinct balls into k identical boxes: `S(n,1) + … + S(n,k)`.
- For Fibonacci: `Fₙ = (φⁿ − ψⁿ)/√5`, where φ = (1+√5)/2, ψ = (1−√5)/2.
- For homogeneous linear recurrences with distinct char roots, # of independent solutions = order.
- **Master Theorem doesn't always apply** — Akra–Bazzi covers more cases.

---

## 3. Short Notes

```
PERMUTATIONS / COMBINATIONS
 P(n,r) = n!/(n−r)!
 C(n,r) = n!/(r!(n−r)!)
 C(n,r) = C(n,n−r)
 Σ C(n,k) = 2ⁿ
 Pascal: C(n,k) = C(n−1,k)+C(n−1,k−1)

MULTINOMIAL
 (x₁+...+xₖ)ⁿ = Σ n!/(n₁!…nₖ!) · ∏ xᵢ^nᵢ

STARS & BARS  (Σ xᵢ = n, k vars)
 ≥0 sols : C(n+k−1, k−1)
 ≥1 sols : C(n−1, k−1)

CIRCULAR perms of n distinct: (n−1)!

PIGEONHOLE: ⌈N/k⌉

PIE
 |A∪B∪C| = Σ−Σ+Σ
 onto fns m→n: Σ(−1)ᵏ C(n,k)(n−k)ᵐ
 derangements: Dₙ = n! Σ(−1)ᵏ/k!  ≈ n!/e
 Euler φ(N) = N·∏(1−1/p)

BINOMIAL IDENTITIES
 Vandermonde: C(m+n,r) = Σ C(m,k)C(n,r−k)
 Hockey-stick: Σ_{i=r}^n C(i,r) = C(n+1,r+1)

RECURRENCES (linear, homog., constant coeff.)
 char eq → roots → solution
 distinct rᵢ : aₙ = Σ αᵢ rᵢⁿ
 root r mult m: (α₀+α₁n+...+α_{m−1}n^(m−1)) rⁿ

CATALAN  Cₙ = C(2n,n)/(n+1)
 1,1,2,5,14,42,132,429,...
 trees, parens, paths

STIRLING(2nd)  S(n,k) partitions into k blocks
 S(n,k)=k·S(n−1,k)+S(n−1,k−1)
 # surjections = n!·S(m,n)

BELL  Bₙ = Σ S(n,k)
 1,1,2,5,15,52,203,877,...
 = # partitions = # equivalence rels

FIBONACCI  Fₙ = F_{n−1}+F_{n−2}
 φ = (1+√5)/2

GENERATING FUNCTIONS
 1/(1−x) = Σ xⁿ
 (1+x)ⁿ = Σ C(n,k) xᵏ
 Cₙ : (1−√(1−4x))/(2x)
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | `C(n,r) = n!/(r!(n−r)!)` | ✅✅✅ |
| 2 | Pascal: `C(n,k)=C(n−1,k)+C(n−1,k−1)` | ✅ |
| 3 | `Σ C(n,k) = 2ⁿ` | ✅✅ |
| 4 | Stars-bars (≥0): `C(n+k−1, k−1)` | ✅✅ |
| 5 | Stars-bars (≥1): `C(n−1, k−1)` | ✅✅ |
| 6 | Multinomial: `n!/(n₁!…nₖ!)` | ✅ |
| 7 | Circular perm: `(n−1)!` | ✅ |
| 8 | Derangement: `Dₙ ≈ n!/e`; recurrence `Dₙ=(n−1)(D_{n−1}+D_{n−2})` | ✅ |
| 9 | Catalan: `C(2n,n)/(n+1)` | ✅✅ |
| 10 | # surjections = `n!·S(m,n)` | ✅ |
| 11 | Bell: `Bₙ = Σ S(n,k)` | ✅ |
| 12 | Vandermonde: `C(m+n,r) = Σ C(m,k)C(n,r−k)` | ✅ |
| 13 | Hockey-stick: `Σ_{i=r}^n C(i,r) = C(n+1, r+1)` | ✅ |
| 14 | Fibonacci closed: `Fₙ = (φⁿ − ψⁿ)/√5` | ✅ |
| 15 | PIE: `|∪Aᵢ| = Σ−Σ+Σ−…` | ✅✅ |

### Tricks

- **"At least one"** counting: total − (none).
- **"At most k"** = sum from 0 to k of "exactly i".
- **"Exactly k of n events"**: PIE-style sum.
- **Gap method:** to keep certain items separated, place them in gaps between non-restricted items.
- **Complement counting:** when "at least one" is hard, count "none" and subtract.
- **Symmetry argument:** in `C(2n, n)` style problems, exploit pairing.
- **Generating function trick:** to count compositions of n into k parts each ≥ a, expand `(xᵃ+x^(a+1)+…)ᵏ`.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
The number of ways to arrange the letters of the word EFFLORESCENCE such that no two C's are adjacent is:
*(Use total − (C's adjacent), or gap method.)*

**Solution.** Letters: E,F,F,L,O,R,E,S,C,E,N,C,E (13 letters; E×4, F×2, C×2, others 1 each). Total arrangements = 13!/(4!·2!·2!). For C's adjacent: glue C's = 12 letters with E×4, F×2, CC×1 ⇒ 12!/(4!·2!). Subtract.
**Answer:** computed as 13!/(4!·2!·2!) − 12!/(4!·2!).

### Q2. (GATE CSE 2014)
The number of ways to choose 4 cards from a deck of 52 such that all 4 are of different suits is:
**Solution.** Choose 1 from each suit: 13 · 13 · 13 · 13 = 13⁴ = 28,561. *(Pattern: independent choices.)*

### Q3. (GATE CSE 2018)
A computer program reads a sequence of distinct positive integers. The number of integer sequences of length 4 from {1,2,3,4,5,6,7,8} that are strictly increasing is:
**Solution.** Choose 4 of 8, exactly one ordering per choice: C(8,4) = 70.

### Q4. (GATE CSE 2008)
The number of n-digit binary strings that have no two consecutive 1's is given by:
**Solution.** Recurrence: aₙ = a_{n−1} + a_{n−2}, a₁=2, a₂=3 ⇒ Fibonacci-like, aₙ = F_{n+2}. *(Pattern: Fibonacci recurrence.)*

### Q5. (GATE CSE 2015)
The number of distinct binary search trees that can be created out of 4 distinct keys is:
**Solution.** Catalan C₄ = C(8,4)/5 = 70/5 = 14.
**Answer: 14.**

### Q6. (GATE CSE 2007)
A bag has 19 red and 19 blue balls. Two balls are drawn at random without replacement. Probability both are red:
**Solution.** C(19,2)/C(38,2) = 171/703 = 9/37. *(Pattern: combinations probability.)*

### Q7. (GATE CSE 2013)
Suppose p = number of cars per minute passing through a junction follows Poisson with mean 3. Probability of 0 cars in a 1-min interval:
**Solution.** P(X=0) = e⁻³ · 3⁰/0! = e⁻³ ≈ 0.0498. *(Pattern: Poisson.)*

### Q8. (GATE CSE 2010)
Aladdin has 5 different gold coins. # ways to distribute among 3 robbers with each getting at least one:
**Solution.** Surjections: 3! · S(5,3) = 6 · 25 = 150. *(Pattern: # surjections.)*

### Q9. (GATE CSE 2004)
The number of integer solutions to `x₁ + x₂ + x₃ + x₄ = 20`, with each xᵢ ≥ 0:
**Solution.** C(20+4−1, 4−1) = C(23, 3) = 1771. *(Pattern: stars-bars.)*

### Q10. (GATE CSE 2011)
Number of distinct ways of choosing exactly 2 balls from a box containing 10 red, 8 blue, 5 green balls (balls of same color identical):
**Solution.** Stars-bars: 2 balls into 3 colors with limits (10,8,5) — all limits ≥ 2 ⇒ C(2+3−1, 2) = C(4,2) = 6.

### Q11. (GATE CSE 2003)
Solve aₙ = 6 a_{n−1} − 9 a_{n−2}, a₀ = 1, a₁ = 6.
**Solution.** Char eq: r² − 6r + 9 = 0 → (r−3)² = 0, repeated root 3. aₙ = (α + βn) 3ⁿ. n=0: α = 1; n=1: (1+β)·3 = 6 ⇒ β = 1. So **aₙ = (1+n) 3ⁿ**.

### Q12. (GATE CSE 2016)
Recurrence: T(n) = 2 T(n/2) + n. Master Theorem gives:
**Solution.** Case 2 (f(n) = Θ(n^(log₂ 2)) = Θ(n)). T = Θ(n log n).

### Q13. (GATE CSE 2009)
A bag contains 10 white and 15 black balls. Two are drawn one after another without replacement. Probability the first is white and second is black:
**Solution.** (10/25) · (15/24) = 150/600 = 1/4.

### Q14. (GATE CSE 2018)
Number of permutations of {1,2,3,4,5,6,7} where each i ≠ position(i) (derangements) is:
**Solution.** D₇ = 1854.

### Q15. (GATE CSE 2020)
The number of permutations of `{1,2,3,4,5}` with exactly 1 fixed point:
**Solution.** Choose the fixed point in 5 ways; derange the rest: 5 · D₄ = 5 · 9 = 45.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Compute C(10, 3).

**P2.** # arrangements of MISSISSIPPI.

**P3.** # subsets of a 6-element set.

**P4.** # ways to choose 5 cards from a 52-card deck.

**P5.** # ways 6 people sit in a row.

**P6.** # ways 6 people sit around a circular table.

**P7.** # bit strings of length 8 with exactly 3 ones.

**P8.** Coefficient of x⁴ in (1+x)⁹.

**P9.** Compute D₅.

**P10.** # ways 10 identical candies to 4 children.

### Medium

**P11.** # binary strings of length 10 with no two consecutive 1's.

**P12.** # ways 5 men and 5 women in a row, no two men adjacent.

**P13.** Solve aₙ = 5 a_{n−1} − 6 a_{n−2}, a₀=1, a₁=4.

**P14.** Coefficient of x¹⁰ in (1−x)⁻³.

**P15.** # integer sols to x+y+z+w = 25, each ≥ 1.

**P16.** # ways to place 8 non-attacking rooks on an 8×8 board.

**P17.** # functions from 5-set to 3-set that are onto.

**P18.** # binary trees with 5 internal nodes.

**P19.** Pigeonhole: among any 11 integers from 1..20, must there be two with sum 21?

**P20.** # ways to seat 4 men and 4 women alternately around a round table.

### Hard

**P21.** # binary strings of length 15 with exactly 5 ones and no two consecutive ones.

**P22.** Solve aₙ = aₙ₋₁ + 2 aₙ₋₂, a₀=1, a₁=2.

**P23.** Find the closed-form for the # of distinct paths from (0,0) to (n,n) on grid moving R or U.

**P24.** # ways to distribute 10 distinct books among 3 students with each getting ≥ 1.

**P25.** Coefficient of x¹⁰ in (1 + x + x²)⁴.

**P26.** Number of ways to write 100 as ordered sum of 4 positive integers.

**P27.** Find Bell number B₆.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 120 | 10·9·8/6 |
| P2 | 11!/(4!·4!·2!) = 34650 | M:1, I:4, S:4, P:2 |
| P3 | 64 | 2⁶ |
| P4 | C(52,5) = 2,598,960 | hand counts |
| P5 | 720 | 6! |
| P6 | 120 | (n−1)! |
| P7 | C(8,3) = 56 | binomial |
| P8 | C(9,4) = 126 | binomial |
| P9 | 44 | D₅ = 44 |
| P10 | C(13,3) = 286 | stars-bars |
| P11 | F₁₂ = 144 (Fibonacci-shift) | Fibonacci recurrence |
| P12 | 5!·5! · 2 (men-positions starting from M or W) — actually arrange women first 5! and slots for men: 6 slots, choose 5: C(6,5)·5! arrangements ⇒ **5!·6·5!/something**; standard answer = 5!·6P5 = 86400 | gap method |
| P13 | r² − 5r + 6 = 0 → r=2,3; aₙ = α·2ⁿ + β·3ⁿ. From a₀=1, a₁=4 ⇒ α=−1, β=2. **aₙ = 2·3ⁿ − 2ⁿ** | distinct roots |
| P14 | C(10+2,2) = 66 | (1−x)⁻ᵏ expansion |
| P15 | C(24,3) = 2024 | shift xᵢ→xᵢ−1 |
| P16 | 8! = 40320 | one rook per row + column |
| P17 | 3! · S(5,3) = 6·25 = 150 | surjections |
| P18 | C₅ = 42 | Catalan |
| P19 | Yes | pairs (1,20),(2,19)…(10,11) — 10 pigeonholes, 11 elements |
| P20 | (4−1)! · 4! = 6·24 = 144 | fix 1 man, arrange other 3 men, then 4 women in 4 alternate seats |
| P21 | C(11,5) = 462 | choose 5 positions among 15−5+1=11 |
| P22 | char r²=r+2 ⇒ r=2,−1; aₙ=α·2ⁿ+β(−1)ⁿ; α+β=1, 2α−β=2 ⇒ α=1, β=0. **aₙ = 2ⁿ** | distinct roots |
| P23 | C(2n, n) | lattice paths |
| P24 | 3! · S(10,3) = 6 · 9330 = 55980 | surjections |
| P25 | coefficient computation; via generating function expansion = 4 (or compute by trinomial) | coefficient extraction |
| P26 | C(99, 3) = 156,849 | stars-bars positive |
| P27 | B₆ = 203 | from list |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing permutations vs combinations | "Order matters?" → P; else C. |
| 2 | Stars-bars formula off by one | ≥0 ⇒ C(n+k−1, k−1); ≥1 ⇒ C(n−1, k−1). |
| 3 | Treating "identical objects to distinct boxes" as kⁿ | That's distinct→distinct. Identical→distinct uses stars-bars. |
| 4 | Counting circular perms as n! | Use (n−1)!. |
| 5 | Forgetting symmetry in Pascal/binomial | C(n,r) = C(n,n−r). |
| 6 | Master Theorem misapplication when f(n) doesn't fit any case | Use Akra-Bazzi or recursion-tree. |
| 7 | Forgetting (−1)ⁿ in PIE | Sign alternates. |
| 8 | Mixing surjection formula with onto count | # surjections = n!·S(m,n), not nᵐ. |
| 9 | Treating Catalan as nⁿ⁻² | Catalan ≠ Cayley. |
| 10 | Solving recurrence without verifying char roots | Repeated roots need n·rⁿ term. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Distinct objects in distinct boxes" | kⁿ |
| "Identical objects in distinct boxes" | Stars-bars: C(n+k−1, k−1) |
| "At least one in each" | Stars-bars positive or surjections |
| "No two adjacent" | Fibonacci or gap method |
| "Round table seating" | (n−1)! |
| "Probability X events from N draws" | C(K,k)C(N−K,n−k)/C(N,n) hypergeometric |
| "Recurrence with constant coefficients" | Char equation |
| "T(n) = aT(n/b) + f(n)" | Master Theorem |
| "Onto functions count" | PIE: Σ(−1)ᵏ C(n,k)(n−k)ᵐ or n!·S(m,n) |
| "BST count / parens / triangulations" | Catalan |
| "Partitions of a set" | Bell / Stirling |
| "Permutations no fixed point" | Derangement Dₙ |
| "Coefficient of xᵏ in (…)ⁿ" | Multinomial / generating function |
| "How many integers ≤ N coprime to N" | Euler φ(N) |

---

## 9. Quick Revision

```
P(n,r)=n!/(n−r)!     C(n,r)=n!/(r!(n−r)!)
ΣC(n,k)=2ⁿ           Pascal: C(n,k)=C(n−1,k)+C(n−1,k−1)

Stars-bars
 ≥0 sols: C(n+k−1,k−1)
 ≥1 sols: C(n−1,k−1)

Multinomial: n!/(n₁!…nₖ!)
Circular: (n−1)!
Pigeonhole: ⌈N/k⌉

PIE: Σ−Σ+Σ−…
Onto fns: Σ(−1)ᵏC(n,k)(n−k)ᵐ = n!·S(m,n)
Derangements: Dₙ ≈ n!/e
Euler φ(N) = N·∏(1−1/p)

Catalan Cₙ = C(2n,n)/(n+1)  : 1,1,2,5,14,42,132
Bell Bₙ                     : 1,1,2,5,15,52,203
Stirling 2nd: S(n,k)=k·S(n−1,k)+S(n−1,k−1)
Fibonacci: Fₙ = (φⁿ − ψⁿ)/√5

Recurrence char-eq:
 distinct roots → aₙ = Σ αᵢrᵢⁿ
 root r mult m → (α₀+α₁n+…+α_{m−1}n^(m−1))rⁿ

Master:
 a T(n/b)+f(n)
 compare f(n) to n^(log_b a)

Vandermonde: C(m+n,r)=ΣC(m,k)C(n,r−k)
Hockey-stick: Σ_{i=r}^n C(i,r) = C(n+1,r+1)
```
