# Pumping Lemma & Closure (Regular Languages)

> Subject: Theory of Computation
> GATE weight: **2–3 marks** every year. Pumping lemma proofs, full closure-property table, regular grammars.

---

## 1. Concept Explanation

### 1.1 Pumping Lemma for Regular Languages

**Statement:** If L is regular, then there exists a constant p (the **pumping length**) such that every string w ∈ L with |w| ≥ p can be split as `w = xyz` with:

1. `|y| ≥ 1` (y is non-empty)
2. `|xy| ≤ p`
3. `xyⁱz ∈ L` for **all** i ≥ 0.

The lemma is a **necessary** condition for regularity (not sufficient).

### 1.2 Using Pumping Lemma to Prove Non-Regularity

**Recipe (proof by contradiction):**
1. Assume L is regular. Let p be the pumping length.
2. Choose a specific w ∈ L with |w| ≥ p.
3. For every decomposition w = xyz with |y| ≥ 1, |xy| ≤ p:
4. Find some i such that xyⁱz ∉ L.
5. Contradiction → L not regular.

**Crucially:** you choose w, the adversary chooses the split.

### 1.3 Classic Non-Regular Languages (proof patterns)

| Language | Choice w | Argument |
|---|---|---|
| L = {aⁿbⁿ} | w = aᵖbᵖ | y is all a's; pumping breaks count |
| L = {aⁿbⁿcⁿ} | w = aᵖbᵖcᵖ | similar |
| L = {ww : w ∈ Σ\*} | w = aᵖbaᵖb | pumping disrupts halving |
| L = {aⁿ : n is prime} | w = aⁿ for prime n > p | pump to non-prime |
| L = {aⁿ²} | w = aᵖ² | gap between consecutive squares > p |
| L = {wwᴿ} | w = aᵖbaᵖ | similar |

### 1.4 Closure Properties of Regular Languages

Regular languages **closed under**:

| Operation | Result regular? |
|---|---|
| Union L₁ ∪ L₂ | ✅ |
| Intersection L₁ ∩ L₂ | ✅ |
| Complement L̄ | ✅ |
| Concatenation L₁L₂ | ✅ |
| Kleene star L\* | ✅ |
| Kleene plus L⁺ | ✅ |
| Reverse Lᴿ | ✅ |
| Difference L₁ − L₂ | ✅ |
| Symmetric difference L₁ ⊕ L₂ | ✅ |
| Homomorphism h(L) | ✅ |
| Inverse homomorphism h⁻¹(L) | ✅ |
| Substitution s(L) | ✅ |
| Quotient L₁/L₂ | ✅ |
| Init: prefix(L) | ✅ |
| Suffix, Substring | ✅ |
| Cycle | ✅ |
| L^k for any constant k | ✅ |

### 1.5 Constructions Behind Closure

**Union:** ε-NFA combining two NFAs.

**Intersection:** product construction (DFA × DFA).

**Complement:** flip final / non-final in DFA (must be DFA, not NFA).

**Concatenation:** ε-link end-of-first to start-of-second.

**Star:** add ε-loop and new accepting start state.

**Reverse:** reverse all transitions, swap start/final.

### 1.6 Closure Under Homomorphism

**Homomorphism h: Σ\* → Δ\*** is a string-to-string mapping that respects concatenation: `h(xy) = h(x)h(y)`.

`h(L) = {h(w) : w ∈ L}` is regular if L is.

### 1.7 Inverse Homomorphism

`h⁻¹(L) = {w ∈ Σ\* : h(w) ∈ L}`. Regular if L regular.

### 1.8 Decision Problems for Regular Languages

| Problem | Decidable? |
|---|---|
| Membership: w ∈ L? | ✅ (run DFA, O(|w|)) |
| Emptiness: L = ∅? | ✅ (graph reachability) |
| Finiteness: |L| < ∞? | ✅ (cycle reachable from start to final) |
| Equivalence: L₁ = L₂? | ✅ (compare min DFAs) |
| Containment: L₁ ⊆ L₂? | ✅ (L₁ ∩ L̄₂ = ∅?) |
| Universality: L = Σ\*? | ✅ |

All decidable in poly time (using min DFA / NFA).

### 1.9 Regular Grammars

**Right-linear grammar:** all productions of form `A → aB` or `A → a` or `A → ε`.

**Left-linear grammar:** `A → Ba` or `A → a` or `A → ε`.

**Both equivalent** to regular languages.

**Linear grammar (mixed):** can be more general — equals **linear context-free**, possibly **not regular**.

### 1.10 Useful Closure Tricks

**Show L is regular** by reducing to known regular operations:
- L = L₁ ∩ L̄₂: regular if L₁, L₂ regular.
- L = max(L₁): regular if L₁ regular.

**Show L is not regular**:
- Pumping lemma.
- Myhill-Nerode classes infinite.
- Closure paradox (e.g., if L regular, some other language would be regular too — contradicting known non-regularity).

### 1.11 Myhill-Nerode for Non-Regularity

If you can show **infinitely many** distinguishing strings, L is not regular.

**Example:** L = {aⁿbⁿ}. Strings aᵏ for distinct k are pairwise distinguishable by the suffix bᵏ. Infinite classes → non-regular.

### 1.12 Homomorphism / Substitution Examples

**Example homomorphism h:** h(a) = 0, h(b) = 11. Apply to L: substitute each char.

**Substitution** is more general: each symbol maps to a **language**, not a single string.

### 1.13 Regular Set vs Regular Language

In some texts, "regular set" = regular language. Same thing.

### 1.14 Non-Closure (Regular)

Regular languages are **not closed under**:
- Substring (when defined as taking *fragment* of strings) — actually closed.

In fact, all common operations preserve regularity. The **distinguishing feature** of regular languages is broad closure.

### 1.15 Closure Comparison Table

| Op | Regular | CFL | CSL | Recursive | RE |
|---|---|---|---|---|---|
| ∪ | ✅ | ✅ | ✅ | ✅ | ✅ |
| ∩ | ✅ | ❌ | ✅ | ✅ | ✅ |
| Complement | ✅ | ❌ | ✅ | ✅ | ❌ |
| Concat | ✅ | ✅ | ✅ | ✅ | ✅ |
| Star | ✅ | ✅ | ✅ | ✅ | ✅ |
| Reverse | ✅ | ✅ | ✅ | ✅ | ✅ |
| Hom | ✅ | ✅ | ❌ | ❌ | ✅ |
| Inv hom | ✅ | ✅ | ✅ | ✅ | ✅ |

### 1.16 Common Pitfalls

- Pumping Lemma can prove **non-regularity**, not regularity.
- A language passing pumping lemma may still be **non-regular** (lemma is necessary, not sufficient).
- Closure operations sometimes apply only when **both** operands are regular.

> **Summary:** Use Pumping Lemma to prove non-regularity. Master full closure-property table. Regular languages decidable for all standard problems. Regular grammar = right-linear (or left-linear).

---

## 2. Important Points

- **Pumping Lemma** is necessary, not sufficient.
- Pumping length p depends on language; you don't know p but assume some exists.
- **You choose w, adversary chooses split.**
- Regular languages closed under all common operations.
- **Intersection of two regular = regular** (product construction).
- **Complement of regular = regular** (flip DFA).
- **Membership** in regular language: O(|w|) using DFA.
- **Emptiness** decidable in poly time.
- **Equivalence** decidable: minimize and compare.
- **Right-linear grammar = regular** (one-to-one with NFA).
- **Linear grammar** is more general (allows recursion in middle).
- Myhill-Nerode infinite classes ⇒ non-regular.
- **Closure paradox** is a useful trick: if L regular, some impossible language follows.

---

## 3. Short Notes

```
PUMPING LEMMA (regular)
 if L regular, ∃ p
 ∀ w ∈ L, |w| ≥ p:
   w = xyz, |y| ≥ 1, |xy| ≤ p
   xyⁱz ∈ L for all i ≥ 0

PROOF OF NON-REGULARITY
 1. assume L regular
 2. choose w
 3. analyze all splits
 4. find i with xyⁱz ∉ L

CLASSIC NON-REGULAR
 aⁿbⁿ, aⁿbⁿcⁿ, ww, palindromes,
 prime length, n²

CLOSURE (regular)
 ∪, ∩, complement, concat, *, reverse,
 difference, symm diff, hom, inv-hom,
 substitution, quotient, prefix, suffix

CONSTRUCTIONS
 union: ε-NFA
 intersection: product
 complement: flip DFA states
 reverse: reverse transitions

DECISION PROBLEMS
 membership: O(|w|)
 emptiness, finiteness, equivalence,
 containment, universality — decidable

REGULAR GRAMMARS
 right-linear: A → aB or A → a or A → ε
 left-linear: A → Ba or ...
 both = regular
 linear (mixed): possibly not regular

MYHILL-NERODE
 infinite classes ⇒ non-regular

CLOSURE COMPARISON (Reg / CFL / CSL / Rec / RE)
 ∩: ✓ ✗ ✓ ✓ ✓
 complement: ✓ ✗ ✓ ✓ ✗
 (all closed under ∪, concat, *, reverse, inv-hom)
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Pumping lemma necessary, not sufficient | ✅✅✅ |
| 2 | aⁿbⁿ not regular | ✅✅✅ |
| 3 | Regular closed under all common ops | ✅✅ |
| 4 | Intersection: product construction | ✅✅ |
| 5 | Complement: flip DFA | ✅✅ |
| 6 | Right-linear grammar = regular | ✅✅ |
| 7 | All decision problems decidable | ✅✅ |
| 8 | CFL not closed under intersection or complement | ✅ |
| 9 | Myhill-Nerode infinite classes ⇒ non-regular | ✅ |
| 10 | Pumping with adversary: you pick w | ✅✅ |

### Tricks

- **For pumping lemma proof:** pick w that exposes counting.
- **For closure proof:** show construction or use closure of regular under operations.
- **For non-closure (CFL):** find counterexample with intersection.
- **For decidability:** convert to graph reachability or DFA equivalence.
- **Myhill-Nerode shortcut:** find infinite distinguishing sequence.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
{aⁿbⁿ : n ≥ 0} regular?
**Solution.** No (pumping lemma).

### Q2. (GATE CSE 2014)
Regular languages closed under:
**Solution.** All common operations including intersection, complement.

### Q3. (GATE CSE 2018)
{aⁿbⁿcⁿ} regular?
**Solution.** No (not even CFL).

### Q4. (GATE CSE 2008)
Regular grammar form:
**Solution.** Right-linear or left-linear.

### Q5. (GATE CSE 2010)
CFL closed under intersection?
**Solution.** No.

### Q6. (GATE CSE 2015)
Pumping lemma proves:
**Solution.** Non-regularity (necessary condition).

### Q7. (GATE CSE 2013)
Membership in regular: time?
**Solution.** O(|w|).

### Q8. (GATE CSE 2007)
{ww : w ∈ Σ\*} regular?
**Solution.** No.

### Q9. (GATE CSE 2003)
Linear grammar = regular?
**Solution.** Not always; only right- or left-linear.

### Q10. (GATE CSE 2009)
Equivalence of two DFAs:
**Solution.** Decidable.

### Q11. (GATE CSE 2019)
Reverse of regular = regular?
**Solution.** Yes.

### Q12. (GATE CSE 2020)
Homomorphism preserves regularity?
**Solution.** Yes.

### Q13. (GATE CSE 2021)
Inverse homomorphism preserves regularity?
**Solution.** Yes.

### Q14. (GATE CSE 2016)
{aⁿ : n is prime} regular?
**Solution.** No.

### Q15. (GATE CSE 2011)
Pumping lemma: who chooses w and split?
**Solution.** You pick w; adversary picks split.

---

## 6. Practice Questions (20+)

### Easy

**P1.** State pumping lemma.

**P2.** What does pumping lemma prove?

**P3.** Is {aⁿbⁿ} regular?

**P4.** Are regular languages closed under intersection?

**P5.** Are regular closed under complement?

**P6.** Is {aⁿbᵐ : n, m ≥ 0} regular?

**P7.** Decision problem time for membership?

**P8.** Right-linear grammar = ?

**P9.** Are CFL closed under intersection?

**P10.** Is {ww} regular?

### Medium

**P11.** Apply pumping lemma to {0ⁿ1ⁿ}.

**P12.** Show union of two regular = regular.

**P13.** Construct DFA for L₁ ∩ L₂ via product.

**P14.** Apply pumping lemma to {aⁿ : n is prime}.

**P15.** Show {aⁿbᵐaⁿ} not regular.

**P16.** Closure under reverse: prove.

**P17.** L₁ regular, L₂ arbitrary; is L₁ ∪ L₂ regular?

**P18.** Find Myhill-Nerode classes for {aⁿbⁿ}.

**P19.** Equivalence: prove L = (a + b)\* and (a\*b\*)\* have same regular language.

**P20.** Show {ww^R} not regular.

### Hard

**P21.** Apply pumping lemma to {aⁿ²}.

**P22.** Prove regular languages closed under inverse homomorphism.

**P23.** Closure of CFL under union (proof).

**P24.** Show DFA equivalence is decidable.

**P25.** Construct DFA for L = (regex transformation).

**P26.** Show that regular ⊊ context-free ⊊ recursively enumerable.

**P27.** Prove finite languages are regular.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.1 | direct |
| P2 | non-regularity | direct |
| P3 | no | direct |
| P4 | yes | direct |
| P5 | yes | direct |
| P6 | yes (a*b*) | direct |
| P7 | O(|w|) | direct |
| P8 | regular | direct |
| P9 | no | direct |
| P10 | no | direct |
| P11 | classic proof | direct |
| P12 | ε-NFA combining | direct |
| P13 | trace product | direct |
| P14 | gaps grow → contradiction | direct |
| P15 | similar | direct |
| P16 | reverse all transitions | direct |
| P17 | not necessarily | direct |
| P18 | infinite classes | direct |
| P19 | both = Σ* | direct |
| P20 | similar to {ww} | direct |
| P21 | gaps between consecutive squares > p | direct |
| P22 | construction | direct |
| P23 | combine grammars | direct |
| P24 | minimize and compare | direct |
| P25 | direct | direct |
| P26 | hierarchy strict | direct |
| P27 | finite ⇒ regular | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Pumping lemma proves regularity | Only proves non-regularity. |
| 2 | Picking w too short | Choose |w| ≥ p. |
| 3 | Picking specific split | Adversary picks; consider all. |
| 4 | Forgetting xy²z (i = 2) | Try i = 0, 2, 3. |
| 5 | Linear grammar = regular grammar | Only right- or left-linear. |
| 6 | CFL closed under all ops | No: not under intersection, complement. |
| 7 | Regular closed under inverse hom | Yes, but may seem unintuitive. |
| 8 | Adversary chooses w | No, you choose. |
| 9 | Pumping lemma sufficient for regularity | Necessary only. |
| 10 | Treating finite as non-regular | Finite always regular. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Show L not regular" | Pumping lemma or Myhill-Nerode. |
| "Show L regular" | Build DFA/NFA/regex, or use closure. |
| "Closure under op" | Look up table; trust standard results. |
| "Decidable for regular" | Yes for membership, equivalence, etc. |
| "Right-linear grammar" | Regular language. |
| "Linear grammar" | Possibly broader than regular. |
| "Inverse homomorphism" | Preserves regularity. |
| "Two regulars combined" | Combination usually regular. |
| "CFL ∩ regular" | Always CFL. |
| "Complement of CFL" | Not always CFL. |

---

## 9. Quick Revision

```
PUMPING LEMMA
 if L regular: ∃p
 ∀w ∈ L, |w| ≥ p
 w = xyz, |y| ≥ 1, |xy| ≤ p
 xyⁱz ∈ L ∀i ≥ 0

NECESSARY, not sufficient

CLASSIC NON-REGULAR
 aⁿbⁿ, aⁿbⁿcⁿ, ww, wwᴿ,
 prime length, n²

CLOSURE (regular)
 ∪, ∩, complement, concat, *, reverse,
 hom, inv-hom, substitution, quotient

DECISION PROBLEMS (regular)
 membership O(|w|)
 emptiness, finiteness, equivalence,
 containment, universality — all decidable

REGULAR GRAMMAR
 right- or left-linear

CLOSURE COMPARISON
 regular: all common ops
 CFL: not closed under ∩, complement
 CSL, Rec: closed under both
 RE: not closed under complement

MYHILL-NERODE
 # min DFA states = # equivalence classes
 infinite classes ⇒ non-regular

ADVERSARY
 you pick w
 adversary picks split
```
