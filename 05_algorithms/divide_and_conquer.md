# Divide & Conquer

> Subject: Algorithms
> GATE weight: **2–3 marks** every year. Recurrence-based algorithms — merge sort, quicksort, Strassen, Karatsuba, closest pair.

---

## 1. Concept Explanation

### 1.1 Divide-and-Conquer Paradigm

Three steps:
1. **Divide** problem into smaller subproblems (typically same kind).
2. **Conquer** subproblems recursively (base case if small).
3. **Combine** subproblem solutions into solution for original.

**Recurrence:** T(n) = a · T(n/b) + f(n) (typical Master Theorem form).

### 1.2 Merge Sort (recap)

```
mergeSort(a, lo, hi):
  if lo >= hi: return
  mid = (lo + hi) / 2
  mergeSort(a, lo, mid)
  mergeSort(a, mid+1, hi)
  merge(a, lo, mid, hi)
```

`T(n) = 2T(n/2) + n → O(n log n)`. Stable, not in-place.

### 1.3 Quick Sort (recap)

```
quickSort(a, lo, hi):
  if lo >= hi: return
  p = partition(a, lo, hi)
  quickSort(a, lo, p-1)
  quickSort(a, p+1, hi)
```

Average O(n log n); worst O(n²) on bad pivot.

### 1.4 Binary Search

```
binarySearch(a, lo, hi, t):
  if lo > hi: return -1
  mid = (lo + hi) / 2
  if a[mid] == t: return mid
  if a[mid] < t: return binarySearch(a, mid+1, hi, t)
  return binarySearch(a, lo, mid-1, t)
```

`T(n) = T(n/2) + 1 → O(log n)`.

### 1.5 Karatsuba Multiplication

Multiplies two n-digit numbers with O(n^log₂3) ≈ O(n^1.58) operations.

```
multiply(x, y):
  if n is small: return x * y
  split x = x_hi · B^(n/2) + x_lo
  split y = y_hi · B^(n/2) + y_lo
  P1 = multiply(x_hi, y_hi)
  P2 = multiply(x_lo, y_lo)
  P3 = multiply(x_hi + x_lo, y_hi + y_lo)
  return P1·B^n + (P3 − P1 − P2)·B^(n/2) + P2
```

Naive: O(n²); Karatsuba: O(n^log₂3) ≈ O(n^1.585).

### 1.6 Strassen Matrix Multiplication

For two n×n matrices, naive multiplication is O(n³).

Strassen reduces 8 sub-multiplications to 7 → `T(n) = 7T(n/2) + n²` → O(n^log₂7) ≈ O(n^2.807).

**Strassen's 7 products** combine submatrices A₁₁, A₁₂, A₂₁, A₂₂ and B partitions:
```
M1 = (A11 + A22)(B11 + B22)
M2 = (A21 + A22) B11
M3 = A11 (B12 − B22)
M4 = A22 (B21 − B11)
M5 = (A11 + A12) B22
M6 = (A21 − A11)(B11 + B12)
M7 = (A12 − A22)(B21 + B22)
```

Then assemble C₁₁, C₁₂, C₂₁, C₂₂.

### 1.7 Closest Pair of Points

Given n points in the plane, find pair with minimum Euclidean distance.

**Brute force:** O(n²).

**D&C:** O(n log n).
```
1. Sort by x-coordinate.
2. Recursively find closest pair in left and right halves: d_L, d_R.
3. d = min(d_L, d_R).
4. Find closest pair across split (within strip of width 2d).
5. Return min.
```

Strip merge: O(n) using property that each point compared to ≤ 7 others.

### 1.8 Maximum Subarray (Kadane / D&C)

Given array, find contiguous subarray with maximum sum.

**Brute force:** O(n²) or O(n³).
**D&C:** O(n log n) — split, recurse, plus crossing-mid sum.
**Kadane (DP):** O(n) — see DP file.

D&C recurrence:
`T(n) = 2T(n/2) + n → O(n log n)`.

### 1.9 Counting Inversions

In array a, count pairs (i, j) with i < j and a[i] > a[j].

**D&C:** modify merge sort. During merge, count inversions when right half element is taken before left.

`T(n) = 2T(n/2) + n → O(n log n)`.

### 1.10 Power Computation

Compute `xⁿ`.

**Naive:** n−1 multiplications, O(n).

**D&C (fast power):**
```
power(x, n):
  if n == 0: return 1
  if n is even: return power(x*x, n/2)
  else: return x * power(x, n−1)
```

`T(n) = T(n/2) + O(1) → O(log n)`.

### 1.11 General D&C Recurrence Forms

| T(n) | Solution |
|---|---|
| T(n) = 2T(n/2) + n | Θ(n log n) |
| T(n) = 2T(n/2) + 1 | Θ(n) |
| T(n) = T(n/2) + 1 | Θ(log n) |
| T(n) = T(n/2) + n | Θ(n) |
| T(n) = 4T(n/2) + n² | Θ(n² log n) |
| T(n) = 7T(n/2) + n² | Θ(n^log₂7) (Strassen) |
| T(n) = 3T(n/2) + n | Θ(n^log₂3) (Karatsuba) |

### 1.12 D&C vs Greedy vs DP

| Approach | When |
|---|---|
| **Greedy** | Local optimum → global; matroid structure |
| **D&C** | Independent subproblems |
| **DP** | Overlapping subproblems |

D&C subproblems are **disjoint**; DP subproblems **overlap** and benefit from memoization.

### 1.13 Master Theorem (Recap)

For T(n) = aT(n/b) + f(n):
- f(n) = O(n^(log_b a − ε)) → Θ(n^log_b a)
- f(n) = Θ(n^log_b a) → Θ(n^log_b a · log n)
- f(n) = Ω(n^(log_b a + ε)) (regular) → Θ(f(n))

### 1.14 Common Pitfalls

- **Not balanced split** → may not give Master form.
- **Combining cost dominates** → solution depends on f.
- **Subproblems overlap** → use DP.
- **Asymmetric splits** → use Akra-Bazzi.

### 1.15 Other D&C Examples

| Problem | Time |
|---|---|
| FFT | O(n log n) |
| Convex hull (D&C) | O(n log n) |
| Polynomial multiplication (FFT) | O(n log n) |
| Median finding (median-of-medians) | O(n) |
| Tower of Hanoi | O(2ⁿ) |

> **Summary:** D&C = divide + recurse + combine. Master-Theorem analysis. Memorize Karatsuba (n^log₂3), Strassen (n^log₂7), merge sort (n log n), binary search (log n), closest pair (n log n).

---

## 2. Important Points

- **D&C subproblems** are **disjoint** (no overlap → no memoization needed).
- **Recurrence form:** T(n) = aT(n/b) + f(n).
- **Combining step** dominates when f is large (Master case 3).
- **Karatsuba** = 3 multiplications instead of 4 → exponent log₂3 ≈ 1.585.
- **Strassen** = 7 multiplications instead of 8 → exponent log₂7 ≈ 2.807.
- **Closest pair** benefits from spatial sorting + strip combine.
- **Counting inversions** via modified merge sort.
- **Fast exponentiation** is O(log n) — useful in modular arithmetic.
- **Median of two sorted arrays** in O(log(min(m, n))).
- **D&C and DP differ** by overlap in subproblems.
- **FFT** is divide-and-conquer; reduces polynomial multiplication to O(n log n).
- **Tower of Hanoi** illustrates exponential D&C.

---

## 3. Short Notes

```
DIVIDE & CONQUER
 1. divide
 2. conquer (recurse)
 3. combine
 T(n) = a T(n/b) + f(n)

EXAMPLES
 merge sort: 2T(n/2) + n → n log n
 quicksort: T(n/2) + n avg → n log n
 binary search: T(n/2) + 1 → log n
 Karatsuba: 3T(n/2) + n → n^log₂3 (≈1.58)
 Strassen: 7T(n/2) + n² → n^log₂7 (≈2.81)
 closest pair: 2T(n/2) + n → n log n
 inversion count: 2T(n/2) + n → n log n
 fast power: T(n/2) + 1 → log n
 Tower Hanoi: 2T(n−1) + 1 → 2ⁿ

MASTER THEOREM (recap)
 a T(n/b) + f(n)
 c = log_b a
 case 1: f = O(n^(c−ε))  → n^c
 case 2: f = Θ(n^c logᵏ n) → n^c log^(k+1) n
 case 3: f = Ω(n^(c+ε)) regular → f

D&C vs DP
 disjoint subproblems → D&C
 overlapping → DP
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Master Theorem cases | ✅✅✅ |
| 2 | Merge sort O(n log n) | ✅✅ |
| 3 | Quicksort avg O(n log n), worst O(n²) | ✅✅ |
| 4 | Binary search O(log n) | ✅✅ |
| 5 | Karatsuba O(n^log₂3) | ✅✅ |
| 6 | Strassen O(n^log₂7) | ✅✅ |
| 7 | Closest pair O(n log n) | ✅ |
| 8 | Inversion count O(n log n) | ✅ |
| 9 | Fast power O(log n) | ✅ |
| 10 | D&C subproblems disjoint | ✅ |
| 11 | DP subproblems overlap | ✅ |

### Tricks

- **Master Theorem first:** identify a, b, f to classify case.
- **Strassen exponent:** log₂7 ≈ 2.807, faster than naive O(n³) for large n.
- **Karatsuba exponent:** log₂3 ≈ 1.585, faster than O(n²) for large numbers.
- **For closest pair:** strip merge is the trick — only constant comparisons per point.
- **Fast power:** halve exponent each step.
- **D&C for max subarray:** consider crossing-midpoint case.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
T(n) = 2T(n/2) + n. Solution?
**Solution.** Master case 2; Θ(n log n).

### Q2. (GATE CSE 2014)
Karatsuba: T(n) = 3T(n/2) + n. Time?
**Solution.** Θ(n^log₂3) ≈ Θ(n^1.585).

### Q3. (GATE CSE 2018)
Strassen multiplies two n×n matrices in:
**Solution.** Θ(n^log₂7).

### Q4. (GATE CSE 2008)
Closest pair time:
**Solution.** O(n log n).

### Q5. (GATE CSE 2010)
Inversion count using merge sort:
**Solution.** O(n log n).

### Q6. (GATE CSE 2015)
Fast power computation x^n:
**Solution.** O(log n).

### Q7. (GATE CSE 2013)
T(n) = 4T(n/2) + n²:
**Solution.** Master case 2; Θ(n² log n).

### Q8. (GATE CSE 2007)
D&C and DP differ by:
**Solution.** Subproblem overlap.

### Q9. (GATE CSE 2003)
Median of two sorted arrays of size n:
**Solution.** O(log n).

### Q10. (GATE CSE 2009)
T(n) = T(n/2) + n:
**Solution.** Master case 3; Θ(n).

### Q11. (GATE CSE 2019)
Strassen exponent:
**Solution.** log₂7.

### Q12. (GATE CSE 2020)
T(n) = 8T(n/2) + n²:
**Solution.** log₂8 = 3; n² < n³; case 1; Θ(n³).

### Q13. (GATE CSE 2021)
Tower of Hanoi T(n) = 2T(n−1) + 1:
**Solution.** Θ(2ⁿ).

### Q14. (GATE CSE 2016)
T(n) = 9T(n/3) + n²:
**Solution.** log₃9 = 2; case 2; Θ(n² log n).

### Q15. (GATE CSE 2011)
FFT time:
**Solution.** O(n log n).

---

## 6. Practice Questions (20+)

### Easy

**P1.** State the 3 D&C steps.

**P2.** Master Theorem case for T(n) = 2T(n/2) + 1?

**P3.** Karatsuba exponent?

**P4.** Strassen exponent?

**P5.** Closest pair brute force time?

**P6.** D&C vs DP key difference?

**P7.** T(n) = T(n/2) + 1 solution?

**P8.** Tower of Hanoi T(n) recurrence?

**P9.** Fast power complexity?

**P10.** Merge sort time?

### Medium

**P11.** Solve T(n) = 5T(n/4) + n.

**P12.** Solve T(n) = 4T(n/4) + n.

**P13.** Implement D&C for max subarray.

**P14.** Trace Karatsuba on x = 1234, y = 5678.

**P15.** Strassen products M1–M7 from given submatrices.

**P16.** Solve T(n) = 2T(n/2) + n²/log n.

**P17.** Recurrence for closest pair.

**P18.** T(n) = 7T(n/3) + n²:

**P19.** Compare brute vs D&C for matrix multiplication.

**P20.** Implement counting inversions.

### Hard

**P21.** Prove Master Theorem case 1 via recursion tree.

**P22.** Show that T(n) = 2T(n/2) + n/log n cannot use Master.

**P23.** Apply Akra-Bazzi to T(n) = T(n/3) + T(2n/3) + n.

**P24.** D&C for matrix exponentiation.

**P25.** D&C for binary search variant on rotated sorted array.

**P26.** D&C convex hull algorithm.

**P27.** D&C polynomial multiplication via FFT.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | divide, conquer, combine | direct |
| P2 | case 1 (Θ(n)) | direct |
| P3 | log₂3 ≈ 1.585 | direct |
| P4 | log₂7 ≈ 2.807 | direct |
| P5 | O(n²) | direct |
| P6 | overlap | direct |
| P7 | Θ(log n) | direct |
| P8 | T(n) = 2T(n−1) + 1 | direct |
| P9 | O(log n) | direct |
| P10 | O(n log n) | direct |
| P11 | log₄5 ≈ 1.16; n = O(n^(1.16-ε)); case 1; Θ(n^log₄5) | direct |
| P12 | log₄4 = 1; case 2; Θ(n log n) | direct |
| P13 | combine left, right, cross | direct |
| P14 | trace | direct |
| P15 | as in 1.6 | direct |
| P16 | not in Master form; use Akra-Bazzi or substitute | direct |
| P17 | T(n) = 2T(n/2) + n | direct |
| P18 | log₃7 ≈ 1.77; n² = Θ(n^(c+ε)); case 3; Θ(n²) | direct |
| P19 | n³ vs n^2.81 | direct |
| P20 | merge sort variant | direct |
| P21 | levels grow geometrically; sum dominated by leaves | direct |
| P22 | f = n/log n is between n^(c−ε) and n^c | direct |
| P23 | Akra-Bazzi p=1; Θ(n log n) | direct |
| P24 | Mⁿ in O(log n) matrix multiplications | direct |
| P25 | modified binary search; O(log n) | direct |
| P26 | sort, divide, merge hulls | direct |
| P27 | recursive butterfly; O(n log n) | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing D&C with DP | Disjoint vs overlapping. |
| 2 | Forgetting combine cost in recurrence | f(n) matters. |
| 3 | Karatsuba and Strassen mixed up | Karatsuba: integers; Strassen: matrices. |
| 4 | Master Theorem applied without checking polynomial separation | Need ε. |
| 5 | Tower of Hanoi as polynomial | It's exponential. |
| 6 | Counting inversions in O(n²) | D&C gives O(n log n). |
| 7 | Fast power n−1 multiplications | Halving gives log n. |
| 8 | Median of two sorted: O(n) | Actually O(log n) with D&C. |
| 9 | Closest pair O(n²) | D&C reduces to O(n log n). |
| 10 | Karatsuba better always | Only for large n; constant factor matters. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "T(n) = aT(n/b) + f(n)" | Master Theorem. |
| "Multiply two large numbers" | Karatsuba. |
| "Multiply two matrices" | Strassen. |
| "Closest pair" | D&C O(n log n). |
| "Count inversions" | D&C merge sort variant. |
| "Compute x^n" | Fast power, O(log n). |
| "Merge sort" | D&C, n log n. |
| "Binary search" | D&C, log n. |
| "FFT / polynomial mult" | D&C, n log n. |
| "Subproblems overlap" | DP, not D&C. |

---

## 9. Quick Revision

```
D&C STEPS
 divide → conquer → combine
 T(n) = a T(n/b) + f(n)

CLASSIC EXAMPLES
 merge sort: 2T(n/2) + n → n log n
 quicksort: avg n log n; worst n²
 binary search: T(n/2) + 1 → log n
 Karatsuba: 3T(n/2) + n → n^log₂3
 Strassen: 7T(n/2) + n² → n^log₂7
 closest pair: 2T(n/2) + n → n log n
 inversion count: n log n
 fast power: log n
 Tower Hanoi: 2ⁿ
 FFT: n log n

MASTER THEOREM
 c = log_b a
 case 1, 2, 3 by f vs n^c

D&C vs DP
 disjoint subproblems → D&C
 overlapping → DP

ASYMMETRIC SPLIT → Akra-Bazzi
```
