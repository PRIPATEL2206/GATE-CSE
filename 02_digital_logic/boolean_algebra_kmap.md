# Boolean Algebra & K-Maps

> Subject: Digital Logic
> GATE weight: **3–5 marks** every year. Boolean simplification, SOP/POS, K-Map minimization, NAND/NOR universality.

---

## 1. Concept Explanation

### 1.1 Boolean Variables & Operations

A **Boolean variable** ∈ {0, 1}. Three primary operations:

| Op | Symbol | Truth Table |
|---|---|---|
| AND | · or ∧ | 0·0=0, 0·1=0, 1·0=0, 1·1=1 |
| OR | + or ∨ | 0+0=0, 0+1=1, 1+0=1, 1+1=1 |
| NOT | ¬ or ' or overbar | ¬0=1, ¬1=0 |

### 1.2 Boolean Algebra Laws

| Law | Form (AND) | Form (OR) |
|---|---|---|
| Identity | A · 1 = A | A + 0 = A |
| Null/Domination | A · 0 = 0 | A + 1 = 1 |
| Idempotent | A · A = A | A + A = A |
| Complement | A · A' = 0 | A + A' = 1 |
| Double negation | (A')' = A | — |
| Commutative | A · B = B · A | A + B = B + A |
| Associative | A(BC) = (AB)C | A + (B+C) = (A+B) + C |
| Distributive | A(B+C) = AB + AC | A + BC = (A+B)(A+C) |
| Absorption | A(A+B) = A | A + AB = A |
| Consensus | AB + A'C + BC = AB + A'C | (A+B)(A'+C)(B+C) = (A+B)(A'+C) |
| **De Morgan** | (AB)' = A' + B' | (A+B)' = A' · B' |

### 1.3 SOP and POS Forms

**Sum of Products (SOP):** OR of AND terms (literals).
Example: `F = AB' + A'B + BC`

**Product of Sums (POS):** AND of OR terms.
Example: `F = (A + B)(A' + C)(B + C')`

**Canonical SOP (Minterms):** every term contains all variables.
**Canonical POS (Maxterms):** every term contains all variables.

### 1.4 Minterms & Maxterms

For n variables, 2ⁿ minterms (or maxterms).

**Minterm m_i:** 1 in row i of truth table.
**Maxterm M_i:** 0 in row i of truth table.

| Row (ABC) | Minterm | Maxterm |
|---|---|---|
| 000 | A'B'C' = m₀ | A+B+C = M₀ |
| 001 | A'B'C = m₁ | A+B+C' = M₁ |
| 010 | A'BC' = m₂ | A+B'+C = M₂ |
| … | … | … |
| 111 | ABC = m₇ | A'+B'+C' = M₇ |

**Function:** `F = Σm(...)` (sum of minterms where F=1) or `F = ΠM(...)` (product of maxterms where F=0).

`Σm(0,2,5,7)` and `ΠM(1,3,4,6)` represent the **same** function.

### 1.5 Karnaugh Map (K-Map)

Geometric tool to minimize Boolean expressions for up to 4–6 variables.

**Layout (3-var, 4-var):**

3-var (A; BC) — Gray code on BC:
```
       BC=00  01  11  10
  A=0    m0   m1  m3  m2
  A=1    m4   m5  m7  m6
```

4-var (AB; CD) — Gray code on both:
```
        CD=00  01  11  10
  AB=00   m0   m1  m3  m2
  AB=01   m4   m5  m7  m6
  AB=11  m12  m13 m15 m14
  AB=10   m8   m9 m11 m10
```

### 1.6 K-Map Procedure

1. Plot 1's at minterm positions (or 0's for POS).
2. Group adjacent 1's in **rectangular** groups of size 1, 2, 4, 8, 16 (powers of 2).
3. Larger groups give simpler terms.
4. Each group = a product term:
   - Variables that **don't change** within the group appear (uncomplemented if 1, complemented if 0).
   - Variables that change are eliminated.
5. Cover all 1's with the **minimum** number of largest groups.

**Edge wrap-around:** opposite edges and corners are adjacent.

### 1.7 Don't-Care Conditions

Some input combinations never occur (e.g., invalid BCD codes 1010–1111). They can be assigned 0 or 1 to **enlarge groups** and minimize.

Notation: `F = Σm(0,2,5) + d(7,8)`.

### 1.8 Implicants

- **Implicant:** any product term where F = 1.
- **Prime implicant (PI):** implicant that cannot be combined with another to form a larger group.
- **Essential prime implicant (EPI):** PI that covers a minterm not covered by any other PI.

**Minimal SOP:** EPIs + extra PIs to cover remaining minterms.

### 1.9 Quine–McCluskey (tabular)

Algorithmic method for any number of variables. Steps:
1. List all minterms in binary.
2. Group by # of 1's; combine pairs differing by 1 bit.
3. Repeat to find PIs.
4. Construct PI chart; find EPIs; cover the rest minimally.

### 1.10 Universal Gates

**NAND (¬AND)** and **NOR (¬OR)** are **universal** — any Boolean function can be implemented using only NAND, or only NOR.

| Gate | Built using NAND | Built using NOR |
|---|---|---|
| NOT | A NAND A | A NOR A |
| AND | (A NAND B) NAND (A NAND B) | (A NOR A) NOR (B NOR B) |
| OR | (A NAND A) NAND (B NAND B) | (A NOR B) NOR (A NOR B) |

### 1.11 XOR / XNOR

**XOR:** A ⊕ B = AB' + A'B (1 when inputs differ).

| Property |
|---|
| A ⊕ 0 = A |
| A ⊕ 1 = A' |
| A ⊕ A = 0 |
| A ⊕ A' = 1 |
| Associative & commutative |
| Distributive over AND not OR |

**XNOR (equivalence):** A ⊙ B = AB + A'B' = (A ⊕ B)'.

### 1.12 Function Counting

For n Boolean inputs:
- # distinct Boolean functions = `2^(2ⁿ)`.
- # symmetric functions = ... (rare in GATE).
- # self-dual functions = `2^(2^(n−1))`.

> **Summary:** Master Boolean laws, SOP/POS, K-Map (3-var/4-var/5-var), don't-cares, NAND/NOR universality. K-Map up to 4 variables is the GATE workhorse — be fast and accurate.

---

## 2. Important Points

- **De Morgan** is the bread and butter of all Boolean simplification.
- **Distributive law for OR** over AND (A + BC = (A+B)(A+C)) is unique to Boolean — different from arithmetic.
- A function with n variables has **2ⁿ minterms** total — one per row.
- **Σm and ΠM are duals**: the maxterms missing from one are the minterms missing from the other.
- **K-map adjacency:** cells differ by exactly one bit (Gray-coded labels).
- **Group sizes:** must be 1, 2, 4, 8, 16 — never 3, 5, 6, etc.
- Don't-cares can be 1 (used in group) or 0 (ignored) — pick whichever helps.
- **EPIs are mandatory**; cover them first.
- **NAND-only / NOR-only realizations** require De Morgan transformations.
- **XOR is its own inverse:** A ⊕ B ⊕ B = A.
- A function is **self-dual** if F(A,B,C,…) = F'(A',B',C',…).
- **Number of literals** in a minimal expression measures cost (gate inputs).

---

## 3. Short Notes

```
OPERATIONS
 AND (·): 1 only when all 1
 OR (+): 1 if any 1
 NOT ('): flip

LAWS (mnemonic CIDIDA + DM + Abs + Cons)
 Identity:  A·1 = A; A+0 = A
 Null:      A·0 = 0; A+1 = 1
 Idempotent: A·A=A; A+A=A
 Complement: A·A'=0; A+A'=1
 Distrib:   A(B+C)=AB+AC; A+BC=(A+B)(A+C)
 Absorption: A(A+B)=A; A+AB=A
 Consensus: AB+A'C+BC = AB+A'C
 De Morgan: (AB)'=A'+B'; (A+B)'=A'·B'

CANONICAL FORMS
 SOP: sum of minterms F=Σm(...)
 POS: product of maxterms F=ΠM(...)
 minterm m_i: row i where F=1
 maxterm M_i: row i where F=0
 m_i and M_i are complements

K-MAP
 cells in Gray code adjacency
 group sizes: 1,2,4,8,16
 each group → one product term
 dropped variables = those that change

DON'T CARES (d, X)
 use to make bigger groups

IMPLICANTS
 PI: maximal group
 EPI: PI covering a unique minterm
 minimal SOP: all EPIs + cover rest

UNIVERSAL GATES
 NAND, NOR (each alone)
 NOT: A NAND A or A NOR A

XOR
 A⊕B = AB'+A'B
 A⊕A=0, A⊕0=A, A⊕1=A', A⊕A'=1
 associative + commutative

# distinct fns of n vars = 2^(2ⁿ)
```

---

## 4. Formulas / Tricks

| # | Identity | Memorize Cold? |
|---|---|---|
| 1 | A · 0 = 0; A · 1 = A | ✅✅ |
| 2 | A + 1 = 1; A + 0 = A | ✅✅ |
| 3 | A + A' = 1; A · A' = 0 | ✅✅ |
| 4 | A + A = A; A · A = A | ✅ |
| 5 | (A')' = A | ✅ |
| 6 | A + AB = A (absorption) | ✅✅ |
| 7 | A + A'B = A + B (NOT absorption — useful!) | ✅✅ |
| 8 | A(A+B) = A | ✅ |
| 9 | (AB)' = A' + B' (DM) | ✅✅✅ |
| 10 | (A+B)' = A'B' (DM) | ✅✅✅ |
| 11 | A + BC = (A + B)(A + C) | ✅ |
| 12 | Consensus: AB + A'C + BC = AB + A'C | ✅ |
| 13 | NAND/NOR universal | ✅✅ |
| 14 | A ⊕ B = AB' + A'B | ✅✅ |
| 15 | A ⊙ B = AB + A'B' = (A ⊕ B)' | ✅ |
| 16 | # Boolean fns of n vars = 2^(2ⁿ) | ✅ |

### Tricks

- **The "secret" rule:** `A + A'B = A + B` (eliminates the A' part of B from A's term). Saves many K-map manipulations.
- **De Morgan iteratively:** any complemented compound expression can be expanded.
- **For NAND-only realization:** turn AND-OR into NAND-NAND using DM.
- **For NOR-only realization:** turn OR-AND into NOR-NOR using DM.
- **Bubble pushing:** use DM to move complement bubbles through gates.
- **K-map shortcut:** start with the largest possible group; cover EPIs first; resolve overlaps last.
- **Wrap-around:** corners of 4-variable map are all adjacent.
- **Don't-care strategic assignment:** assign 1's to extend groups; 0's only when no benefit.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Minimize: `F = AB + A'B' + AB'`.
**Solution.** = AB + AB' + A'B' = A(B+B') + A'B' = A + A'B' = A + B' (using A+A'B=A+B).
**Answer: A + B'.**

### Q2. (GATE CSE 2014)
Express F = Σm(1, 3, 5, 7) on 3 variables (A, B, C). Simplify.
**Solution.** Minterms 1,3,5,7 are all C=1. **F = C.**

### Q3. (GATE CSE 2018)
Number of essential prime implicants of `F(A,B,C,D) = Σm(0, 2, 5, 7, 8, 10, 13, 15)`:
**Solution.** Plot K-map; identify PIs; mark EPIs.
- Group {0,2,8,10}: B'D'
- Group {5,7,13,15}: BD
EPIs: B'D' and BD. **2 EPIs.**

### Q4. (GATE CSE 2008)
The minimum SOP of `F = Σm(0,1,2,5,8,9,10)`:
**Solution.** Combine pairs/quads in K-map (4 vars).
Groups: B'C' (covers 0,1,8,9), AB'D' (covers 8,10), A'C'D' (covers 0,2)... Final compact form: `B'C' + B'D' + A'CD` (representative).

### Q5. (GATE CSE 2010)
NAND universality: implement F = AB + CD using only NAND gates.
**Solution.**
- AB = NAND(NAND(A,B), NAND(A,B))
- CD same
- AB + CD = ¬(¬(AB) · ¬(CD)) = NAND(NAND(A,B), NAND(C,D))
Total: 3 NANDs (after simplification 5 NANDs).

### Q6. (GATE CSE 2015)
Boolean expression for `F = (A+B)(B+C)(C+A)`:
**Solution.** Expand: ABC + AB' AC + BC + … (use distribution + absorption).
Simplification: F = AB + BC + CA. *(Pattern: 2-out-of-3 majority → equivalent to AB + BC + CA.)*

### Q7. (GATE CSE 2013)
The complement of `F = AB + A'B' + B'C` is:
**Solution.** F' = (AB + A'B' + B'C)'. Apply DM:
F' = (AB)'(A'B')'(B'C)' = (A'+B')(A+B)(B+C')
Simplify (long): use truth table to verify.

### Q8. (GATE CSE 2007)
Given `F = AB' + A'B + BC`, # of minterms?
**Solution.** Plot truth table or expand each term to canonical:
Minterms: 100, 011, 001, 010 (depending on which terms cover) — count distinct.
Standard answer: **5 minterms**.

### Q9. (GATE CSE 2016)
The function `F(A,B,C,D)` = AB + AB'C + A'C'D' has how many literals (in the minimum SOP)?
**Solution.** Simplify: AB + AB'C = A(B + B'C) = A(B + C); so F = AB + AC + A'C'D'. Literals: 2 + 2 + 3 = 7.
**Answer: 7 literals.**

### Q10. (GATE CSE 2003)
Realize XOR using 4 NAND gates.
**Solution.** Standard: A⊕B = NAND(NAND(A, NAND(A,B)), NAND(B, NAND(A,B))).

### Q11. (GATE CSE 2009)
Number of distinct Boolean functions of 3 variables:
**Solution.** 2^(2³) = 256.

### Q12. (GATE CSE 2019)
Simplify F = (A+B)(A'+C)(B+C):
**Solution.** Consensus (POS form): the BC-style term is redundant. F = (A+B)(A'+C).

### Q13. (GATE CSE 2020)
Truth table for F has 1s at minterms 1, 4, 5, 6, 7. Minimal SOP:
**Solution.** K-map (3-var): {4,5,6,7} = A; {1,5} = ... wait: {1} is m1 = A'B'C; {4,5,6,7} = A. Cover: F = A + A'B'C = A + B'C.
**Answer: A + B'C.**

### Q14. (GATE CSE 2021)
F(A,B,C) = A ⊕ B ⊕ C is:
**Solution.** Odd parity function — 1 when odd # of inputs are 1.

### Q15. (GATE CSE 2011)
Convert (A + B'C) to NAND-only form:
**Solution.** A + B'C = ((A + B'C)')' = ¬(A'(B'C)') = ¬(A' · (B + C')) — implement via NANDs after DM.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Truth table of A AND B.

**P2.** Truth table of A NAND B.

**P3.** Apply De Morgan to (AB)'.

**P4.** Simplify A + AB.

**P5.** Simplify A·1 + A·0.

**P6.** Simplify A + A'.

**P7.** Find F if F = Σm(0,2,4,6) on 3-var.

**P8.** Apply absorption: AB + A.

**P9.** Express A ⊕ B in SOP.

**P10.** Number of Boolean functions of 2 variables.

### Medium

**P11.** Simplify F = AB + AB'C + A'C'D using K-map.

**P12.** Minimal SOP of F = Σm(0,1,2,3,5,7,8,10,12,14).

**P13.** Implement A·B + C using NAND only.

**P14.** Show A + A'B = A + B.

**P15.** Implement OR using only NOR gates.

**P16.** Find prime implicants of Σm(1,3,5,7,8,9,11,15) (4-var).

**P17.** Find EPIs of F = Σm(0,2,5,7,8,10,13,15).

**P18.** Convert F = AB' + B'C to POS.

**P19.** Compute (A+B)(A'+B)(A+B').

**P20.** Show: AB + A'C + BC = AB + A'C (consensus).

### Hard

**P21.** Minimize F = Σm(0,1,2,5,7,8,9,10,11,15) using K-map.

**P22.** Implement A ⊕ B ⊕ C using minimum NAND gates.

**P23.** Simplify F = (A+B)(B+C)(C+A) into SOP.

**P24.** A function of 4 variables has F = 1 only when exactly 2 inputs are 1. Express in canonical SOP (min terms 0011, 0101, 0110, 1001, 1010, 1100 → 3,5,6,9,10,12).

**P25.** Find # essential prime implicants of F = Σm(0,4,8,12,1,5,9,13).

**P26.** Implement F = AB + CD using only 2-input NAND gates; count gates.

**P27.** Find minimum POS for F = ΠM(1,3,4,6).

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.1 | direct |
| P2 | NAND = NOT AND | direct |
| P3 | A' + B' | DM |
| P4 | A | absorption |
| P5 | A | identity |
| P6 | 1 | complement |
| P7 | C' | C=0 minterms |
| P8 | A | absorption |
| P9 | AB' + A'B | XOR |
| P10 | 16 | 2^(2²) |
| P11 | A + C'D | K-map; reduce |
| P12 | several PIs; cover via K-map | K-map |
| P13 | NAND(NAND(A,B), C̄) chained appropriately | universality |
| P14 | LHS truth table = RHS | direct |
| P15 | A NOR B then NOT, or (A NOR B) NOR (A NOR B) | NOR univ |
| P16 | C (1,3,5,7); A (8,9,...); plus combine | K-map |
| P17 | B'D' (0,2,8,10), BD (5,7,13,15) — both EPIs | EPI count = 2 |
| P18 | (A+B')(B'+C) — use truth table or factoring | direct |
| P19 | B(A+A')(...) = expand and simplify | direct |
| P20 | use distrib + complement | identity |
| P21 | Result: B'D' + A'B'C + AC'D' + AB'D + B' (etc.) — verify via K-map | K-map |
| P22 | typically 4 NANDs for XOR; chain two for 3-input → ~8 NANDs | direct |
| P23 | AB + BC + CA | majority |
| P24 | 6 minterms; SOP straightforward | direct |
| P25 | EPI = D' (covers 0,4,8,12) and D (covers 1,5,9,13) → 2 EPIs | K-map |
| P26 | 5 NAND gates | direct |
| P27 | (B+D')(B'+D) — apply consensus | POS form |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting A + A'B = A + B (not A) | Truth-table verify. |
| 2 | Counting groups of size 3, 5, 6 in K-map | Only powers of 2. |
| 3 | Not wrapping K-map at edges | All 4 corners adjacent; left ↔ right. |
| 4 | Ignoring don't cares to enlarge groups | Use them whenever advantageous. |
| 5 | Missing EPIs in coverage | Cover EPIs first. |
| 6 | Confusing SOP and POS | SOP from minterms (1's); POS from maxterms (0's). |
| 7 | DM applied to single literal: (A)' ≠ ... | DM applies to compound terms only. |
| 8 | Mismatching bit positions in K-map | Use Gray code labels. |
| 9 | Treating XOR as OR | They're different. |
| 10 | Forgetting that NAND/NOR each are individually universal | Single gate type suffices. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Minimize Boolean expression" | K-map for ≤ 4 vars; Quine-McCluskey for more. |
| "F = Σm(...)" | Plot 1's; group; minimal SOP. |
| "F = ΠM(...)" | Plot 0's (or take complement of Σm); minimal POS. |
| "Number of EPIs" | K-map + EPI identification. |
| "Implement using NAND only" | Use NAND-NAND form (SOP via DM). |
| "Implement using NOR only" | Use NOR-NOR form (POS via DM). |
| "Number of distinct Boolean functions" | 2^(2ⁿ). |
| "Don't cares" | Use as 1's in K-map to enlarge groups. |
| "Complement of expression" | Apply De Morgan. |
| "XOR / parity / odd / even of inputs" | XOR chain. |

---

## 9. Quick Revision

```
LAWS
 A·1=A, A+0=A
 A·0=0, A+1=1
 A·A=A, A+A=A
 A·A'=0, A+A'=1
 (A')' = A
 (AB)' = A'+B', (A+B)' = A'B' (DM)
 A+AB = A; A+A'B = A+B
 A(A+B) = A
 A+BC = (A+B)(A+C)
 consensus: AB+A'C+BC = AB+A'C

SOP / POS
 minterm m_i: where F=1; F = Σm
 maxterm M_i: where F=0; F = ΠM
 m_i and M_i are complements

K-MAP
 Gray-coded adjacency
 groups: 1,2,4,8,16
 wrap edges
 don't cares help

IMPLICANTS
 PI: maximal group
 EPI: covers minterm uniquely
 minimal: all EPIs + minimal extras

UNIVERSAL: NAND, NOR alone

XOR
 A⊕B = AB'+A'B
 A⊕0=A, A⊕1=A', A⊕A=0, A⊕A'=1
 odd parity = chain XOR

# fns of n vars = 2^(2ⁿ)
```
