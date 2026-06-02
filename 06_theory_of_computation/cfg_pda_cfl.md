# CFG, PDA & CFL

> Subject: Theory of Computation
> GATE weight: **2–4 marks** every year. CFG → CNF/GNF, PDA, ambiguity, parse trees, CFL closure.

---

## 1. Concept Explanation

### 1.1 Context-Free Grammar (CFG)

`G = (V, T, P, S)`:
- V: finite set of **non-terminals** (variables).
- T: finite set of **terminals** (alphabet).
- P: finite set of **productions** A → α, where A ∈ V, α ∈ (V ∪ T)\*.
- S ∈ V: start symbol.

Generates **context-free language (CFL)**.

### 1.2 Derivations

`A → α` means α can replace A.
- **Leftmost derivation:** always rewrite the leftmost non-terminal.
- **Rightmost derivation:** always rewrite the rightmost.
- **Sentential form:** any string of (V ∪ T)\* derivable from S.
- **Sentence:** a sentential form with no non-terminals.

### 1.3 Parse Tree

Tree-form derivation: root = S, internal nodes = non-terminals, leaves = terminals (or ε), children given by production used.

**Yield:** concatenation of leaves left-to-right.

### 1.4 Ambiguity

A CFG is **ambiguous** if some string has more than one parse tree (or equivalently, more than one leftmost derivation).

A **CFL is inherently ambiguous** if every CFG for it is ambiguous.

**Examples of inherently ambiguous CFL:** {aⁿbⁿcᵐdᵐ : n,m ≥ 1} ∪ {aⁿbᵐcᵐdⁿ : n,m ≥ 1}.

### 1.5 Useful CFG Forms

#### Chomsky Normal Form (CNF)

All productions of form:
- A → BC (two non-terminals)
- A → a (single terminal)
- S → ε allowed only if ε ∈ L

Used in **CYK parsing** algorithm.

#### Greibach Normal Form (GNF)

All productions of form:
- A → aα (terminal followed by string of non-terminals)

Used to simulate CFG in PDA.

### 1.6 CNF Conversion Steps

1. Eliminate ε-productions (except possibly S → ε).
2. Eliminate unit productions A → B.
3. Eliminate useless symbols.
4. Convert to A → BC or A → a:
   - Replace A → α (|α| > 2): introduce new non-terminals.
   - Replace A → β where β has terminals among non-terminals: introduce new non-terminal Tₐ → a.

### 1.7 Pushdown Automaton (PDA)

`P = (Q, Σ, Γ, δ, q₀, Z₀, F)`:
- Q: states.
- Σ: input alphabet.
- Γ: stack alphabet.
- δ: Q × (Σ ∪ {ε}) × Γ → finite subsets of Q × Γ\* (NPDA) or single (DPDA).
- q₀: start state.
- Z₀: initial stack symbol.
- F: final states.

**Acceptance:**
- By final state: input consumed, in accepting state.
- By empty stack: input consumed, stack empty.

(Both equivalent.)

### 1.8 PDA vs CFG

- **CFG ↔ NPDA** (non-deterministic): equivalent in power.
- **DPDA** (deterministic): strictly weaker — accepts only **deterministic CFL (DCFL)**.

### 1.9 Deterministic CFL (DCFL)

Languages accepted by DPDA. Examples:
- {aⁿbⁿ}
- {wcwᴿ : w ∈ Σ\*}

DCFL is closed under complement (unlike full CFL).

### 1.10 Closure Properties of CFL

CFL **closed under**:
- Union, concatenation, Kleene star.
- Reverse, homomorphism, inverse homomorphism.
- Substitution.
- Intersection **with regular language**.

CFL **NOT closed under**:
- Intersection (general).
- Complement.
- Difference.

### 1.11 Pumping Lemma for CFL

If L is a CFL, ∃ p such that every w ∈ L with |w| ≥ p can be written w = uvxyz with:
- |vxy| ≤ p
- |vy| ≥ 1
- uvⁱxyⁱz ∈ L for all i ≥ 0.

Used to prove non-CFL.

### 1.12 Common Non-CFL Languages

- {aⁿbⁿcⁿ : n ≥ 0}
- {ww : w ∈ Σ\*}
- {aⁱbʲcᵏ : i = j = k}
- {a^p : p prime}

### 1.13 Decision Problems for CFL

| Problem | Decidable? |
|---|---|
| Membership (CYK) | ✅ (O(n³)) |
| Emptiness | ✅ |
| Finiteness | ✅ |
| Equivalence (general CFG) | ❌ (undecidable!) |
| Equivalence of DCFL | ✅ |
| Universality (general CFG) | ❌ |
| Ambiguity | ❌ |
| Inherent ambiguity | ❌ |
| Containment | ❌ |
| Disjointness | ❌ |

### 1.14 CYK Algorithm

For CFG in CNF, decides membership in O(n³).

`dp[i][j]` = set of non-terminals deriving substring w[i..j].

For each substring length, fill table. Check S ∈ dp[0][n−1].

### 1.15 Eliminating Useless Symbols

A symbol X is **useful** if some derivation S ⇒\* αXβ ⇒\* w (terminal string w).

**Useless** = not useful (cannot reach terminal, or unreachable from S).

Two-pass algorithm: find generating symbols, then reachable.

### 1.16 Unit & ε Production Elimination

**ε-production:** A → ε. Eliminate by adding all combinations omitting ε producers (except possibly S).

**Unit production:** A → B. Eliminate by replacing with B's productions for each unit pair.

### 1.17 PDA Configurations

`(q, w, γ)`: state, remaining input, stack contents.

**Move:** (q, aw, Xγ) ⊢ (q', w, βγ) using δ(q, a, X) ∋ (q', β).

**Acceptance via final state:** (q₀, w, Z₀) ⊢\* (q_f, ε, γ) for q_f ∈ F.
**Acceptance via empty stack:** (q₀, w, Z₀) ⊢\* (q, ε, ε).

### 1.18 Common CFGs

| Language | Example CFG |
|---|---|
| L = {aⁿbⁿ} | S → aSb \| ε |
| L = palindromes | S → aSa \| bSb \| a \| b \| ε |
| L = strings with equal a's, b's | S → aSb \| bSa \| SS \| ε |
| L = balanced parens | S → (S) \| SS \| ε |
| L = arithmetic expressions | E → E+E \| E*E \| (E) \| id |

### 1.19 Closure Comparison (Regular vs CFL)

| Op | Regular | CFL |
|---|---|---|
| ∪ | ✅ | ✅ |
| ∩ | ✅ | ❌ |
| Complement | ✅ | ❌ |
| ∩ regular | ✅ | ✅ |
| Concat | ✅ | ✅ |
| Star | ✅ | ✅ |
| Reverse | ✅ | ✅ |
| Hom | ✅ | ✅ |
| Inv hom | ✅ | ✅ |

### 1.20 Membership Hierarchy

```
Regular ⊊ DCFL ⊊ CFL ⊊ CSL ⊊ Recursive ⊊ RE
```

> **Summary:** CFG/PDA equivalence; CNF for CYK; ambiguity; closure (CFL not under intersection or complement); pumping lemma for CFL; decision problems mostly undecidable for general CFG.

---

## 2. Important Points

- **CFG = NPDA** in power.
- **DPDA ⊊ NPDA** — DPDA accepts DCFL only.
- **CNF:** A → BC or A → a.
- **GNF:** A → aα (used for PDA simulation).
- **Pumping for CFL:** |vxy| ≤ p, |vy| ≥ 1, uvⁱxyⁱz ∈ L.
- **CFL not closed under intersection**, but **CFL ∩ regular = CFL**.
- **DCFL closed under complement**; full CFL is not.
- **Membership** (CYK) O(n³); equivalence undecidable for general CFG.
- Many basic problems undecidable (ambiguity, equivalence, universality).
- **CYK** requires CNF.
- **Inherent ambiguity** = no CFG for L is unambiguous.
- {aⁿbⁿcⁿ} is **not CFL** (counter-example for closure).
- Useless symbols can be removed without changing language.
- **{wwᴿ}** is CFL; **{ww}** is not.
- **Palindromes** are CFL.
- **Equal a/b/c counts** is not CFL.

---

## 3. Short Notes

```
CFG: G = (V, T, P, S)
 V non-terminals, T terminals, P productions A → α

DERIVATION
 leftmost / rightmost
 sentential form / sentence

PARSE TREE
 yield = concatenation of leaves

AMBIGUOUS CFG: > 1 parse tree
INHERENTLY AMBIGUOUS CFL: every CFG ambiguous

CNF: A → BC or A → a (S → ε allowed)
GNF: A → aα

CONVERSION TO CNF
 1. eliminate ε
 2. eliminate unit
 3. eliminate useless
 4. convert to CNF form

PDA = (Q, Σ, Γ, δ, q₀, Z₀, F)
 NPDA = CFG in power
 DPDA ⊊ NPDA → DCFL
 acceptance: final state OR empty stack

DCFL closed under complement; CFL not

CFL CLOSURE
 ✅ ∪, concat, *, reverse, hom, inv-hom, ∩ regular, substitution
 ❌ ∩, complement, difference

PUMPING FOR CFL
 w = uvxyz, |vxy| ≤ p, |vy| ≥ 1, uvⁱxyⁱz ∈ L

NON-CFL
 aⁿbⁿcⁿ, ww, equal a/b/c, primes

DECIDABILITY (CFG)
 ✅ membership (CYK O(n³)), emptiness, finiteness
 ❌ equivalence, ambiguity, universality, containment

CYK
 needs CNF; O(n³)

USELESS / UNIT / ε-PROD
 elimination via standard algorithms

PDA CONFIG: (state, input, stack)
 ⊢ for moves

HIERARCHY
 regular ⊊ DCFL ⊊ CFL ⊊ CSL ⊊ recursive ⊊ RE
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | CFG ↔ NPDA equivalence | ✅✅✅ |
| 2 | DPDA ⊊ NPDA (DCFL ⊊ CFL) | ✅✅ |
| 3 | CFL closed under ∪, concat, *, reverse, hom | ✅✅ |
| 4 | CFL not closed under ∩ or complement | ✅✅ |
| 5 | CFL ∩ regular = CFL | ✅✅ |
| 6 | DCFL closed under complement | ✅ |
| 7 | CYK O(n³) | ✅✅ |
| 8 | aⁿbⁿcⁿ not CFL | ✅✅ |
| 9 | ww not CFL | ✅✅ |
| 10 | wwᴿ is CFL | ✅ |
| 11 | Equivalence of CFG: undecidable | ✅ |
| 12 | Ambiguity: undecidable | ✅ |
| 13 | CNF: A → BC or A → a | ✅ |
| 14 | GNF: A → aα | ✅ |
| 15 | CFL pumping: 5 parts (uvxyz) | ✅ |

### Tricks

- **For non-CFL proof:** pumping with uvxyz; cases on which of v, y has terminals.
- **CYK trick:** must convert grammar to CNF first.
- **CFL closure under ∩ regular:** product of PDA × DFA.
- **For CFG equivalence:** undecidable in general.
- **Quick check non-CFL:** count three or more interrelated quantities like a^n b^n c^n.
- **Inherent ambiguity:** rare; some specific languages.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Is {aⁿbⁿcⁿ} CFL?
**Solution.** No.

### Q2. (GATE CSE 2014)
CFG and which automaton equivalent?
**Solution.** NPDA.

### Q3. (GATE CSE 2018)
DPDA strictly weaker than NPDA?
**Solution.** Yes — DCFL ⊊ CFL.

### Q4. (GATE CSE 2008)
CFL closed under intersection?
**Solution.** No.

### Q5. (GATE CSE 2010)
CFL ∩ regular language:
**Solution.** CFL.

### Q6. (GATE CSE 2015)
CYK algorithm time:
**Solution.** O(n³) (n = string length).

### Q7. (GATE CSE 2013)
Equivalence of two CFGs:
**Solution.** Undecidable.

### Q8. (GATE CSE 2007)
Ambiguity of CFG:
**Solution.** Undecidable.

### Q9. (GATE CSE 2003)
Membership in CFL:
**Solution.** Decidable (CYK).

### Q10. (GATE CSE 2009)
{aⁱbʲcᵏ : i = j or j = k} CFL?
**Solution.** Yes (union of two CFLs).

### Q11. (GATE CSE 2019)
{ww : w ∈ Σ\*} CFL?
**Solution.** No.

### Q12. (GATE CSE 2020)
Number of strings of length 4 in regular L = (a+b)*ab:
**Solution.** Strings ending in "ab" of length 4: 4 strings.

### Q13. (GATE CSE 2021)
DCFL closed under complement?
**Solution.** Yes.

### Q14. (GATE CSE 2016)
CNF of CFG:
**Solution.** A → BC or A → a (with possible S → ε).

### Q15. (GATE CSE 2011)
Greibach Normal Form:
**Solution.** A → aα.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define CFG.

**P2.** What is a parse tree?

**P3.** Define ambiguous CFG.

**P4.** What's CNF form?

**P5.** What's GNF form?

**P6.** PDA stack alphabet?

**P7.** Is L = {aⁿbⁿ} CFL?

**P8.** Is L = {aⁿbⁿcⁿ} CFL?

**P9.** Is L = {ww : w ∈ Σ\*} CFL?

**P10.** Membership in CFL: which algorithm?

### Medium

**P11.** CFG for {aⁿbⁿ}.

**P12.** CFG for palindromes.

**P13.** CFG for balanced parens.

**P14.** Convert CFG to CNF: S → aSb | ε.

**P15.** Apply pumping lemma to {aⁿbⁿcⁿ}.

**P16.** Build PDA for {aⁿbⁿ}.

**P17.** Show {aⁱbʲ : i ≤ j} is CFL.

**P18.** Show inherent ambiguity example.

**P19.** Decide if {aⁿbⁿ : n > 100} is CFL.

**P20.** CFL ∩ regular = ?

### Hard

**P21.** Prove CFL not closed under intersection.

**P22.** Show DCFL closed under complement.

**P23.** Apply CYK on CNF grammar to test membership.

**P24.** Show equivalence of CFG and PDA.

**P25.** Prove {aⁿbⁿcⁿdⁿ} not CFL using pumping lemma.

**P26.** Use closure to show {ww} not CFL.

**P27.** Show CFL closed under reverse.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.1 | direct |
| P2 | tree of derivation | direct |
| P3 | > 1 parse tree | direct |
| P4 | A → BC or A → a | direct |
| P5 | A → aα | direct |
| P6 | Γ | direct |
| P7 | yes | direct |
| P8 | no | direct |
| P9 | no | direct |
| P10 | CYK | direct |
| P11 | S → aSb \| ε | direct |
| P12 | S → aSa \| bSb \| ε \| a \| b | direct |
| P13 | S → (S) \| SS \| ε | direct |
| P14 | S → AB \| ε; A → a; ... | direct |
| P15 | classic proof | direct |
| P16 | push a's, pop on b | direct |
| P17 | S → aSb \| Sb \| ε | direct |
| P18 | {aⁿbⁿcᵐdᵐ} ∪ {aⁿbᵐcᵐdⁿ} | direct |
| P19 | yes | finite difference |
| P20 | CFL | direct |
| P21 | aⁿbⁿcⁿ = aⁿbⁿc\* ∩ a\*bⁿcⁿ | direct |
| P22 | switch final/non-final in DPDA | direct |
| P23 | trace CYK | direct |
| P24 | construct PDA from CFG (push) | direct |
| P25 | pump v and y; force imbalance | direct |
| P26 | use closure paradox | direct |
| P27 | reverse RHS of productions | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | DPDA = NPDA in power | DPDA strictly weaker. |
| 2 | CFL closed under ∩ | Only ∩ regular. |
| 3 | CFL closed under complement | Not in general; DCFL is. |
| 4 | CYK on non-CNF | Convert first. |
| 5 | Pumping lemma proves CFL | Only proves non-CFL. |
| 6 | CFG equivalence decidable | Undecidable. |
| 7 | Ambiguity decidable | Undecidable. |
| 8 | wwᴿ same as ww | Different (palindrome vs square). |
| 9 | CFL ⊆ regular | Other way around. |
| 10 | Forgetting ε in CNF (only S → ε allowed) | Special case. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Is L a CFL?" | Build CFG/PDA or apply pumping lemma. |
| "Counting unrelated quantities" | Likely not CFL. |
| "wwᴿ" | CFL. |
| "ww" | Not CFL. |
| "Equivalence of CFGs" | Undecidable. |
| "CFL ∩ regular" | CFL. |
| "DCFL complement" | DCFL. |
| "CYK" | O(n³); needs CNF. |
| "Ambiguity decidable" | No. |
| "Pumping CFL" | uvxyz, 5 parts. |

---

## 9. Quick Revision

```
CFG = (V, T, P, S)
NPDA ↔ CFG; DPDA → DCFL ⊊ CFL

CNF: A → BC or A → a
GNF: A → aα

CYK: O(n³), needs CNF

CFL CLOSURE
 ∪, concat, *, reverse, hom, inv-hom: ✅
 ∩, complement: ✗
 ∩ regular: ✅

DCFL closed under complement

PUMPING (CFL)
 w = uvxyz; |vxy| ≤ p; |vy| ≥ 1
 uvⁱxyⁱz ∈ L

NON-CFL: aⁿbⁿcⁿ, ww, equal a/b/c

DECIDABILITY
 ✅ membership, emptiness, finiteness
 ✗ equivalence, ambiguity, universality

HIERARCHY
 regular ⊊ DCFL ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE
```
