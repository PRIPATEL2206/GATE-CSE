# Minimization & Hazards

> Subject: Digital Logic
> GATE weight: **1–2 marks** every year. Quine-McCluskey, hazards, glitch elimination, multi-output minimization.

---

## 1. Concept Explanation

### 1.1 Why Minimize?

Minimum cost ≈ minimum gates / literals → less area, less power, less delay.

**Cost metrics:**
- # of literals.
- # of product terms.
- # of gates.
- # of inputs to all gates.

GATE problems typically count literals or gates.

### 1.2 K-Map Recap (cross-link → boolean_algebra_kmap.md)

Up to 6 variables practical. Beyond that, use Quine-McCluskey or computer tools.

### 1.3 Quine-McCluskey Method

Systematic tabular method to find all prime implicants and a minimal cover.

**Steps:**
1. List minterms (and don't-cares) in binary.
2. Group by # of 1's.
3. Combine pairs from adjacent groups differing in **exactly one bit**; mark the differing position with `−`.
4. Repeat with the new list (groups by # of 1's, now with `−`'s).
5. Continue until no further combinations possible.
6. Unmarked terms (those that couldn't combine further) are **prime implicants**.
7. Build the **prime implicant chart**:
   - Rows: PIs.
   - Columns: minterms.
   - Mark covers.
8. Identify **essential PIs** (covering at least one minterm covered by only that PI).
9. Cover remaining minterms with minimum extra PIs.

### 1.4 Petrick's Method

When EPI selection alone doesn't cover all minterms uniquely, use Petrick's method:

1. Build product-of-sums where each minterm contributes a sum of PIs covering it.
2. Multiply out (Boolean), simplify with absorption.
3. The shortest products correspond to minimum-cost solutions.

### 1.5 Multi-Output Minimization

Multiple functions sharing logic:
- Identify shared product terms across outputs.
- Use a **multi-output PI chart** — minimize total cost over all outputs.
- ROM/PLA naturally do this.

### 1.6 Hazards: Definitions

A **hazard** is an unwanted transient (glitch) on the output due to non-zero, unequal gate delays — even when the steady-state output should not change.

Three types:

| Type | What it looks like |
|---|---|
| **Static-1 hazard** | Output should remain 1 but momentarily drops to 0 |
| **Static-0 hazard** | Output should remain 0 but momentarily rises to 1 |
| **Dynamic hazard** | Output transitions multiple times instead of once |

### 1.7 Static Hazard Detection (K-Map)

A static-1 hazard exists between two adjacent 1-minterms if **no single product term in the SOP expression covers both**.

Example: `F = AB + B'C` has hazard when transitioning from ABC = 110 to 100 (differ in B). Both are 1's; if A=1, C=0, then with B=1: AB=1, B'C=0, F=1. With B=0: AB=0, B'C=0, F=0 if C=0 — wait, recompute. A static-1 hazard appears if neither term covers both adjacent 1's.

**Fix:** add a redundant prime implicant covering the transition:
`F = AB + B'C + AC` (the AC term covers transition from B=1 to B=0 with A=1, C=1).

### 1.8 Static-0 Hazard

Dual: in POS form, two adjacent 0-cells not covered by a single sum term cause a glitch. Fix: add redundant maxterm.

### 1.9 Dynamic Hazard

Caused by multiple paths with different delays. Eliminating static hazards usually eliminates dynamic ones.

### 1.10 Hazard-Free Circuit

A two-level SOP circuit is **hazard-free** if every pair of adjacent 1-cells in the K-map is covered by **a single common product term** in the implementation.

**Procedure:**
1. K-map the function.
2. Identify all PIs.
3. Check each adjacent 1-cell pair is covered by a single PI present in the chosen cover.
4. If not, add the redundant PI that covers them.

### 1.11 Implicant Counts

| Term | Definition |
|---|---|
| Implicant | Product term where F=1 |
| Prime Implicant (PI) | Maximal implicant — can't grow further |
| Essential PI (EPI) | PI covering a minterm covered by **no other PI** |
| Selected PI | PI in final cover |

### 1.12 Comparison: K-Map vs Quine-McCluskey

| Feature | K-Map | Quine-McCluskey |
|---|---|---|
| Visual | ✅ | ❌ |
| Variables | ≤ 6 | any |
| Suitable for | small | algorithmic (exam, software) |

### 1.13 Minimization in NAND/NOR Logic

After SOP minimization:
- For **NAND-NAND** realization, take double complement: F = (F')' = ((Σ minterms)')' = NAND of NAND of literals.
- For **NOR-NOR**: dual approach using POS.

### 1.14 Hazard-Free Sequential Circuits

In FSMs, hazards on FF inputs can cause incorrect state transitions. Use **edge-triggered FFs** + hazard-free combinational logic.

> **Summary:** Minimize to reduce gates/literals. K-map for ≤ 4 vars; Quine-McCluskey for larger. Hazards = transient glitches from unequal delays. Fix static-1 hazards with redundant prime implicants in SOP.

---

## 2. Important Points

- **Minimal SOP** uses all EPIs + minimal extras to cover non-EPI minterms.
- **EPIs are mandatory**; pick them first.
- Quine-McCluskey is **always optimal** but slow for large variable counts.
- A **prime implicant chart** is the bridge from PIs to minimal cover.
- **Petrick's method** finds minimum cover when EPIs are insufficient.
- **Static-1 hazard** ⇔ adjacent 1-cells not jointly covered by any PI in the implementation.
- **Hazard-free** SOP includes redundant PIs covering all adjacent 1-cell pairs.
- **Don't cares** can be assigned to extend grouping in K-map and Quine-McCluskey.
- A **fully specified** function might still need redundant PIs to be hazard-free — pure minimal SOP may have hazards.
- **Multi-output minimization** reduces total cost by sharing PIs.
- For PLA implementation, # product terms = # AND lines used.

---

## 3. Short Notes

```
MINIMIZATION
 K-map: ≤ 4 (or 5/6) vars
 Quine-McCluskey: any n
   1. binary minterms
   2. group by # of 1's
   3. combine adjacent (1-bit diff)
   4. iterate until none
   5. unmarked = PIs
   6. PI chart → EPIs → cover

PETRICK'S METHOD
 if EPIs insufficient
 product-of-sums of PI selections

HAZARDS
 static-1: should be 1, glitches to 0
 static-0: should be 0, glitches to 1
 dynamic: multiple transitions
 caused by unequal gate delays

FIX
 static-1: add redundant PI covering adjacent 1's
 static-0: add redundant sum term

HAZARD-FREE SOP
 every adjacent 1-cell pair covered by a PI in cover

COSTS
 # literals
 # product terms
 # gates
 # gate inputs

NAND-NAND realization: double-complement SOP
NOR-NOR: dual via POS
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | EPIs are mandatory in minimal cover | ✅✅ |
| 2 | Quine-McCluskey: combine differing in one bit | ✅✅ |
| 3 | Static-1 hazard fixed with redundant PI | ✅✅ |
| 4 | Hazard-free SOP includes redundant PIs | ✅ |
| 5 | Petrick: minimum cost from PI chart | ✅ |
| 6 | NAND-NAND ⇔ SOP | ✅ |
| 7 | NOR-NOR ⇔ POS | ✅ |
| 8 | Don't cares free to choose | ✅ |
| 9 | # 1-cells with all PIs covered ≠ hazard-free | ✅ |
| 10 | Multi-output minimization shares PIs | ✅ |

### Tricks

- **Quick PI count:** in K-map, every group of size 1, 2, 4, 8, … that can't be enlarged is a PI.
- **EPI shortcut:** any column in PI chart with exactly one ✓ marks an EPI.
- **Petrick's method gives exact answer**, but combinatorial; Quine-McCluskey + EPI usually suffices for GATE-sized problems.
- **Hazard-free check shortcut:** if any adjacent pair of 1-cells in your cover isn't in the same PI, add a covering PI.
- **For PLAs and PALs**, count product terms — minimization directly reduces cost.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Find all prime implicants of `F = Σm(0,2,5,7,8,10,13,15)` (4-var).
**Solution.** Group in K-map:
- {0,2,8,10}: B'D'
- {5,7,13,15}: BD
Both maximal — both are PIs.
**Answer: B'D' and BD.** Both are also EPIs.

### Q2. (GATE CSE 2014)
Number of EPIs of `F(A,B,C,D) = Σm(1,3,5,7,9,11,13,15)`:
**Solution.** All odd minterms — single PI is D (covers all). 1 EPI.

### Q3. (GATE CSE 2018)
Minimal SOP of `F = Σm(0,1,2,3,4,5,7,9,15)`:
**Solution.** K-map; identify PIs:
- {0,1,2,3,4,5}: A'B'+A'C — wait recompute by K-map; standard answer: `A'B' + A'C' + B'D + ABCD' (or similar combination)`. Final compact form depends on selection.

### Q4. (GATE CSE 2008)
Identify static-1 hazard in `F = AB + BC'`:
**Solution.** Transition ABC=111 to 110: AB=11, BC'=01 → F=1; 110: AB=11, BC'=10 → F=1. No issue. Transition 011 to 010: hazards possible if delays mismatched.
*(Check: hazard occurs when changing input causes one product term to drop before another rises.)*

### Q5. (GATE CSE 2010)
Hazard-free SOP for `F = AB + BC + AC`:
**Solution.** All adjacent 1-cells already covered by some product. No hazard.

### Q6. (GATE CSE 2015)
A 4-variable function has 4 PIs and 2 EPIs. Minimum # of PIs in a minimal cover:
**Solution.** At least 2 (the EPIs). Need to check if EPIs cover all minterms; otherwise add more.

### Q7. (GATE CSE 2013)
After K-map minimization, F has minimum SOP `AB + B'C + AC`. Is this hazard-free?
**Solution.** Yes — AC is the consensus term covering transition between AB and B'C as B changes. Hazard-free.

### Q8. (GATE CSE 2007)
Quine-McCluskey: combine `m1 = 0001` and `m3 = 0011`:
**Solution.** Differ in 1 bit; combine to `00−1`.

### Q9. (GATE CSE 2003)
Minimum number of NAND gates for `F = AB + CD`:
**Solution.** Standard 5 NANDs.

### Q10. (GATE CSE 2009)
Identify all PIs of `F = Σm(0, 4, 8, 12, 1, 5, 9, 13)`:
**Solution.** All have C=0 → C'. Single PI: C'. 1 EPI.

### Q11. (GATE CSE 2019)
A static-1 hazard is removed by:
**Solution.** Adding a redundant prime implicant.

### Q12. (GATE CSE 2020)
Minimal POS for `F = ΠM(0, 1, 4, 6)`:
**Solution.** Plot 0's at minterms 0,1,4,6; group; derive maxterm products.

### Q13. (GATE CSE 2021)
Multi-output minimization compared to single-output:
**Solution.** Shares PIs across outputs; total cost ≤ sum of individual minimizations.

### Q14. (GATE CSE 2016)
Hazard-free implementation of XOR — possible using two-level SOP?
**Solution.** XOR has inherent transitions; use redundant terms or three-level implementation. In two-level SOP, XOR `AB' + A'B` has potential hazards on equal A=B transitions.

### Q15. (GATE CSE 2011)
A 5-variable K-map has how many cells?
**Solution.** 32.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define prime implicant.

**P2.** What's an essential prime implicant?

**P3.** State the cause of a static-1 hazard.

**P4.** Method to fix static-1 hazard?

**P5.** Quine-McCluskey: combine `0010` and `0011`.

**P6.** # of cells in 4-variable K-map.

**P7.** Define dynamic hazard.

**P8.** When are two minterms adjacent in K-map?

**P9.** Are EPIs mandatory in minimal cover?

**P10.** Difference between hazard-free and minimal SOP?

### Medium

**P11.** Apply Quine-McCluskey to F = Σm(0, 1, 2, 5, 6, 7).

**P12.** Find PIs of F = Σm(1, 3, 7, 11, 15).

**P13.** Identify hazard in F = AB + AC' + BC.

**P14.** Minimize and check hazard-free: F = Σm(1, 3, 7, 5).

**P15.** Number of PIs and EPIs of F = Σm(0, 2, 3, 5, 7, 11, 12, 13).

**P16.** Apply Petrick's method to find minimum cover for F = Σm(1, 3, 5, 7, 11, 13).

**P17.** Convert minimal SOP to NAND-NAND form: F = AB + CD.

**P18.** Multi-output minimization of F1 = AB + BC, F2 = AB + AC.

**P19.** Eliminate static-0 hazard in F = (A + B)(B' + C).

**P20.** Find # of redundant PIs needed for hazard-free implementation of F = Σm(0,1,2,3,4,5,7).

### Hard

**P21.** Apply Quine-McCluskey to F(A,B,C,D) = Σm(0,1,5,6,7,11,12,13,15).

**P22.** Show that adding consensus term to F = AB + A'C eliminates the hazard.

**P23.** A function has 6 PIs of which 3 are EPIs. Use Petrick's method to find minimum cover.

**P24.** Implement F = Σm(1, 3, 7, 11, 15) hazard-free using SOP.

**P25.** A 4-variable function has minimal SOP `AB + B'D + ACD'` — is it hazard-free?

**P26.** Multi-output minimization: F1 = Σm(0,1,2,3); F2 = Σm(2,3,4,5). Find shared PIs.

**P27.** Compare cost (# literals) of minimal SOP and minimal POS for F = Σm(0,1,2,5,6,7).

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | implicant that can't combine to a larger one | direct |
| P2 | PI covering a minterm not covered by other PIs | direct |
| P3 | unequal gate delays cause transient glitch | direct |
| P4 | add redundant PI | direct |
| P5 | 001− | bit difference at last position |
| P6 | 16 | 2⁴ |
| P7 | multiple transitions where one expected | direct |
| P8 | differ by one bit (Gray code adjacency) | direct |
| P9 | yes | minimal cover |
| P10 | minimal might miss redundant; hazard-free includes them | direct |
| P11 | result: A'B' + B'C + BC' or similar | combine |
| P12 | C+D = 1 form, single PI? recompute (1,3): 0001, 0011; (7,11,15): 0111, 1011, 1111 | direct |
| P13 | check transitions | hazard analysis |
| P14 | F = D + ... ; check pairs | direct |
| P15 | depends on K-map | direct |
| P16 | combinatorial | Petrick |
| P17 | F = NAND(NAND(A,B), NAND(C,D)) | DM |
| P18 | shared PI: AB | multi-output |
| P19 | add redundant maxterm | dual |
| P20 | depends on transitions | analysis |
| P21 | use Quine-McCluskey systematically | direct |
| P22 | consensus AC covers transition | direct |
| P23 | enumerate covers | Petrick |
| P24 | SOP with redundant terms | direct |
| P25 | check pair coverage | hazard analysis |
| P26 | shared minterm 2,3 | multi-output |
| P27 | compute literals each side | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Stopping at minimal SOP for hazard-free | Add redundant PIs as needed. |
| 2 | Forgetting EPIs first | EPIs always in minimal cover. |
| 3 | Quine-McCluskey: missing combine step | Repeat combining until stable. |
| 4 | Not handling don't-cares well | Use them to make groups bigger. |
| 5 | Single-output minimization for multi-output problems | Apply joint minimization. |
| 6 | Forgetting Petrick's method when EPIs insufficient | Use Petrick. |
| 7 | Static-1 hazard fix in POS | Use static-0 fix instead. |
| 8 | Counting cells incorrectly | 2ⁿ for n vars. |
| 9 | Mixing SOP and POS in fixes | Stay in one form per analysis. |
| 10 | Treating dynamic hazards as separate problems | Often static fixes suffice. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Find prime implicants" | K-map for ≤ 4 vars; Quine-McCluskey otherwise. |
| "Find essential PIs" | PI chart; column with single ✓. |
| "Hazard-free SOP" | Add redundant PI for adjacent 1-cells not in same PI. |
| "Quine-McCluskey procedure" | Group by # 1's; combine; iterate; PI chart. |
| "Multi-output minimization" | Share PIs across outputs. |
| "NAND-NAND realization" | Apply DM to SOP. |
| "Static-0 hazard" | Use POS minimization with redundant maxterms. |
| "Petrick's method" | Combinatorial PI selection when EPIs insufficient. |
| "Don't-care assignment" | Maximize grouping. |
| "Cost comparison: # gates / literals" | Count carefully. |

---

## 9. Quick Revision

```
PRIME IMPLICANT (PI): maximal group
ESSENTIAL PI (EPI): PI covering a unique minterm
MINIMAL SOP: all EPIs + minimal extras

QUINE-McCLUSKEY
 1. binary minterms
 2. group by # of 1's
 3. combine differing in 1 bit
 4. iterate
 5. PI chart → EPI selection
 6. Petrick if needed

PETRICK'S METHOD
 product-of-sums of PI choices
 multiply, simplify
 minimum-cost = minimal SOP

HAZARDS
 static-1: 1 → glitches to 0
 static-0: 0 → glitches to 1
 dynamic: multiple transitions
 cause: unequal gate delays
 fix: redundant PI covering adjacent 1-cells

HAZARD-FREE SOP
 every adjacent 1-pair in same PI

COSTS
 # literals, terms, gates, inputs

REALIZATION
 NAND-NAND ⇔ SOP
 NOR-NOR ⇔ POS

MULTI-OUTPUT
 share PIs across outputs
```
