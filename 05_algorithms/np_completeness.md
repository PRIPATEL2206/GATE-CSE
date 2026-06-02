# NP-Completeness & Reductions

> Subject: Algorithms
> GATE weight: **1–3 marks** every year. Complexity classes, reductions, classic NP-complete problems.

---

## 1. Concept Explanation

### 1.1 Decision Problems

A **decision problem** has a yes/no answer. Examples:
- Is this graph 3-colorable?
- Is there a Hamiltonian cycle?
- Does this set sum to S?

Algorithm questions are formalized as decision problems for complexity analysis.

### 1.2 Complexity Classes

| Class | Definition |
|---|---|
| **P** | Decidable in polynomial time on deterministic Turing machine |
| **NP** | Verifiable in polynomial time given a "certificate" |
| **co-NP** | Complement is in NP (no-instances verifiable) |
| **NP-hard** | At least as hard as any problem in NP |
| **NP-complete** | NP **and** NP-hard |
| **PSPACE** | Polynomial space |
| **EXPTIME** | Exponential time |

### 1.3 Class Relationships

```
P ⊆ NP ⊆ PSPACE ⊆ EXPTIME
```

**P vs NP:** open problem. Most believe P ≠ NP.

P ⊆ NP-complete only if P = NP.

### 1.4 NP — Verification

A problem is in NP iff a "yes" answer comes with a **polynomial-size certificate** verifiable in polynomial time.

**Example (SAT):** boolean formula has satisfying assignment. Certificate: the assignment.

### 1.5 Reductions

**Polynomial-time many-one reduction (≤_p):**
A ≤_p B iff there's a poly-time function f such that x ∈ A ⇔ f(x) ∈ B.

**Implications:**
- If B ∈ P, then A ∈ P.
- If A is NP-hard, B is NP-hard.

**Use:** to prove B is NP-hard, reduce a known NP-hard A to B.

### 1.6 NP-Hardness Proof Recipe

1. Pick a known NP-hard problem A.
2. Construct poly-time reduction from A to your problem B.
3. Show: A has yes-answer ⇔ B has yes-answer (correctness).
4. Show reduction runs in poly time.

### 1.7 NP-Completeness

A problem B is **NP-complete** iff:
1. B ∈ NP (verification in poly time).
2. B is NP-hard (every problem in NP reduces to B).

To prove B is NP-complete:
- Show B ∈ NP (give certificate + verifier).
- Show B is NP-hard (reduction from known NP-complete to B).

### 1.8 Cook-Levin Theorem

**SAT is NP-complete** (proved 1971).

This is the **first** NP-complete problem; every problem in NP reduces to SAT in polynomial time.

### 1.9 Classic NP-Complete Problems

| Problem | Description |
|---|---|
| **SAT** | Boolean formula satisfiable? |
| **3-SAT** | Boolean CNF with 3 literals/clause |
| **CIRCUIT-SAT** | Boolean circuit satisfiable? |
| **CLIQUE** | Graph has clique of size k? |
| **VERTEX-COVER** | Graph has vertex cover of size k? |
| **INDEPENDENT-SET** | Graph has IS of size k? |
| **HAM-CYCLE** | Graph has Hamiltonian cycle? |
| **TSP (decision)** | Tour of length ≤ k? |
| **SUBSET-SUM** | Subset sums to target? |
| **PARTITION** | Partition into two equal-sum sets? |
| **3-COLOR** | Graph 3-colorable? |
| **KNAPSACK (decision)** | Value ≥ k with weight ≤ W? |
| **SET-COVER** | Cover universe with k sets? |
| **GRAPH-COLORING** | k-colorable? |

### 1.10 Common Reductions

| Reduction | From | To |
|---|---|---|
| 3-SAT → CLIQUE | SAT formula → graph | direct |
| CLIQUE ↔ INDEPENDENT-SET | complement graph | direct |
| INDEPENDENT-SET ↔ VERTEX-COVER | complement set | direct |
| 3-SAT → 3-COLOR | gadgets | non-trivial |
| 3-SAT → HAM-CYCLE | gadgets | non-trivial |
| HAM-CYCLE → TSP | weights 1 / large | direct |
| SUBSET-SUM → KNAPSACK (decision) | direct | direct |

### 1.11 P Problems (in poly time)

- Sorting, searching, BFS/DFS, MST, Dijkstra, etc.
- 2-SAT (linear time).
- Linear Programming (Khachiyan, Karmarkar): polynomial.
- Primality testing (AKS, 2002): polynomial.
- Bipartite matching: polynomial.
- Min cut, max flow: polynomial.

### 1.12 Examples Not Known P or NP-complete

| Problem | Status |
|---|---|
| **Graph isomorphism** | Quasi-poly (2017) |
| **Factoring** | Open; subexponential |
| **Discrete logarithm** | Open |

These are in NP but neither known polynomial nor NP-complete.

### 1.13 NP-Hard but Not NP

NP-hard problems may not be in NP (e.g., Halting Problem is NP-hard but **undecidable**).

### 1.14 Approximation Algorithms

For NP-hard problems:
- **2-approximation for Vertex Cover:** repeatedly pick edge, add both endpoints.
- **2-approximation for Metric TSP** (Christofides: 1.5).
- **Greedy O(log n) for Set Cover.**
- **PTAS** (Polynomial Time Approximation Scheme): (1+ε)-approximation in time poly(n) for fixed ε.

### 1.15 P, NP, Co-NP Relationships

| Class | Examples |
|---|---|
| P | sorting, MST, bipartite matching |
| NP | SAT, CLIQUE, 3-COLOR |
| co-NP | TAUTOLOGY, UNSAT |
| NP ∩ co-NP | factoring, primality (now P) |

P ⊆ NP ∩ co-NP. Whether NP = co-NP is open.

### 1.16 PSPACE-Complete

Problems requiring polynomial space, possibly exponential time:
- TQBF (True Quantified Boolean Formulas)
- Generalized Geography

NP ⊆ PSPACE.

### 1.17 Algorithm Strategies for NP-Hard Problems

| Strategy | Description |
|---|---|
| **Brute force** | Try all possibilities (small n) |
| **Branch and bound** | Prune search space |
| **Dynamic programming** | If pseudo-poly possible |
| **Backtracking** | DFS with pruning |
| **Approximation** | Bounded-ratio solution |
| **Randomized** | Often good in practice |
| **Heuristic** | No bound; e.g., simulated annealing |

### 1.18 Time Hierarchy & Reduction Direction

`A ≤_p B` means **B is at least as hard as A**.

To prove B is NP-hard: reduce **known hard A to B** (B may be harder).

> **Summary:** NP = verifiable in poly time. NP-complete = NP ∩ NP-hard. To prove NPC: show in NP + reduce from known NPC. Memorize core NP-complete problems and reductions among them.

---

## 2. Important Points

- **P ⊆ NP ⊆ PSPACE ⊆ EXPTIME**.
- **P vs NP open**; widely believed P ≠ NP.
- **NP-hard ≠ NP-complete**: NP-complete is the subset of NP-hard that is also in NP.
- **SAT is the first NP-complete problem** (Cook-Levin).
- **Reduction direction matters:** A ≤_p B says B is harder.
- **2-SAT is in P**; **3-SAT is NP-complete**.
- **TSP optimization** is NP-hard; decision version is NP-complete.
- **Subset Sum and Knapsack** are NP-complete (despite pseudo-polynomial DP).
- **Halting Problem** is undecidable, hence NP-hard but not in NP.
- **NP-complete problems** all reduce to each other in polynomial time.
- **Approximation** can give bounded-error solutions in poly time.
- **Co-NP** is for "no" verification (e.g., UNSAT).
- **Vertex Cover and Independent Set** are complements: VC = V − IS.

---

## 3. Short Notes

```
DECISION PROBLEMS: yes/no
COMPLEXITY CLASSES
 P: poly-time decidable
 NP: poly-time verifiable
 co-NP: complement in NP
 NP-hard: ≥ all in NP
 NP-complete: NP ∧ NP-hard
 PSPACE: poly space
 EXPTIME: exponential time

P ⊆ NP ⊆ PSPACE ⊆ EXPTIME
P = NP open
NP ∩ co-NP includes factoring

REDUCTION (≤_p)
 A ≤_p B ⇒ B at least as hard
 prove NP-hard: reduce known NP-hard to B

NP-COMPLETENESS PROOF
 1. B ∈ NP (certificate + verifier)
 2. B is NP-hard (reduction)

COOK-LEVIN: SAT is NP-complete

CLASSIC NPC PROBLEMS
 SAT, 3-SAT, CLIQUE, VC, IS,
 HAM-CYCLE, TSP, SUBSET-SUM,
 PARTITION, 3-COLOR, KNAPSACK (dec), SET-COVER

REDUCTIONS
 3-SAT → CLIQUE
 CLIQUE ↔ IS via complement
 IS ↔ VC: complement in V
 3-SAT → 3-COLOR (gadgets)
 HAM-CYCLE → TSP (weights)
 SUBSET-SUM → KNAPSACK

P PROBLEMS
 sorting, MST, BFS, max flow,
 2-SAT, primality, LP, bipartite matching

UNDECIDABLE
 halting problem (NP-hard, not NP)

APPROXIMATION
 vertex cover: 2-approx (matching)
 metric TSP: 2-approx (MST), Christofides 1.5
 set cover: O(log n)
 PTAS for some

ALGO STRATEGIES (NP-hard)
 brute, DP (pseudo-poly), branch-and-bound,
 backtracking, approximation, randomized, heuristic
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | P ⊆ NP ⊆ PSPACE ⊆ EXPTIME | ✅✅ |
| 2 | NP = poly-time verifiable | ✅✅ |
| 3 | NP-complete = NP + NP-hard | ✅✅ |
| 4 | A ≤_p B: B at least as hard | ✅✅ |
| 5 | Cook-Levin: SAT NP-complete | ✅✅ |
| 6 | 2-SAT in P; 3-SAT NPC | ✅✅ |
| 7 | TSP decision NPC; optimization NP-hard | ✅ |
| 8 | Halting NP-hard; not NP (undecidable) | ✅ |
| 9 | VC = V − IS | ✅ |
| 10 | Approximations: 2-VC, 1.5-Christofides | ✅ |

### Tricks

- **Identify NP-completeness:** can a polynomial verifier check yes-answers?
- **Reduction direction:** known hard → new (proves new hard).
- **For optimization NP-hard:** decision version usually NPC.
- **Pseudo-polynomial:** Subset Sum O(nS) — polynomial in S not log S.
- **Spotting NPC family:** clique, IS, VC, dominating set, set cover.
- **Distinguish hardness:** NP-hard may not be in NP (undecidable, etc.).

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
SAT is:
**Solution.** NP-complete (Cook-Levin).

### Q2. (GATE CSE 2014)
2-SAT is in:
**Solution.** P.

### Q3. (GATE CSE 2018)
A ≤_p B and B ∈ P. Then:
**Solution.** A ∈ P.

### Q4. (GATE CSE 2008)
Halting Problem is:
**Solution.** Undecidable.

### Q5. (GATE CSE 2010)
Vertex Cover ≤_p Independent Set?
**Solution.** Yes (and vice versa).

### Q6. (GATE CSE 2015)
TSP (decision) is:
**Solution.** NP-complete.

### Q7. (GATE CSE 2013)
P = NP if and only if:
**Solution.** Some NP-complete problem is in P.

### Q8. (GATE CSE 2007)
3-coloring of graph is:
**Solution.** NP-complete.

### Q9. (GATE CSE 2003)
Knapsack (decision) is:
**Solution.** NP-complete.

### Q10. (GATE CSE 2009)
Reduction from problem A to B in poly time means:
**Solution.** B at least as hard as A.

### Q11. (GATE CSE 2019)
Co-NP example:
**Solution.** TAUTOLOGY, UNSAT.

### Q12. (GATE CSE 2020)
Approximation factor for vertex cover:
**Solution.** 2 (greedy matching-based).

### Q13. (GATE CSE 2021)
2-approximation for metric TSP uses:
**Solution.** MST traversal.

### Q14. (GATE CSE 2016)
A problem in NP-hard but not in NP:
**Solution.** Halting problem.

### Q15. (GATE CSE 2011)
NP-completeness of 3-SAT proved by:
**Solution.** Cook (1971); reduction from SAT.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define NP.

**P2.** Define NP-complete.

**P3.** P ⊆ NP — true?

**P4.** Cook-Levin theorem statement.

**P5.** Is sorting in P?

**P6.** Is 3-SAT in P?

**P7.** Is Halting Problem in NP?

**P8.** Reduction direction for proving NP-hardness?

**P9.** What's NP-hard?

**P10.** Examples of P problems.

### Medium

**P11.** Reduce 3-SAT to CLIQUE.

**P12.** Reduce CLIQUE to IS.

**P13.** Reduce IS to VC.

**P14.** Reduce SUBSET-SUM to KNAPSACK (decision).

**P15.** Show why 2-SAT is in P.

**P16.** Is Graph Isomorphism known P?

**P17.** Approximation ratio for greedy set cover.

**P18.** Difference between NP and co-NP.

**P19.** Difference between NP-hard and NP-complete.

**P20.** Why is Halting Problem NP-hard?

### Hard

**P21.** Prove 3-SAT is NP-complete.

**P22.** Show Independent Set NP-hard via reduction.

**P23.** Prove TSP optimization is NP-hard.

**P24.** Approximation algorithm for Vertex Cover.

**P25.** Show Subset Sum NP-complete despite pseudo-polynomial DP.

**P26.** Reductions among 6 classic NPC problems (graph).

**P27.** Compare PSPACE vs NP.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | poly-time verifiable | direct |
| P2 | NP + NP-hard | direct |
| P3 | yes | direct |
| P4 | SAT is NP-complete | direct |
| P5 | yes | direct |
| P6 | no (NP-complete) | direct |
| P7 | no (undecidable) | direct |
| P8 | known hard → new | direct |
| P9 | every NP problem reduces to it | direct |
| P10 | sorting, MST, BFS, etc. | direct |
| P11 | gadgets per clause | direct |
| P12 | complement graph | direct |
| P13 | V − IS | direct |
| P14 | weight = value | direct |
| P15 | implication graph SCC | direct |
| P16 | quasi-polynomial since 2017 | direct |
| P17 | O(log n) | direct |
| P18 | yes vs no verification | direct |
| P19 | NPC ⊂ NP-hard, also ∈ NP | direct |
| P20 | reduce SAT → Halting | direct |
| P21 | reduction from SAT to 3-SAT | direct |
| P22 | reduce CLIQUE | direct |
| P23 | reduce HAM-CYCLE | direct |
| P24 | matching-based | direct |
| P25 | input encoding length log S | direct |
| P26 | trace reductions | direct |
| P27 | NP ⊆ PSPACE | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | NP = "non-polynomial" (wrong) | NP = nondeterministic poly. |
| 2 | Treating NP-hard as NP-complete | NP-complete is NP-hard ∩ NP. |
| 3 | Reduction direction confusion | Reduce known hard → new. |
| 4 | Halting Problem as NP-complete | Undecidable, hence not in NP. |
| 5 | Subset Sum is in P (myth) | NPC; pseudo-polynomial DP. |
| 6 | 2-SAT vs 3-SAT same | 2-SAT in P; 3-SAT NPC. |
| 7 | TSP optimization in NP | Optimization usually NP-hard, not NP. |
| 8 | Approximation for any NP-hard | Some are inapproximable. |
| 9 | P = NP proof by example | Need general argument. |
| 10 | NP-complete problems differ in difficulty | All equivalent under poly reductions. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Is X in P?" | Find polynomial algorithm or known result. |
| "Prove X NP-complete" | Show NP + reduce known NPC to X. |
| "X reduces to Y; X NP-hard. Is Y?" | Yes, Y at least as hard. |
| "X reduces to Y; Y in P. Is X?" | Yes, X in P. |
| "Approximation factor" | 2 for VC, 1.5 for metric TSP, log n for set cover. |
| "Pseudo-polynomial" | Subset sum, knapsack — depend on numeric value. |
| "Decision vs optimization" | Decision usually NPC; optimization NP-hard. |
| "Halting problem" | Undecidable; NP-hard; not NP. |
| "P vs NP" | Open. |
| "Cook-Levin" | SAT NP-complete. |

---

## 9. Quick Revision

```
COMPLEXITY CLASSES
 P ⊆ NP ⊆ PSPACE ⊆ EXPTIME
 NP = poly-time verifiable
 co-NP = complement in NP
 NP-hard = at least as hard as any NP
 NP-complete = NP ∧ NP-hard

REDUCTION (≤_p)
 A ≤_p B: B at least as hard
 prove NP-hard: reduce known NPC → new

COOK-LEVIN: SAT is NP-complete (first)

CLASSIC NPC
 SAT, 3-SAT, CLIQUE, IS, VC, HAM, TSP,
 SUBSET-SUM, PARTITION, 3-COLOR,
 KNAPSACK (dec), SET-COVER

P EXAMPLES
 sorting, MST, BFS/DFS, 2-SAT, max flow,
 LP, primality (AKS), bipartite matching

UNDECIDABLE: Halting Problem

APPROXIMATIONS
 VC: 2 (matching)
 metric TSP: 2 (MST), 1.5 (Christofides)
 set cover: O(log n)
 PTAS for some

PSEUDO-POLYNOMIAL
 subset sum, knapsack: O(nS) — poly in S not log S
```
