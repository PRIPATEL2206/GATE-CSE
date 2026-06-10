# Functional Dependencies & Normalization

> Subject: Databases
> GATE weight: **3–5 marks** every year. FD closure, candidate key derivation, BCNF/3NF/lossless decomposition.

---

## 1. Concept Explanation

### 1.1 Functional Dependency (FD)

`X → Y` means: whenever two tuples agree on X, they agree on Y.

**Example:** `EmpID → Name, Salary` means employee ID determines name and salary.

### 1.2 Trivial vs Non-trivial FD

| Type | Definition |
|---|---|
| **Trivial** | Y ⊆ X (e.g., AB → A) |
| **Non-trivial** | Y ⊄ X |
| **Completely non-trivial** | X ∩ Y = ∅ |

### 1.3 Armstrong's Axioms

Sound and complete inference rules for FDs:

| Axiom | Form |
|---|---|
| **Reflexivity** | If Y ⊆ X, then X → Y |
| **Augmentation** | If X → Y, then XZ → YZ |
| **Transitivity** | If X → Y and Y → Z, then X → Z |

**Derived rules:**
- **Union:** X → Y, X → Z ⇒ X → YZ.
- **Decomposition:** X → YZ ⇒ X → Y, X → Z.
- **Pseudo-transitivity:** X → Y, WY → Z ⇒ WX → Z.

### 1.4 Closure of Attributes (X⁺)

`X⁺` = set of attributes determined by X using FDs.

**Algorithm:**
```
result = X
repeat:
  for each FD A → B:
    if A ⊆ result, add B to result
until no change
```

### 1.5 Candidate Key Derivation

**Candidate key** = minimal set X such that X⁺ = all attributes.

**Steps:**
1. Find attributes appearing only on **LHS** of FDs → must be in every candidate key.
2. Find attributes appearing only on **RHS** → never in candidate key.
3. Compute closure of "must-be" attributes; if it's all attributes, that's the only candidate key.
4. Otherwise, try adding "either side" attributes.

### 1.6 Closure of FD Set (F⁺)

Set of all FDs derivable from F using Armstrong's axioms.

**Equivalence of FD sets:** F ≡ G if F⁺ = G⁺.

### 1.7 Canonical (Minimal) Cover

A minimal set of FDs equivalent to F:
1. RHS has single attribute.
2. No redundant FDs.
3. No redundant attributes on LHS.

**Algorithm:**
1. Decompose RHS to single attribute.
2. Check each FD: can it be removed?
3. For each FD, check each LHS attribute: can it be removed?

### 1.8 Lossless Decomposition

Decomposition R → R₁, R₂ is **lossless** iff:
- (R₁ ∩ R₂) → R₁ **or** (R₁ ∩ R₂) → R₂
- (Common attributes form a key for one of them.)

### 1.9 Dependency Preservation

Decomposition preserves dependencies if every FD in F can be checked locally on one of the subrelations (or implied by FDs there).

### 1.10 Normalization Goals

Reduce:
- **Redundancy** (data repetition).
- **Insertion / update / deletion anomalies.**

### 1.11 Normal Forms (Hierarchy)

```
1NF ⊂ 2NF ⊂ 3NF ⊂ BCNF ⊂ 4NF ⊂ 5NF
```

### 1.12 1NF (First Normal Form)

All attribute values are **atomic** (no multi-valued, no nested relations).

### 1.13 2NF

In 1NF + every **non-prime attribute** is **fully** functionally dependent on every candidate key.

**No partial dependency** of non-prime on part of candidate key.

**Prime attribute:** appears in some candidate key. **Non-prime:** doesn't.

### 1.14 3NF

In 2NF + for every FD X → A:
- X is a super key, **or**
- A is a prime attribute.

**No transitive dependency** of non-prime on key.

### 1.15 BCNF (Boyce-Codd)

For every non-trivial FD X → Y:
- X is a **super key**.

Stronger than 3NF.

### 1.16 BCNF vs 3NF

- **3NF**: dependency-preserving; lossless.
- **BCNF**: lossless but **may not** preserve dependencies.

**BCNF ⇒ 3NF**. Some relations in 3NF aren't in BCNF.

### 1.17 4NF (Multi-valued Dependencies)

For every non-trivial MVD X →→ Y:
- X is a super key.

MVD: independent multi-valued sets.

### 1.18 5NF (PJNF)

Every join dependency is implied by candidate keys.

### 1.19 Normalization Procedure

1. Identify FDs.
2. Compute candidate keys.
3. Check each NF condition.
4. Decompose violating relations.
5. Verify lossless and dependency preservation.

### 1.20 Common Anomalies (in unnormalized data)

| Anomaly | Description |
|---|---|
| **Insertion** | Cannot insert without other data |
| **Deletion** | Lose unrelated info |
| **Update** | Multiple updates needed for consistency |

### 1.21 Decomposition Algorithm

**For BCNF:**
```
Find FD X → Y violating BCNF.
Decompose R into R₁ = X⁺, R₂ = R − (X⁺ − X).
Recursively decompose if needed.
```

**For 3NF (synthesis):** use canonical cover; create one relation per FD; ensure at least one candidate key.

### 1.22 Pitfalls

- **3NF doesn't imply BCNF.**
- **BCNF may break dependency preservation.**
- **Lossless decomposition condition** must be checked.
- **Multi-valued dependencies** lead to 4NF.

> **Summary:** FDs drive normalization. Compute attribute closure, derive candidate keys, identify violations of 2NF/3NF/BCNF, decompose. Lossless + dependency preservation are the two key properties of decomposition.

---

## 2. Important Points

- **Attribute closure** is foundational for FD reasoning.
- **Candidate key:** minimal set with closure = all attributes.
- **Prime attribute:** in some candidate key.
- **2NF:** no partial dependencies.
- **3NF:** no transitive dependencies of non-prime on key.
- **BCNF:** every FD has super key on LHS.
- **BCNF ⊃ 3NF ⊃ 2NF ⊃ 1NF**.
- **Lossless decomposition:** common attribute(s) is super key in one fragment.
- **Dependency preservation:** all FDs checkable locally.
- **3NF always preserves dependencies**; **BCNF may not**.
- **Canonical cover:** minimal equivalent FD set.
- **Armstrong's axioms** derive all FDs.
- **MVD → 4NF**.

---

## 3. Short Notes

```
FD: X → Y
 trivial: Y ⊆ X
 non-trivial: Y ⊄ X

ARMSTRONG'S AXIOMS
 reflexivity, augmentation, transitivity
 derived: union, decomposition, pseudo-transitivity

CLOSURE X⁺
 result = X
 add B if A ⊆ result and A → B
 repeat

CANDIDATE KEY
 minimal X with X⁺ = all attributes
 attributes only on LHS → must include
 only on RHS → never include
 try combinations

CANONICAL COVER (minimal)
 single-attribute RHS
 no redundant FD
 no redundant LHS attr

LOSSLESS DECOMPOSITION
 (R₁ ∩ R₂) → R₁ or → R₂

DEPENDENCY PRESERVATION
 all FDs locally checkable

NORMAL FORMS
 1NF: atomic
 2NF: 1NF + no partial dep on candidate key (for non-prime)
 3NF: 2NF + no transitive dep
   for FD X → A: X is superkey OR A is prime
 BCNF: every FD X → Y: X is super key
 4NF: MVD super key
 5NF: PJNF

PRIME / NON-PRIME ATTRIBUTE
 in some candidate key / not

BCNF ⇒ 3NF
3NF dep-preserving; BCNF may not

ANOMALIES
 insertion / deletion / update

DECOMPOSITION
 BCNF: split on violating FD
 3NF synthesis from canonical cover
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Attribute closure algorithm | ✅✅✅ |
| 2 | Candidate key from closure | ✅✅ |
| 3 | Armstrong's axioms (3 basic) | ✅✅ |
| 4 | Lossless: (R₁∩R₂) → R₁ or R₂ | ✅✅ |
| 5 | 1NF → 2NF → 3NF → BCNF | ✅✅ |
| 6 | 3NF condition | ✅ |
| 7 | BCNF condition: super key on LHS | ✅✅ |
| 8 | 3NF dep-preserving; BCNF may not | ✅ |
| 9 | Canonical cover algorithm | ✅ |
| 10 | MVD → 4NF | ✅ |

### Tricks

- **For closure:** start with X; repeatedly apply FDs until no change.
- **For candidate key:** identify "must-include" attributes from LHS-only.
- **For BCNF check:** for each FD, verify LHS is super key.
- **For 3NF check:** allow if RHS attribute is prime.
- **For lossless join:** ensure common attribute is key in one fragment.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Closure of {AB} given F = {A → C, B → D, AB → E}:
**Solution.** Start AB; add C (from A → C); add D (from B → D); add E (from AB → E). {AB}⁺ = ABCDE.

### Q2. (GATE CSE 2014)
Candidate key of R(A, B, C, D, E) with F = {A → BC, CD → E, B → D, E → A}:
**Solution.** Compute closures of single/double attributes; minimal supersets of F's keys.
{A}⁺ = ABCDE; {E}⁺ = ABCDE; etc. Multiple candidate keys.

### Q3. (GATE CSE 2018)
BCNF condition:
**Solution.** For every non-trivial FD X → Y, X is super key.

### Q4. (GATE CSE 2008)
Lossless decomposition condition:
**Solution.** Common attribute is super key in one fragment.

### Q5. (GATE CSE 2010)
3NF allows:
**Solution.** Transitive dep allowed if RHS is prime.

### Q6. (GATE CSE 2015)
4NF removes:
**Solution.** Multi-valued dependencies.

### Q7. (GATE CSE 2013)
2NF prevents:
**Solution.** Partial dependency of non-prime on candidate key.

### Q8. (GATE CSE 2007)
Armstrong's axioms:
**Solution.** Reflexivity, augmentation, transitivity.

### Q9. (GATE CSE 2003)
Canonical cover:
**Solution.** Minimal FD set equivalent to original.

### Q10. (GATE CSE 2009)
3NF vs BCNF dependency preservation:
**Solution.** 3NF preserves; BCNF may not.

### Q11. (GATE CSE 2019)
Prime attribute:
**Solution.** Member of some candidate key.

### Q12. (GATE CSE 2020)
Anomaly types:
**Solution.** Insertion, deletion, update.

### Q13. (GATE CSE 2021)
Trivial FD example:
**Solution.** AB → A.

### Q14. (GATE CSE 2016)
Compute # candidate keys with given FDs:
**Solution.** Enumerate via closure tests.

### Q15. (GATE CSE 2011)
Decompose to BCNF — example:
**Solution.** Find violating FD; split.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define functional dependency.

**P2.** Trivial FD example.

**P3.** Armstrong's axioms.

**P4.** Closure algorithm.

**P5.** Candidate key definition.

**P6.** Prime attribute.

**P7.** 1NF requirement.

**P8.** 2NF condition.

**P9.** 3NF condition.

**P10.** BCNF condition.

### Medium

**P11.** Compute {A}⁺ for F = {A → B, B → C, C → D}.

**P12.** Find candidate keys of R(A,B,C,D) with F = {AB → C, C → D}.

**P13.** Check 3NF for given relation.

**P14.** Check BCNF.

**P15.** Decompose to BCNF.

**P16.** Find canonical cover.

**P17.** Verify lossless decomposition.

**P18.** Verify dependency preservation.

**P19.** Identify anomaly type.

**P20.** Apply decomposition algorithm.

### Hard

**P21.** Show 3NF doesn't imply BCNF.

**P22.** Decompose to 3NF using synthesis.

**P23.** Find all candidate keys with multiple FDs.

**P24.** Apply 4NF for MVD.

**P25.** Verify lossless via attribute closure.

**P26.** Equivalence of FD sets.

**P27.** Optimal decomposition strategy.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | X → Y constraint | direct |
| P2 | AB → A | direct |
| P3 | reflexivity, augmentation, transitivity | direct |
| P4 | iterate FDs | direct |
| P5 | minimal super key | direct |
| P6 | in some CK | direct |
| P7 | atomic | direct |
| P8 | no partial dep | direct |
| P9 | no transitive dep (non-prime) | direct |
| P10 | every FD has super key on LHS | direct |
| P11 | {A,B,C,D} | direct |
| P12 | AB | direct |
| P13 | check FDs | direct |
| P14 | check FDs | direct |
| P15 | split on violating FD | direct |
| P16 | minimize | direct |
| P17 | common = super key | direct |
| P18 | local checkability | direct |
| P19 | scenario | direct |
| P20 | iterative | direct |
| P21 | counterexample with composite key | direct |
| P22 | synthesis | direct |
| P23 | enumeration | direct |
| P24 | independent multi-valued sets | direct |
| P25 | closure check | direct |
| P26 | F⁺ = G⁺ | direct |
| P27 | BCNF if possible; else 3NF | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | BCNF always preserves dependencies | Sometimes doesn't. |
| 2 | 3NF never has redundancy | May still have. |
| 3 | Forgetting "or A is prime" in 3NF | Important loophole. |
| 4 | Lossless = dependency preserving | Different. |
| 5 | Closure trivial | Apply iteratively. |
| 6 | Mixing canonical cover and minimal cover | Same concept. |
| 7 | All keys are candidate keys | No: PK is one of them. |
| 8 | 4NF easier than BCNF | Stronger; harder to achieve. |
| 9 | Augmentation = transitivity | Different axioms. |
| 10 | MVD = FD | Different concept. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Compute closure" | Iterative algorithm. |
| "Find candidate keys" | Closure of "must-include" + extensions. |
| "Check NF level" | Verify NF condition for each FD. |
| "Decompose to BCNF" | Split on violating FD. |
| "Lossless join check" | Common = super key. |
| "Dependency preservation" | All FDs locally checkable. |
| "Canonical cover" | Minimize FD set. |
| "Prime attribute" | In some candidate key. |
| "Trivial FD" | RHS ⊆ LHS. |
| "MVD" | 4NF analysis. |

---

## 9. Quick Revision

```
FD: X → Y; trivial if Y ⊆ X

ARMSTRONG: reflexivity, augmentation, transitivity

CLOSURE X⁺: iterate FDs until stable

CANDIDATE KEY: minimal X with X⁺ = all

CANONICAL COVER: minimal FD set
 single-attr RHS, no redundant FD, no redundant LHS attr

LOSSLESS DECOMPOSITION
 (R₁ ∩ R₂) → R₁ or R₂

DEPENDENCY PRESERVATION
 all FDs locally checkable

NORMAL FORMS
 1NF: atomic
 2NF: no partial dep on CK (non-prime)
 3NF: for FD X → A, X super key OR A prime
 BCNF: every FD X → Y, X super key
 4NF: MVD super key
 5NF: PJNF

BCNF ⇒ 3NF; 3NF dep-preserving; BCNF may not

ANOMALIES: insertion / deletion / update

DECOMPOSITION
 BCNF: split on violation
 3NF: synthesis from canonical cover
```
