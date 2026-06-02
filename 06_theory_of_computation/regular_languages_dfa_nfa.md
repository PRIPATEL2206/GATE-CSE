# Regular Languages, DFA/NFA & Regex

> Subject: Theory of Computation
> GATE weight: **3–5 marks** every year. Finite automata, regular expressions, conversions, minimization.

---

## 1. Concept Explanation

### 1.1 Alphabets, Strings, Languages

| Term | Definition |
|---|---|
| **Alphabet (Σ)** | Finite, non-empty set of symbols |
| **String** | Finite sequence of symbols from Σ |
| **Σ\*** | Set of all strings over Σ (including ε) |
| **Σ⁺** | Σ\* − {ε} (non-empty strings) |
| **Language L** | Subset of Σ\* |
| **|w|** | Length of string w |
| **ε** | Empty string (length 0) |
| **w^R** | Reverse of w |

### 1.2 Operations on Strings

- **Concatenation:** w·x.
- **Power:** wⁿ = w concatenated n times; w⁰ = ε.
- **Reverse:** w^R.

### 1.3 Operations on Languages

| Operation | Definition |
|---|---|
| Union | L₁ ∪ L₂ |
| Intersection | L₁ ∩ L₂ |
| Complement | L̄ = Σ\* − L |
| Concatenation | L₁L₂ = {xy : x ∈ L₁, y ∈ L₂} |
| Kleene star | L\* = ∪ Lⁿ for n ≥ 0 |
| Kleene plus | L⁺ = ∪ Lⁿ for n ≥ 1 |
| Reverse | L^R |

### 1.4 Deterministic Finite Automaton (DFA)

`M = (Q, Σ, δ, q₀, F)`:
- Q: finite set of states.
- Σ: alphabet.
- δ: Q × Σ → Q (transition function — total).
- q₀ ∈ Q: start state.
- F ⊆ Q: set of final (accept) states.

**Acceptance:** w accepted iff δ\*(q₀, w) ∈ F.

DFA = exactly one transition per (state, symbol).

### 1.5 Non-deterministic Finite Automaton (NFA)

Same tuple, but δ: Q × Σ → 2^Q (set of states; possibly multiple).

**Acceptance:** w accepted iff some path leads to a final state.

### 1.6 NFA with ε-transitions (ε-NFA)

δ: Q × (Σ ∪ {ε}) → 2^Q. ε-transitions consume no input.

### 1.7 Equivalence

DFA, NFA, and ε-NFA are **equivalent** in expressive power — they all recognize **regular languages**.

### 1.8 NFA → DFA (Subset Construction)

For NFA with n states, equivalent DFA has up to 2ⁿ states.

```
new state = subset of NFA states
δ_DFA(S, a) = ∪ δ_NFA(q, a) for q in S
start: ε-closure({q₀})
accept: any subset containing an NFA accept state
```

### 1.9 DFA Minimization

Find equivalent DFA with **minimum** states.

**Algorithm (Hopcroft / Myhill-Nerode):**
1. Remove unreachable states.
2. Partition states into equivalence classes (Myhill-Nerode).
3. Two states equivalent if same behavior on all strings.

**Time:** O(n log n) (Hopcroft); O(n²) standard table-filling.

### 1.10 Myhill-Nerode Theorem

L is regular ⇔ # of equivalence classes of `≡_L` (Myhill-Nerode) is finite.

**Equivalence:** x ≡_L y iff ∀z: xz ∈ L ⇔ yz ∈ L.

# states in min DFA = # equivalence classes.

### 1.11 Regular Expression

Inductive definition:
- ∅, ε, a (a ∈ Σ) are regex.
- If r, s are regex: (r + s), (rs), (r\*) are regex.

Operations precedence: \* > concat > +.

### 1.12 Regex → NFA (Thompson's Construction)

| Regex | NFA |
|---|---|
| ε | start ─ε→ accept |
| a | start ─a→ accept |
| r₁ + r₂ | ε-branch to r₁ and r₂ |
| r₁r₂ | concat |
| r\* | ε-loop with start/accept |

Linear in regex size.

### 1.13 NFA → Regex (State Elimination)

Reduce graph by eliminating intermediate states; combine paths via concat/union/star. Output regex from start to accept.

### 1.14 Regular Language Closure (preview)

Regular languages closed under:
- Union, concatenation, Kleene star.
- Intersection, complement.
- Difference, reverse.
- Homomorphism, inverse homomorphism.

(See [pumping_lemma_closure_regular.md](pumping_lemma_closure_regular.md).)

### 1.15 Two-Way DFA / Mealy / Moore

| Machine | Description |
|---|---|
| **2-DFA** | Can move right and left | same power as DFA |
| **Mealy** | Output on transitions | finite-state transducer |
| **Moore** | Output on states | equivalent to Mealy |

### 1.16 Common Regular Languages

| Language | Description |
|---|---|
| Σ\* | All strings |
| {ε} | Just empty |
| Even-length strings | (ΣΣ)\* |
| Strings ending in 0 | Σ\*0 |
| At most 2 a's | aaa-free |
| Divisible by 3 in binary | DFA with 3 states |

### 1.17 Common Non-Regular Languages

- {aⁿbⁿ : n ≥ 0}
- {wwᴿ : w ∈ Σ\*} (palindromes)
- {ww : w ∈ Σ\*}
- {aⁿ : n is prime}
- {aⁿ²}

These need at least context-free or beyond.

### 1.18 DFA Tricks for Common Patterns

**Strings with substring "ab":** 3-state DFA (no a, saw a, saw ab).

**Strings divisible by k in base b:** DFA with k states (track remainder).

**Strings containing equal a's and b's:** NOT regular (counting required).

### 1.19 Regular Expression Identities

| Identity |
|---|
| r + r = r |
| (r\*)\* = r\* |
| (rs)\*r = r(sr)\* |
| (r + s)\* = (r\*s\*)\* = (r\* + s\*)\* |
| ε + rr\* = r\*r + ε = r\* |
| (ε + r)\* = r\* |
| r∅ = ∅r = ∅ |

> **Summary:** DFA/NFA/ε-NFA all equivalent. NFA → DFA via subset construction (2ⁿ states max). Regex ↔ NFA conversions are systematic. Master DFA design for common patterns + minimization.

---

## 2. Important Points

- **DFA has unique transition** per (state, symbol); NFA may have many.
- **NFA with n states → DFA with up to 2ⁿ states.**
- **# states in min DFA** = # Myhill-Nerode classes of L.
- **DFA, NFA, ε-NFA, regex** all equivalent → regular languages.
- **Regular languages closed** under union, intersection, complement, concat, star, reverse, homomorphism.
- **Pumping lemma** proves non-regularity.
- **{aⁿbⁿ} is non-regular** — counting requires unbounded memory.
- **Minimization** removes unreachable + merges equivalent states.
- **Mealy and Moore** are equivalent in power (with possible state-count differences).
- **Regular grammar** (right-linear or left-linear) generates regular languages.
- **2-way DFA** = same power as DFA.
- For binary divisibility: DFA size = divisor.
- **Concatenation** is non-commutative: L₁L₂ ≠ L₂L₁ in general.
- **Empty string ε** is in L\* always, even if L = ∅.
- The **minimum DFA is unique** up to renaming.

---

## 3. Short Notes

```
ALPHABET, STRINGS
 Σ alphabet; Σ* all strings; ε empty
 |w|, w^R

LANGUAGE OPS
 union, intersection, complement
 concat L₁L₂
 Kleene star L*; plus L⁺
 reverse L^R

DFA: M = (Q, Σ, δ, q₀, F)
 δ: Q × Σ → Q

NFA: δ: Q × Σ → 2^Q
ε-NFA: + ε transitions
DFA = NFA = ε-NFA = REGEX in power

NFA → DFA: subset construction
 up to 2ⁿ states

DFA MINIMIZATION
 remove unreachable
 merge equivalent (table-filling / Hopcroft)
 unique min DFA

MYHILL-NERODE
 # states in min DFA = # equivalence classes
 L regular ⇔ finite classes

REGEX
 ∅, ε, a primitive
 +, concat, *
 precedence: * > concat > +

REGEX ↔ NFA
 Thompson construction
 state elimination

CLOSURE: regular under ∪, ∩, complement, concat, *, reverse

REGULAR GRAMMAR: right-linear or left-linear

NON-REGULAR: aⁿbⁿ, palindromes, ww, aⁿ²

REGEX IDENTITIES
 r + r = r
 (r*)* = r*
 (r + s)* = (r*s*)*
 ε + rr* = r*

MEALY / MOORE: equivalent power
2-DFA = DFA in power
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | DFA, NFA, ε-NFA, Regex equivalent | ✅✅✅ |
| 2 | NFA to DFA: 2ⁿ states max | ✅✅✅ |
| 3 | Min DFA states = # MN classes | ✅✅ |
| 4 | Regular languages closed under ∪, ∩, complement, concat, * | ✅✅ |
| 5 | aⁿbⁿ not regular | ✅✅ |
| 6 | Regex precedence: * > concat > + | ✅ |
| 7 | (r + s)* = (r*s*)* | ✅ |
| 8 | DFA divisibility by k: k states | ✅ |
| 9 | Substring search DFA: m+1 states for pattern of length m | ✅ |
| 10 | Regular grammar = right/left linear | ✅ |
| 11 | Mealy = Moore in power | ✅ |
| 12 | 2-DFA = 1-DFA in power | ✅ |

### Tricks

- **DFA design for "contains 101":** 4 states (none, 1, 10, 101).
- **DFA for "ends in pattern":** track last m characters.
- **NFA may be exponentially smaller** than DFA.
- **Regex simplification:** use identities; check examples.
- **For minimization:** start with all final vs non-final pairs; then refine.
- **DFA for binary divisible by k:** state = remainder mod k.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
NFA with n states converted to DFA: max states?
**Solution.** 2ⁿ.

### Q2. (GATE CSE 2014)
DFA, NFA, ε-NFA equivalent in power?
**Solution.** Yes.

### Q3. (GATE CSE 2018)
Number of states in min DFA recognizing strings divisible by 3 (binary):
**Solution.** 3.

### Q4. (GATE CSE 2008)
{aⁿbⁿ : n ≥ 0} is regular?
**Solution.** No.

### Q5. (GATE CSE 2010)
Min DFA for "strings ending in 01":
**Solution.** 3 states (start, after 0, after 01).

### Q6. (GATE CSE 2015)
Regex (a + b)\*ab represents:
**Solution.** Strings ending in "ab".

### Q7. (GATE CSE 2013)
Conversion NFA → DFA worst case:
**Solution.** Exponential blow-up.

### Q8. (GATE CSE 2007)
DFA for ((a + b)\*aba) — # states in min DFA?
**Solution.** 4.

### Q9. (GATE CSE 2003)
NFA states = 5; DFA worst case states?
**Solution.** 32 (2⁵).

### Q10. (GATE CSE 2009)
Closed under complement?
**Solution.** Regular languages — yes.

### Q11. (GATE CSE 2019)
Min DFA accepting strings with even number of 0s:
**Solution.** 2 states (parity of 0).

### Q12. (GATE CSE 2020)
Regular expression for "even number of a's over {a, b}":
**Solution.** b\*(ab\*ab\*)\*.

### Q13. (GATE CSE 2021)
Number of states in min DFA: strings with substring "11":
**Solution.** 3 states.

### Q14. (GATE CSE 2016)
Mealy machine vs Moore: which has fewer states?
**Solution.** Mealy may have fewer.

### Q15. (GATE CSE 2011)
Equivalence of two DFAs decidable?
**Solution.** Yes (compare minimal forms).

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define DFA.

**P2.** NFA states = 4; DFA worst case states?

**P3.** L = {aⁿbⁿ}: regular?

**P4.** Regex precedence order?

**P5.** L = ∅ is regular?

**P6.** Smallest DFA for L = {ε}?

**P7.** Smallest DFA for L = Σ\*?

**P8.** What does Σ⁺ mean?

**P9.** Regex for "strings ending in 0"?

**P10.** Regex (0 + 1)\* represents?

### Medium

**P11.** Construct DFA for "even number of a's".

**P12.** Construct NFA for "ends in ab".

**P13.** Convert NFA from P12 to DFA.

**P14.** Minimize DFA: 5-state machine.

**P15.** Regex for "binary numbers divisible by 4".

**P16.** Apply state elimination to derive regex from DFA.

**P17.** Regex (a + b)\*a(a + b) — # states in min DFA?

**P18.** Show {aᵐbⁿ : m, n ≥ 0} is regular.

**P19.** Equivalence of (a + b)\* and (a\*b\*)\*.

**P20.** DFA for divisible by 5 in binary.

### Hard

**P21.** Convert ε-NFA to DFA via subset construction.

**P22.** Apply Myhill-Nerode to L = {ww}.

**P23.** Show that union of two regular = regular.

**P24.** Regex for "binary strings with no two consecutive 1s".

**P25.** Construct DFA for "strings with substring 11 and ending in 0".

**P26.** Equivalence between DFAs via product construction.

**P27.** Show Mealy and Moore equivalent.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.4 | direct |
| P2 | 16 | 2⁴ |
| P3 | no | direct |
| P4 | * > concat > + | direct |
| P5 | yes | direct |
| P6 | 1 state (start = accept), self-loops | direct |
| P7 | 1 state (loop) | direct |
| P8 | non-empty strings | direct |
| P9 | (0+1)*0 | direct |
| P10 | all binary strings | direct |
| P11 | 2 states | direct |
| P12 | 3-state NFA | direct |
| P13 | 3-state DFA | direct |
| P14 | merge equivalent classes | direct |
| P15 | binary ending 00 | direct |
| P16 | trace state elim | direct |
| P17 | 4 states | direct |
| P18 | regex a*b* | direct |
| P19 | both = Σ* | direct |
| P20 | 5 states (mod 5) | direct |
| P21 | trace ε-closures | direct |
| P22 | infinite classes ⇒ non-regular | direct |
| P23 | product construction | direct |
| P24 | (0 + 10)*(1 + ε) | direct |
| P25 | combine 11 and ending 0 | direct |
| P26 | accept iff XOR finalness | direct |
| P27 | construction both ways | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Treating NFA strictly weaker than DFA | Same language class. |
| 2 | DFA must have transitions for **all** symbols | Total function. |
| 3 | Confusing Kleene star vs plus | * includes ε; + does not. |
| 4 | NFA → DFA always 2ⁿ states | Often fewer. |
| 5 | Forgetting min DFA uniqueness | Up to isomorphism. |
| 6 | Regex precedence: + binds tightest (myth) | * > concat > +. |
| 7 | Regular implies finite | No — can be infinite. |
| 8 | aⁿbⁿ regular (myth) | Non-regular. |
| 9 | Mealy more powerful than Moore | Same power. |
| 10 | 2-DFA more powerful than DFA | Same power. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Number of states in min DFA" | Compute Myhill-Nerode classes. |
| "NFA → DFA" | Subset construction. |
| "Regex → NFA" | Thompson's construction. |
| "NFA → Regex" | State elimination. |
| "Regular?" | Build DFA or use closure properties. |
| "Non-regular" | Pumping lemma. |
| "Substring contained" | DFA with prefix tracking. |
| "Divisibility in base k" | DFA with k states. |
| "Closure under op" | List of regular closure properties. |
| "Mealy vs Moore" | Equivalent in power. |

---

## 9. Quick Revision

```
DFA = (Q, Σ, δ, q₀, F); δ: Q×Σ→Q
NFA: δ: Q×Σ→2^Q
ε-NFA: + ε transitions

EQUIVALENT: DFA = NFA = ε-NFA = Regex
NFA → DFA: subset, up to 2ⁿ states

MIN DFA = # Myhill-Nerode classes
Hopcroft O(n log n)

REGEX
 ∅, ε, a primitive
 +, concat, *
 precedence: * > concat > +

REGEX ↔ NFA
 Thompson, state elimination

CLOSURE (regular)
 ∪, ∩, complement, concat, *, reverse, hom

NON-REGULAR
 aⁿbⁿ, palindromes, ww

DFA TRICKS
 div by k base b: k states
 substring of length m: m+1 states

REGEX IDENTITIES
 (r*)* = r*
 (r + s)* = (r*s*)*
 ε + rr* = r*

MEALY = MOORE in power
2-DFA = DFA in power
```
