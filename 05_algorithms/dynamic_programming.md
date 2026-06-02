# Dynamic Programming

> Subject: Algorithms
> GATE weight: **3–6 marks** every year. Most heavily tested algorithm topic. Knapsack, LCS, MCM, shortest paths, edit distance.

---

## 1. Concept Explanation

### 1.1 Dynamic Programming Idea

DP solves problems by:
1. **Optimal substructure:** optimal solution composed of optimal subproblem solutions.
2. **Overlapping subproblems:** same subproblems recur many times → memoize.

DP avoids recomputation by storing solutions.

### 1.2 Two Approaches

| Approach | Description |
|---|---|
| **Top-down (memoization)** | Recursion + cache; computes only needed subproblems |
| **Bottom-up (tabulation)** | Iterative; fills table in order |

Both have same time complexity; tabulation typically uses less constant overhead.

### 1.3 DP vs D&C vs Greedy

| Approach | Subproblems | Choice |
|---|---|---|
| D&C | Disjoint, no reuse | Recurse |
| Greedy | Decision narrows search | Locally optimal |
| DP | Overlap, reused | All options + memoize |

### 1.4 Recipe for DP

1. Define state (parameters).
2. Write recurrence (transition).
3. Identify base case(s).
4. Identify order to fill table.
5. Compute final answer.

### 1.5 Fibonacci (canonical example)

Naive recursion: T(n) = T(n−1) + T(n−2) + 1 → O(φⁿ).

**DP (memoization or tabulation):** O(n).

```python
fib[0] = 0; fib[1] = 1
for i in 2..n:
  fib[i] = fib[i-1] + fib[i-2]
```

### 1.6 0/1 Knapsack

n items with weight wᵢ, value vᵢ; capacity W. Maximize total value.

**State:** dp[i][w] = max value using first i items with capacity w.

**Recurrence:**
```
dp[i][w] = max(
  dp[i-1][w],                      # don't take i
  dp[i-1][w-w_i] + v_i              # take i (if w >= w_i)
)
```

**Base:** dp[0][w] = 0; dp[i][0] = 0.

**Time:** O(n · W). **Space:** O(n · W) (or O(W) with rolling array).

### 1.7 Unbounded Knapsack

Each item can be taken any number of times.

```
dp[w] = max(dp[w], dp[w - w_i] + v_i) for each i
```

Time: O(n · W).

### 1.8 Coin Change (Min Coins)

Coins {c₁, …, cₖ}, amount W. Min coins.

```
dp[0] = 0; dp[i] = ∞ for i > 0
for w in 1..W:
  for c in coins:
    if w >= c:
      dp[w] = min(dp[w], dp[w-c] + 1)
```

Time: O(W · k).

**Variant: # of ways:**
```
dp[0] = 1
for c in coins:
  for w in c..W:
    dp[w] += dp[w-c]
```

### 1.9 Longest Common Subsequence (LCS)

Two strings X (length m), Y (length n). Find longest subsequence in both.

**State:** dp[i][j] = LCS length of X[0..i], Y[0..j].

**Recurrence:**
```
if X[i] == Y[j]: dp[i][j] = dp[i-1][j-1] + 1
else:           dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

**Time/Space:** O(m · n).

### 1.10 Longest Increasing Subsequence (LIS)

Find longest strictly increasing subsequence in array.

**O(n²) DP:**
```
dp[i] = 1 + max(dp[j] for j < i if a[j] < a[i])
```

**O(n log n) (patience sorting):** maintain end-of-sequence array using binary search.

### 1.11 Edit Distance (Levenshtein)

Min operations (insert, delete, replace) to transform string X into Y.

**State:** dp[i][j] = edit distance for X[0..i], Y[0..j].

**Recurrence:**
```
if X[i] == Y[j]: dp[i][j] = dp[i-1][j-1]
else:           dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
```

**Time/Space:** O(m · n).

### 1.12 Matrix Chain Multiplication

Optimize parenthesization of matrix products to minimize scalar multiplications.

n matrices, dimensions p₀ × p₁ × p₂ × … × pₙ.

**State:** m[i][j] = min cost to multiply Aᵢ … Aⱼ.

**Recurrence:**
```
m[i][j] = min over k from i to j-1:
  m[i][k] + m[k+1][j] + p_{i-1} · p_k · p_j
```

**Base:** m[i][i] = 0.

**Time:** O(n³). **Space:** O(n²).

### 1.13 All-Pairs Shortest Path (Floyd-Warshall)

For weighted directed graph, find shortest paths between all pairs.

**State:** dp[k][i][j] = shortest path from i to j using only vertices 1..k as intermediate.

**Recurrence:**
```
dp[k][i][j] = min(dp[k-1][i][j], dp[k-1][i][k] + dp[k-1][k][j])
```

**Time:** O(V³). **Space:** O(V²) using rolling.

Detects negative cycles via diagonal.

### 1.14 Bellman-Ford

Single-source shortest path with possibly negative edges.

**Relax all edges V−1 times:**
```
for i in 1..V-1:
  for each edge (u, v, w):
    if dist[u] + w < dist[v]:
      dist[v] = dist[u] + w
```

**Time:** O(V · E).

If a relaxation is possible after V−1 iterations → negative cycle.

### 1.15 Subset Sum

Decide if some subset of {a₁, …, aₙ} sums to S.

**State:** dp[i][s] = true if some subset of first i elements sums to s.

**Recurrence:**
```
dp[i][s] = dp[i-1][s] OR dp[i-1][s - a_i]
```

**Time:** O(n · S).

### 1.16 Rod Cutting

Rod of length n; price[i] = price for piece of length i. Maximize revenue.

```
dp[0] = 0
for i in 1..n:
  dp[i] = max(price[j] + dp[i-j]) for j in 1..i
```

Time: O(n²).

### 1.17 Catalan-style DP

Count of binary trees / ways to triangulate polygon, etc.

`C(n) = Σ_{i=0}^{n-1} C(i) · C(n-1-i)` → O(n²).

### 1.18 Common DP Patterns

| Pattern | Examples |
|---|---|
| **Sequence** | LIS, LCS, edit distance |
| **Knapsack** | 0/1, unbounded, subset sum |
| **Interval / range** | MCM, palindrome partitioning |
| **Tree DP** | Independent set on tree, tree diameter |
| **Bitmask DP** | TSP exponential, set cover |
| **Probability DP** | Expected value, Markov-like |

### 1.19 Space Optimization

Many DP problems use **rolling arrays** to reduce O(n) → O(1) per dimension.

E.g., 0/1 knapsack: dp[w] (1D) updated in reverse order.

### 1.20 DP with State Encoding

For TSP: dp[mask][last] = min cost visiting set "mask" ending at "last".
**Time:** O(2ⁿ · n²). Exponential but exact.

> **Summary:** Master DP recurrences for: 0/1 knapsack, LCS, LIS, MCM, edit distance, coin change, Floyd-Warshall, Bellman-Ford. Recognize overlapping subproblems; build state and transitions.

---

## 2. Important Points

- **DP needs both** optimal substructure AND overlapping subproblems.
- **Top-down memoization** is recursion with cache.
- **Bottom-up tabulation** is iterative.
- **0/1 Knapsack:** O(nW) — pseudo-polynomial.
- **LCS / Edit distance / LIS:** O(mn) or O(n² / n log n).
- **MCM:** O(n³).
- **Floyd-Warshall:** O(V³); detects negative cycles.
- **Bellman-Ford:** O(VE); handles negative weights.
- **Coin change number-of-ways** vs min-coins: different transitions.
- **Pseudo-polynomial:** depends on numeric input value (W, S).
- **For tree DP:** define DP on root with subtree info.
- **For bitmask DP:** state = subset; useful for n ≤ ~20.
- **DP space optimization** via rolling arrays.
- **Many problems have multiple DP formulations** with different complexity.

---

## 3. Short Notes

```
DP PRINCIPLES
 optimal substructure
 overlapping subproblems

APPROACHES
 top-down (memoization)
 bottom-up (tabulation)

CLASSIC PROBLEMS

0/1 KNAPSACK
 dp[i][w] = max(dp[i-1][w], dp[i-1][w-w_i] + v_i)
 O(nW)

UNBOUNDED KNAPSACK
 dp[w] = max(dp[w], dp[w-w_i] + v_i)
 O(nW)

COIN CHANGE (min)
 dp[w] = min over c: dp[w-c] + 1
 O(Wk)

COIN CHANGE (# ways)
 dp[w] += dp[w-c]
 O(Wk)

LCS
 dp[i][j] = dp[i-1][j-1] + 1 if X[i] == Y[j]
        else max(dp[i-1][j], dp[i][j-1])
 O(mn)

LIS
 O(n²) basic; O(n log n) patience sort

EDIT DISTANCE
 1 + min(insert, delete, replace) when chars differ
 O(mn)

MCM
 m[i][j] = min over k: m[i][k] + m[k+1][j] + p_{i-1}·p_k·p_j
 O(n³)

FLOYD-WARSHALL
 dp[k][i][j] = min(dp[k-1][i][j], dp[k-1][i][k] + dp[k-1][k][j])
 O(V³); negative cycle iff diagonal < 0

BELLMAN-FORD
 V−1 relaxations
 O(VE); negative cycle: extra relaxation possible

SUBSET SUM
 dp[i][s] = dp[i-1][s] OR dp[i-1][s-a_i]
 O(nS)

ROD CUTTING
 dp[i] = max(price[j] + dp[i-j])
 O(n²)

PATTERNS
 sequence DP
 knapsack DP
 interval DP
 tree DP
 bitmask DP
 probability DP

SPACE: rolling arrays often reduce dim
```

---

## 4. Formulas / Tricks

| # | Recurrence | Time | Memorize Cold? |
|---|---|---|---|
| 1 | LCS: dp[i-1][j-1]+1 or max(left, top) | O(mn) | ✅✅✅ |
| 2 | 0/1 Knapsack: max(skip, take) | O(nW) | ✅✅✅ |
| 3 | Edit dist: min(insert, del, replace) | O(mn) | ✅✅ |
| 4 | LIS: max(dp[j])+1 | O(n²) or O(n log n) | ✅✅ |
| 5 | MCM: min over k: m[i][k]+m[k+1][j]+pᵢ₋₁ pₖ pⱼ | O(n³) | ✅✅ |
| 6 | Coin change min/count | O(Wk) | ✅ |
| 7 | Floyd-Warshall | O(V³) | ✅✅ |
| 8 | Bellman-Ford | O(VE) | ✅ |
| 9 | Subset sum | O(nS) | ✅ |
| 10 | Rod cutting | O(n²) | ✅ |
| 11 | Catalan DP | O(n²) | ✅ |
| 12 | TSP bitmask DP | O(2ⁿ n²) | ✅ |

### Tricks

- **For DP problems:** define state precisely; identify base; check transitions.
- **Use 1D rolling array** for knapsack-like problems: iterate w in reverse for 0/1, forward for unbounded.
- **For LCS reconstruction:** trace back from dp[m][n] using transitions.
- **For LIS in O(n log n):** binary search end-of-LIS array.
- **For MCM:** iterate by length of subchain.
- **Floyd-Warshall** also works for transitive closure (replace min with OR).
- **Bellman-Ford** works for any directed graph; detects negative cycles.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
0/1 knapsack time complexity:
**Solution.** O(nW) (pseudo-polynomial).

### Q2. (GATE CSE 2014)
LCS of "ABCBDAB" and "BDCAB":
**Solution.** "BCAB" or "BDAB" — length 4.

### Q3. (GATE CSE 2018)
MCM dimensions p = [10, 20, 30, 40]. Min multiplications?
**Solution.** Compute m[i][j] for n=3 matrices: 18000 (10·20·40 + 10·30·20 path = 6000 + 8000 = 14000? recompute) — try ((A1·A2)·A3): 10·20·30 + 10·30·40 = 6000 + 12000 = 18000. (A1·(A2·A3)): 20·30·40 + 10·20·40 = 24000 + 8000 = 32000. **Min = 18000**.

### Q4. (GATE CSE 2008)
Floyd-Warshall time:
**Solution.** O(V³).

### Q5. (GATE CSE 2010)
Bellman-Ford detects:
**Solution.** Negative cycles.

### Q6. (GATE CSE 2015)
LIS of [10, 22, 9, 33, 21, 50, 41, 60]:
**Solution.** Length 5: e.g., 10, 22, 33, 41, 60.

### Q7. (GATE CSE 2013)
Edit distance "kitten" → "sitting":
**Solution.** 3 (substitute k→s, e→i, insert g).

### Q8. (GATE CSE 2007)
DP optimal substructure required for:
**Solution.** All DP problems.

### Q9. (GATE CSE 2003)
Coin change: # of ways to make 5 with {1, 2, 5}:
**Solution.** {5}, {2,2,1}, {2,1,1,1}, {1,1,1,1,1} = 4 ways.

### Q10. (GATE CSE 2009)
Subset sum O(nS) — pseudo-polynomial?
**Solution.** Yes — depends on S.

### Q11. (GATE CSE 2019)
Catalan DP for binary trees:
**Solution.** C(n) = Σ C(i)·C(n-1-i).

### Q12. (GATE CSE 2020)
0/1 knapsack with rolling array uses:
**Solution.** O(W) space.

### Q13. (GATE CSE 2021)
Floyd-Warshall handles negative weights?
**Solution.** Yes (no negative cycles).

### Q14. (GATE CSE 2016)
LIS in O(n log n) uses:
**Solution.** Binary search on patience array.

### Q15. (GATE CSE 2011)
Longest Palindromic Subsequence is a variant of:
**Solution.** LCS (with reverse string).

---

## 6. Practice Questions (20+)

### Easy

**P1.** State DP requirements.

**P2.** Knapsack 0/1 time complexity?

**P3.** LCS time?

**P4.** Edit distance time?

**P5.** Floyd-Warshall time?

**P6.** Bellman-Ford time?

**P7.** MCM time?

**P8.** Subset sum time?

**P9.** Difference between top-down and bottom-up?

**P10.** Pseudo-polynomial means?

### Medium

**P11.** LCS of "AGCAT" and "GAC".

**P12.** 0/1 knapsack: items (w,v) = (1,1),(2,2),(3,5); W=4. Max value?

**P13.** Coin change (# ways): coins {1,2,5}, W=5.

**P14.** LIS of [3, 10, 2, 1, 20].

**P15.** Edit distance "horse" to "ros".

**P16.** MCM: p = [5, 10, 3, 12, 5]. Min ops?

**P17.** Subset sum for {3, 34, 4, 12, 5, 2}, S=9.

**P18.** Floyd-Warshall on 4-vertex graph.

**P19.** Bellman-Ford with negative weights graph.

**P20.** Rod cutting: rod length 8, prices [1, 5, 8, 9, 10, 17, 17, 20].

### Hard

**P21.** Implement 0/1 knapsack with O(W) space.

**P22.** LIS in O(n log n) — explain algorithm.

**P23.** TSP bitmask DP for n=4.

**P24.** Longest palindromic subsequence DP.

**P25.** Egg dropping DP problem.

**P26.** Maximum sum subarray with at most one reverse.

**P27.** Optimal binary search tree DP.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | optimal substructure + overlap | direct |
| P2 | O(nW) | direct |
| P3 | O(mn) | direct |
| P4 | O(mn) | direct |
| P5 | O(V³) | direct |
| P6 | O(VE) | direct |
| P7 | O(n³) | direct |
| P8 | O(nS) | direct |
| P9 | recursion+memo vs iterative table | direct |
| P10 | poly in numerical input value | direct |
| P11 | "GA" — length 2 | direct |
| P12 | 6 (items 2 and 3) | direct |
| P13 | 4 ways | direct |
| P14 | 3 (3,10,20) | direct |
| P15 | 3 | direct |
| P16 | trace MCM table | direct |
| P17 | yes (4+5 or 4+3+2) | direct |
| P18 | trace | direct |
| P19 | trace | direct |
| P20 | 22 | direct |
| P21 | 1D array, iterate w in reverse | direct |
| P22 | maintain end-of-LIS via binary search | direct |
| P23 | 16 states × 4 last; trace | direct |
| P24 | LCS of s and reverse(s) | direct |
| P25 | DP on (eggs, floors) | direct |
| P26 | DP with extra dimension | direct |
| P27 | DP on intervals with prob | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing DP and D&C | Overlap is the test. |
| 2 | Top-down vs bottom-up: same answer | Yes, but bottom-up often faster. |
| 3 | 0/1 knapsack: wrong iteration order in 1D | Iterate w from W to wᵢ. |
| 4 | Coin change min vs count: same recurrence (myth) | Different transitions. |
| 5 | LIS strict vs non-strict | Specify carefully. |
| 6 | MCM forgetting dimensions | Use p_{i-1}·p_k·p_j carefully. |
| 7 | Bellman-Ford ignoring negative cycle check | Run V−1 times then check. |
| 8 | Floyd-Warshall on negative cycles | Diagonal becomes negative. |
| 9 | Subset sum exponential without DP | DP makes it pseudo-polynomial. |
| 10 | Edit distance: not symmetric | Same min ops apply both directions. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Knapsack" | DP O(nW). |
| "Longest common subsequence / substring" | LCS DP. |
| "Edit distance" | DP O(mn). |
| "LIS" | O(n²) or O(n log n). |
| "Matrix chain" | MCM O(n³). |
| "All-pairs shortest path" | Floyd-Warshall O(V³). |
| "Single-source negative weights" | Bellman-Ford. |
| "Subset sum / partition" | Subset sum DP. |
| "Coin change" | DP. |
| "TSP small n" | Bitmask DP O(2ⁿ n²). |
| "Optimal BST" | Interval DP. |
| "Longest palindrome" | LCS variant. |

---

## 9. Quick Revision

```
DP PRINCIPLES
 optimal substructure + overlapping subproblems

APPROACHES
 top-down (memoization)
 bottom-up (tabulation)

KEY PROBLEMS
 0/1 KNAPSACK: O(nW)
 UNBOUNDED KNAPSACK: O(nW)
 COIN CHANGE: O(Wk)
 LCS: O(mn)
 LIS: O(n²) or O(n log n)
 EDIT DIST: O(mn)
 MCM: O(n³)
 FLOYD-WARSHALL: O(V³)
 BELLMAN-FORD: O(VE)
 SUBSET SUM: O(nS)
 ROD CUTTING: O(n²)
 TSP (bitmask): O(2ⁿ n²)

PSEUDO-POLY: depends on numeric input value

PATTERNS
 sequence, knapsack, interval, tree, bitmask, probability

SPACE
 rolling arrays often reduce dim
```
