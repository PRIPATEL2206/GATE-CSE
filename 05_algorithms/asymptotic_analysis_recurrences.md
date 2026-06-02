# Asymptotic Analysis & Recurrences

> Subject: Algorithms
> GATE weight: **2–4 marks** every year. Big-O/Θ/Ω, recurrence solving, Master Theorem.

---

## 1. Concept Explanation

### 1.1 Why Asymptotic Analysis?

Compare algorithm efficiency for **large input sizes**, ignoring constants and lower-order terms. Focuses on **growth rate**.

### 1.2 Asymptotic Notations

| Notation | Definition | Reads as |
|---|---|---|
| **O(g(n))** | f(n) ≤ c·g(n) for n ≥ n₀ | upper bound (≤) |
| **Ω(g(n))** | f(n) ≥ c·g(n) for n ≥ n₀ | lower bound (≥) |
| **Θ(g(n))** | c₁·g(n) ≤ f(n) ≤ c₂·g(n) | tight bound (=) |
| **o(g(n))** | f(n) < c·g(n) for all c > 0 | strict upper (<) |
| **ω(g(n))** | f(n) > c·g(n) for all c > 0 | strict lower (>) |

### 1.3 Common Growth Rates (slowest → fastest)

```
1 < log log n < log n < √n < n < n log n
  < n² < n³ < ... < 2ⁿ < 3ⁿ < n! < nⁿ
```

### 1.4 Properties of O, Θ, Ω

| Property |
|---|
| Reflexive: f = O(f), Ω(f), Θ(f) |
| Transitive: if f = O(g), g = O(h), then f = O(h) |
| Symmetric: f = Θ(g) ⇔ g = Θ(f) |
| f = Θ(g) ⇔ f = O(g) **and** f = Ω(g) |
| Sum rule: O(f) + O(g) = O(max(f, g)) |
| Constant factor: O(c·f) = O(f) |

### 1.5 Identifying Notation from Limit

Let L = lim_{n→∞} f(n)/g(n).

| L | Conclusion |
|---|---|
| 0 | f = o(g), so f = O(g) but f ≠ Θ(g) |
| ∞ | f = ω(g), so f = Ω(g) but f ≠ Θ(g) |
| Finite > 0 | f = Θ(g) |

### 1.6 Recurrence Relations

A recurrence T(n) defines T(n) in terms of T at smaller arguments.

**Common forms:**
- **Linear:** T(n) = T(n−1) + f(n).
- **Divide-and-conquer:** T(n) = a · T(n/b) + f(n).
- **Decrease-and-conquer:** T(n) = T(n−c) + f(n).

### 1.7 Solving Linear Recurrences (Iteration / Substitution)

**Example:** T(n) = T(n−1) + n, T(1) = 1.
Expand: T(n) = T(n−1) + n = T(n−2) + (n−1) + n = … = 1 + 2 + … + n = n(n+1)/2 = Θ(n²).

**Example:** T(n) = T(n−1) + 1 → T(n) = Θ(n).

### 1.8 Master Theorem

For `T(n) = a·T(n/b) + f(n)` with a ≥ 1, b > 1:

Let `c = log_b a`.

| Case | Condition | T(n) |
|---|---|---|
| 1 | f(n) = O(n^(c−ε)) for some ε > 0 | Θ(n^c) |
| 2 | f(n) = Θ(n^c · logᵏ n), k ≥ 0 | Θ(n^c · log^(k+1) n) |
| 3 | f(n) = Ω(n^(c+ε)) AND a·f(n/b) ≤ d·f(n) for d < 1 (regularity) | Θ(f(n)) |

### 1.9 Master Theorem Examples

| Recurrence | log_b a | f(n) | Case | T(n) |
|---|---|---|---|---|
| T(n) = 2T(n/2) + n | 1 | n | 2 (k=0) | Θ(n log n) |
| T(n) = 2T(n/2) + n² | 1 | n² | 3 | Θ(n²) |
| T(n) = 2T(n/2) + 1 | 1 | 1 | 1 | Θ(n) |
| T(n) = 4T(n/2) + n² | 2 | n² | 2 (k=0) | Θ(n² log n) |
| T(n) = 4T(n/2) + n | 2 | n | 1 | Θ(n²) |
| T(n) = 4T(n/2) + n³ | 2 | n³ | 3 | Θ(n³) |
| T(n) = 7T(n/2) + n² | log₂7 ≈ 2.81 | n² | 1 | Θ(n^(log₂7)) (Strassen) |
| T(n) = 8T(n/2) + n² | 3 | n² | 1 | Θ(n³) |
| T(n) = 9T(n/3) + n | 2 | n | 1 | Θ(n²) |
| T(n) = T(n/2) + 1 | 0 | 1 | 2 | Θ(log n) |

### 1.10 When Master Theorem Doesn't Apply

- f(n) is not polynomial (e.g., n / log n).
- a < 1 or b ≤ 1.
- Gap cases: f(n) between n^c and n^(c+ε) without polynomial separation.

**Use Akra-Bazzi** or **recursion-tree** method.

### 1.11 Recursion Tree Method

Draw the tree of recursive calls; sum work per level.

**Example:** T(n) = 2T(n/2) + n.
- Each level has total n work.
- log₂ n levels.
- Total = n · log n = Θ(n log n).

### 1.12 Substitution Method

Guess solution; verify by induction.

**Example:** T(n) = 2T(n/2) + n. Guess T(n) ≤ c·n log n. Substitute and solve for c.

### 1.13 Linear Recurrences with Constant Coefficients

Form: `aₙ = c₁ aₙ₋₁ + c₂ aₙ₋₂ + … + cₖ aₙ₋ₖ`.

(See [combinatorics.md](../../01_engineering_mathematics/discrete_mathematics/combinatorics.md) §1.8.)

**Solve via characteristic polynomial.** Important for algorithm analysis (e.g., Fibonacci recursion).

### 1.14 Common Algorithmic Recurrences

| Algorithm | Recurrence | T(n) |
|---|---|---|
| Linear search | T(n) = T(n−1) + 1 | Θ(n) |
| Binary search | T(n) = T(n/2) + 1 | Θ(log n) |
| Merge sort | T(n) = 2T(n/2) + n | Θ(n log n) |
| Quicksort (avg) | T(n) = 2T(n/2) + n | Θ(n log n) |
| Quicksort (worst) | T(n) = T(n−1) + n | Θ(n²) |
| Tower of Hanoi | T(n) = 2T(n−1) + 1 | Θ(2ⁿ) |
| Strassen | T(n) = 7T(n/2) + n² | Θ(n^log₂7) ≈ Θ(n^2.81) |
| Karatsuba | T(n) = 3T(n/2) + n | Θ(n^log₂3) ≈ Θ(n^1.58) |

### 1.15 Amortized Analysis

Average cost per operation across worst-case sequence of operations.

**Methods:**
- **Aggregate:** total cost / # ops.
- **Accounting:** assign credit to operations.
- **Potential:** define potential function.

**Examples:**
- Dynamic array doubling: amortized O(1) per insert.
- Stack with multipop: amortized O(1) per op.
- Splay tree: amortized O(log n).

### 1.16 Best/Average/Worst Case

| Case | Description |
|---|---|
| **Best** | Min running time over all inputs of size n |
| **Average** | Expected time over random inputs |
| **Worst** | Max running time over all inputs of size n |

GATE typically asks for worst-case (or specific average).

### 1.17 Polynomial vs Exponential

- **Polynomial time:** O(n^k) for some constant k. **Tractable.**
- **Exponential:** O(c^n), c > 1. Generally intractable for large n.
- **P, NP, NP-Complete:** topic in algorithms (np_completeness.md).

### 1.18 Logarithm Properties

- log(ab) = log a + log b
- log(a^b) = b log a
- log_b(a) = log_c(a) / log_c(b)
- log₂ n = log n / log 2 (base change)
- O(log_a n) = O(log_b n) (constant factor difference)

> **Summary:** Master O/Θ/Ω, Master Theorem cases (with examples), recursion tree, common recurrences for known algorithms, growth rate ladder.

---

## 2. Important Points

- **Big-O is upper bound**, **Ω is lower**, **Θ is tight**.
- Growth rates: 1 < log n < √n < n < n log n < n² < 2ⁿ < n!.
- **Master Theorem applies** to T(n) = aT(n/b) + f(n) when f is polynomial-like.
- Case 1: small f → Θ(n^log_b a).
- Case 2: balanced → Θ(n^log_b a · log n).
- Case 3: large f → Θ(f(n)).
- **Regularity condition** in Case 3 sometimes overlooked.
- **Recursion tree** is fastest informal method.
- **Substitution** verifies guesses by induction.
- **Linear search:** Θ(n); **binary search:** Θ(log n).
- **Merge sort:** Θ(n log n) regardless of input.
- **Quicksort:** Θ(n log n) average; Θ(n²) worst.
- **Tower of Hanoi:** Θ(2ⁿ).
- **Fibonacci recursion (no memo):** Θ(φⁿ).
- **Amortized cost** averages over a sequence; not best-case.
- **Logarithm base** doesn't matter in big-O.

---

## 3. Short Notes

```
ASYMPTOTIC NOTATIONS
 O: ≤ (upper bound)
 Ω: ≥ (lower bound)
 Θ: = (tight)
 o, ω: strict

GROWTH RATES (slow → fast)
 1, log log n, log n, √n, n, n log n,
 n², n³, ..., 2ⁿ, 3ⁿ, n!, nⁿ

LIMIT TEST
 lim f/g = 0 ⇒ f = o(g)
 lim f/g = ∞ ⇒ f = ω(g)
 lim f/g = c > 0 ⇒ f = Θ(g)

RECURRENCES
 T(n) = T(n−1) + f(n) — linear
 T(n) = aT(n/b) + f(n) — divide & conquer
 T(n) = T(n−c) + f(n) — decrease

MASTER THEOREM (a ≥ 1, b > 1)
 c = log_b a
 case 1: f = O(n^(c−ε)) ⇒ Θ(n^c)
 case 2: f = Θ(n^c logᵏn) ⇒ Θ(n^c log^(k+1) n)
 case 3: f = Ω(n^(c+ε)) + regularity ⇒ Θ(f(n))

RECURSION TREE
 sum work per level
 # levels = depth

SUBSTITUTION
 guess + induction

COMMON RECURRENCES
 T(n) = T(n−1) + 1: Θ(n)
 T(n) = T(n/2) + 1: Θ(log n)
 T(n) = 2T(n/2) + n: Θ(n log n)
 T(n) = 2T(n/2) + n²: Θ(n²)
 T(n) = T(n/2) + n: Θ(n)
 T(n) = 2T(n−1) + 1: Θ(2ⁿ)

AMORTIZED
 aggregate / accounting / potential

LINEAR HOMOGENEOUS
 char poly → roots → solution
 (cross-link to combinatorics)
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Master Theorem 3 cases | ✅✅✅ |
| 2 | log_b a key value for Master | ✅✅ |
| 3 | T(n) = T(n/2)+1 ⇒ Θ(log n) | ✅✅ |
| 4 | T(n) = 2T(n/2)+n ⇒ Θ(n log n) | ✅✅ |
| 5 | T(n) = T(n-1)+1 ⇒ Θ(n) | ✅ |
| 6 | T(n) = 2T(n-1)+1 ⇒ Θ(2ⁿ) | ✅ |
| 7 | log property: log(ab) = log a + log b | ✅ |
| 8 | Base change: log_b a = ln a / ln b | ✅ |
| 9 | f = Θ(g) ⇔ O(g) + Ω(g) | ✅ |
| 10 | Limit test for asymptotic comparison | ✅ |
| 11 | Sum rule: O(f) + O(g) = O(max) | ✅ |

### Tricks

- **For Master Theorem ε:** check if f beats n^c by polynomial factor (n^ε).
- **Recursion tree shortcut:** levels of work follow geometric series; use ratio to identify dominant level.
- **For T(n) = aT(n/b) + f(n):** compute n^log_b a, compare to f.
- **Logarithm base in big-O ignored:** O(log₂ n) = O(log₁₀ n) = O(log n).
- **Identify O/Ω/Θ:** compute limit of f/g.
- **Skip Master Theorem when f is non-polynomial:** use recursion tree or Akra-Bazzi.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
T(n) = 2T(n/2) + n. T(n) is:
**Solution.** Master case 2; Θ(n log n).

### Q2. (GATE CSE 2014)
Order: 1, n, n log n, log n, n², 2ⁿ, n³ from smallest to largest.
**Solution.** 1 < log n < n < n log n < n² < n³ < 2ⁿ.

### Q3. (GATE CSE 2018)
T(n) = 4T(n/2) + n²:
**Solution.** log₂4 = 2; f = n² = Θ(n² log⁰ n) → Case 2; Θ(n² log n).

### Q4. (GATE CSE 2008)
T(n) = T(n/2) + n. T(n) is:
**Solution.** Master case 3; Θ(n).

### Q5. (GATE CSE 2010)
Tower of Hanoi: T(n) = 2T(n−1) + 1. Solve.
**Solution.** T(n) = 2ⁿ − 1.

### Q6. (GATE CSE 2015)
Best case for quicksort:
**Solution.** Θ(n log n) (balanced partitions).

### Q7. (GATE CSE 2013)
Strassen's: T(n) = 7T(n/2) + n². T(n)?
**Solution.** Θ(n^log₂7) ≈ Θ(n^2.807).

### Q8. (GATE CSE 2007)
T(n) = 9T(n/3) + n²:
**Solution.** log₃9 = 2; Case 2; Θ(n² log n).

### Q9. (GATE CSE 2003)
What's bigger: 2ⁿ or n!?
**Solution.** n! grows faster.

### Q10. (GATE CSE 2009)
Amortized cost of dynamic array doubling:
**Solution.** O(1).

### Q11. (GATE CSE 2019)
Solve T(n) = T(n − 1) + log n.
**Solution.** Σ log i = log(n!) = Θ(n log n).

### Q12. (GATE CSE 2020)
T(n) = 2T(n/2) + n log n:
**Solution.** Master case 2 (f = Θ(n log n) = Θ(n^1 log¹ n)); Θ(n log² n).

### Q13. (GATE CSE 2021)
Comparison: f = n^(log n), g = n²:
**Solution.** n^(log n) > n² for large n.

### Q14. (GATE CSE 2016)
Big-O of `for(i=1;i<n;i*=2) sum++;` — O(?)
**Solution.** O(log n).

### Q15. (GATE CSE 2011)
T(n) = 2T(n/2) + 1:
**Solution.** Master case 1; Θ(n).

---

## 6. Practice Questions (20+)

### Easy

**P1.** State Master Theorem cases.

**P2.** Big-O of n + n log n?

**P3.** Solve T(n) = T(n−1) + 1.

**P4.** Solve T(n) = 2T(n/2) + n.

**P5.** Order: log n, √n, n, log² n.

**P6.** Solve T(n) = T(n/3) + n.

**P7.** Solve T(n) = T(n−1) + n.

**P8.** Big-O of `for(i=1; i<n; i++) for(j=1; j<n; j*=2) sum++;`?

**P9.** Logarithm base affects big-O?

**P10.** Define amortized cost.

### Medium

**P11.** Solve T(n) = 4T(n/2) + n.

**P12.** Solve T(n) = 8T(n/2) + n³.

**P13.** Solve T(n) = T(n/2) + log n.

**P14.** Solve T(n) = 2T(n−1) + 1.

**P15.** Solve T(n) = 3T(n/2) + n.

**P16.** Solve T(n) = T(n/2) + n.

**P17.** Solve T(n) = 2T(n/2) + n²/log n.

**P18.** Solve T(n) = T(√n) + 1.

**P19.** Solve T(n) = T(n − 1) + 1/n.

**P20.** Compare 2^(log n) and n.

### Hard

**P21.** Show Master case 2 with k = 0.

**P22.** Solve T(n) = 2T(n/4) + √n via Master.

**P23.** Recursion tree: T(n) = 2T(n/2) + n²; find total.

**P24.** Akra-Bazzi for T(n) = T(n/3) + T(2n/3) + n.

**P25.** Amortized cost of binary counter increment.

**P26.** Solve T(n) = T(n/2) + T(n/4) + n via tree.

**P27.** Show f = O(g), Ω(g), Θ(g) is consistent.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.8 | direct |
| P2 | Θ(n log n) | direct |
| P3 | Θ(n) | direct |
| P4 | Θ(n log n) | Master |
| P5 | log n < log² n < √n < n | direct |
| P6 | Θ(n) | Master case 3 |
| P7 | Θ(n²) | sum |
| P8 | Θ(n log n) | nested |
| P9 | No | constant factor |
| P10 | avg cost over worst-case sequence | direct |
| P11 | Θ(n²) | log₂4=2; n=O(n^(2−ε)); case 1 |
| P12 | Θ(n³ log n) | log₂8=3; case 2 |
| P13 | Θ(log² n) | not Master directly; substitution |
| P14 | Θ(2ⁿ) | direct |
| P15 | Θ(n^log₂3) ≈ n^1.58 | log₂3 ≈ 1.58; case 1 |
| P16 | Θ(n) | case 3 |
| P17 | Θ(n² log log n) | Akra-Bazzi |
| P18 | Θ(log log n) | substitution m=log n |
| P19 | Θ(log n) | harmonic |
| P20 | n (equal) | 2^(log n) = n |
| P21 | n^c × log⁰ n = Θ(n^c); → Θ(n^c log n) | direct |
| P22 | log₄2 = 0.5; f=√n=Θ(n^0.5); case 2 → Θ(√n log n) | direct |
| P23 | sum geometric: top dominates → Θ(n²) | direct |
| P24 | Θ(n log n) | Akra-Bazzi p=1 |
| P25 | O(1) per increment amortized | direct |
| P26 | Θ(n log n) | direct |
| P27 | f = Θ(g) ⇔ both O and Ω | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting regularity in Master case 3 | Check a · f(n/b) ≤ c · f(n). |
| 2 | Using Master when f is non-polynomial | Use Akra-Bazzi or recursion tree. |
| 3 | Confusing O and Θ | Tightness matters. |
| 4 | Treating constant base log as different | Same in big-O. |
| 5 | Missing recursion tree imbalance | T(n/3) + T(2n/3) needs care. |
| 6 | Average-case = worst-case | They differ in quicksort. |
| 7 | Tower of Hanoi is polynomial | It's exponential 2ⁿ. |
| 8 | Forgetting lower-order in solutions | Big-O hides them. |
| 9 | Not checking polynomial separation | Master case 1/3 needs ε. |
| 10 | Treating f = O(g) and g = O(f) as Θ | Yes, but verify both directions. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "T(n) = aT(n/b) + f(n)" | Apply Master Theorem. |
| "Recursion: T(n) = 2T(n/2) + n" | Θ(n log n). |
| "Tower of Hanoi" | 2ⁿ − 1. |
| "Binary search recurrence" | Θ(log n). |
| "Quicksort worst case" | Θ(n²). |
| "Amortized analysis" | Aggregate, accounting, or potential. |
| "Strassen / Karatsuba" | Specific exponent log₂7 / log₂3. |
| "Compare growth" | Use limit test. |
| "Big-O of nested loops" | Multiply iteration counts. |
| "Master fails / non-polynomial f" | Recursion tree or Akra-Bazzi. |

---

## 9. Quick Revision

```
NOTATIONS
 O: upper, Ω: lower, Θ: tight
 o, ω: strict

GROWTH (slow → fast)
 1 < log n < √n < n < n log n
 < n² < n³ < 2ⁿ < n!

LIMIT TEST f/g
 0 → o(g)
 ∞ → ω(g)
 c > 0 → Θ(g)

MASTER THEOREM
 T(n) = aT(n/b) + f(n)
 c = log_b a
 case 1: f = O(n^(c−ε)) → Θ(n^c)
 case 2: f = Θ(n^c logᵏ n) → Θ(n^c log^(k+1) n)
 case 3: f = Ω(n^(c+ε)) + regularity → Θ(f)

RECURSION TREE
 sum work per level

SUBSTITUTION
 guess + induct

COMMON
 T(n) = T(n−1) + 1: Θ(n)
 T(n) = T(n/2) + 1: Θ(log n)
 T(n) = 2T(n/2) + n: Θ(n log n)
 T(n) = T(n/2) + n: Θ(n)
 T(n) = 2T(n−1) + 1: Θ(2ⁿ)
 Strassen 7T(n/2)+n²: Θ(n^log₂7)
 Karatsuba 3T(n/2)+n: Θ(n^log₂3)

AMORTIZED: aggregate / accounting / potential
```
