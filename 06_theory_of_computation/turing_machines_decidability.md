# Turing Machines, Decidability & Reducibility

> Subject: Theory of Computation
> GATE weight: **2–4 marks** every year. TM definition, decidability, halting problem, reductions.

---

## 1. Concept Explanation

### 1.1 Turing Machine (TM)

`M = (Q, Σ, Γ, δ, q₀, B, F)`:
- Q: states.
- Σ: input alphabet.
- Γ: tape alphabet (Σ ⊆ Γ).
- δ: Q × Γ → Q × Γ × {L, R, S} (sometimes also halt or stay).
- q₀: start state.
- B ∈ Γ \ Σ: blank symbol.
- F ⊆ Q: final/accept states.

**Operation:** read tape symbol, write new symbol, move head L or R, change state.

### 1.2 Acceptance, Rejection, Looping

A TM on input w can:
- **Accept** (reach accept state).
- **Reject** (reach reject state, or halt without accepting).
- **Loop forever**.

**Language accepted L(M)** = strings that lead to accept.

### 1.3 Recognizable vs Decidable

| Term | Definition |
|---|---|
| **Recursively Enumerable (RE) / Recognizable** | Some TM accepts L (may loop on rejects) |
| **Recursive / Decidable** | Some TM halts on every input, accepts iff w ∈ L |
| **co-RE** | Complement of RE |

`Decidable ⊊ RE`. **Decidable = RE ∩ co-RE.**

### 1.4 TM Variants — Same Power

| Variant | Equivalent? |
|---|---|
| Multi-tape TM | ✅ same power |
| Non-deterministic TM | ✅ same power |
| 2-way infinite tape | ✅ same power |
| Multi-track | ✅ same power |
| Stay-option (no move) | ✅ same power |

(Variants may differ in **time complexity**, but accept same languages.)

### 1.5 Church-Turing Thesis

Anything algorithmically computable can be computed by a TM. (A working hypothesis, not theorem.)

### 1.6 Halting Problem

**HALT_TM = {⟨M, w⟩ : TM M halts on w}**.

**Theorem:** HALT_TM is **undecidable**.

**Proof sketch (diagonalization):** Assume decider H. Construct D(⟨M⟩) that accepts iff M(⟨M⟩) loops, loops iff M(⟨M⟩) accepts. Apply D to itself → contradiction.

### 1.7 Other Undecidable Problems (TM-related)

| Problem | Description |
|---|---|
| **A_TM** | M accepts w? |
| **HALT_TM** | M halts on w? |
| **E_TM** | L(M) = ∅? |
| **EQ_TM** | L(M₁) = L(M₂)? |
| **REGULAR_TM** | L(M) is regular? |
| **CFL_TM** | L(M) is CFL? |

All RE but not decidable.

### 1.8 Rice's Theorem

**Any non-trivial property of L(M)** (depends only on language, not on machine) is **undecidable**.

"Non-trivial" = some TM has property, some doesn't.

**Examples:**
- Is L(M) empty?
- Is L(M) regular?
- Is L(M) finite?
- Does L(M) contain specific string?

All undecidable.

### 1.9 Reductions for Undecidability

To prove problem B undecidable: reduce known undecidable A to B.

**Mapping reduction:** A ≤_m B iff there's computable f such that x ∈ A ⇔ f(x) ∈ B.

**If A ≤_m B and A undecidable, then B undecidable.**

### 1.10 RE Closure Properties

RE closed under:
- ∪, ∩
- Concatenation, Kleene star
- Reverse
- Homomorphism, inverse homomorphism

**NOT closed under**:
- Complement (RE ∩ co-RE = decidable, but RE alone isn't closed under complement).

### 1.11 Decidable (Recursive) Closure

Decidable closed under:
- ∪, ∩, complement
- Concatenation, star, reverse
- Homomorphism, inverse homomorphism

### 1.12 Linear Bounded Automaton (LBA)

TM with tape limited to **input length**. Recognizes **Context-Sensitive Languages (CSL)**.

CSL = LBA-recognizable.

### 1.13 Chomsky Hierarchy

| Type | Language | Grammar | Automaton |
|---|---|---|---|
| Type 0 | RE | Unrestricted | TM |
| Type 1 | CSL | Context-Sensitive | LBA |
| Type 2 | CFL | Context-Free | NPDA |
| Type 3 | Regular | Right-linear (or left-linear) | DFA/NFA |

**Strict hierarchy:** Reg ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE.

### 1.14 Decidable Problems

| Problem | Decidable? |
|---|---|
| DFA membership | ✅ |
| DFA equivalence | ✅ |
| DFA emptiness | ✅ |
| CFG membership (CYK) | ✅ |
| CFG emptiness | ✅ |
| CFG equivalence | ❌ |
| TM membership | ❌ (semi-dec) |
| TM equivalence | ❌ |
| HALT_TM | ❌ |

### 1.15 Post Correspondence Problem (PCP)

Given pairs (a₁, b₁), …, (aₙ, bₙ) of strings. Is there sequence i₁, …, iₖ such that aᵢ₁ aᵢ₂ … aᵢₖ = bᵢ₁ bᵢ₂ … bᵢₖ?

**PCP is undecidable.** Often used as basis for further undecidability proofs.

### 1.16 Universal Turing Machine

A TM U such that U(⟨M, w⟩) simulates M on w. Existence of U is the basis for diagonalization arguments.

### 1.17 Time / Space Complexity Classes

| Class | Definition |
|---|---|
| TIME(f(n)) | Decidable in f(n) time |
| SPACE(f(n)) | Decidable in f(n) space |
| P | TIME(n^c) for some c |
| NP | NTIME(n^c) for some c |
| PSPACE | SPACE(n^c) |
| EXPTIME | TIME(2^(n^c)) |
| L | SPACE(log n) |
| NL | NSPACE(log n) |

**Hierarchies:**
- Time hierarchy theorem.
- Space hierarchy theorem.

P ⊆ NP ⊆ PSPACE ⊆ EXPTIME.

### 1.18 Classic Reductions

- **HALT_TM ≤_m A_TM:** halting reduces to acceptance.
- **A_TM ≤_m HALT_TM:** vice versa.
- **A_TM ≤_m E_TM** (via complement or direct).
- **A_TM ≤_m REGULAR_TM:** acceptance to regular-language test.
- **PCP ≤_m other undecidable** problems.

### 1.19 Decision Problems Summary

| Problem | Regular | CFG | TM |
|---|---|---|---|
| Membership | ✅ | ✅ (CYK) | ❌ (semi-dec) |
| Emptiness | ✅ | ✅ | ❌ |
| Equivalence | ✅ | ❌ | ❌ |
| Universality | ✅ | ❌ | ❌ |
| Containment | ✅ | ❌ | ❌ |

### 1.20 Decidable, Semi-decidable, Undecidable

- **Decidable:** halting decider exists.
- **Semi-decidable (RE):** TM accepts members; may loop on non-members.
- **Co-RE:** TM rejects (i.e., accepts complement).
- **Undecidable but RE:** A_TM, HALT_TM.
- **Neither RE nor co-RE:** EQ_TM (equivalence of TMs).

> **Summary:** TM = ultimate computation model. Halting problem undecidable (diagonalization). Rice's theorem kills almost all language properties of TMs. Chomsky hierarchy: Reg ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE.

---

## 2. Important Points

- **TM variants** (multi-tape, non-deterministic) all equivalent in power.
- **Halting problem is undecidable** (diagonalization).
- **Rice's theorem** kills decidability of non-trivial language properties.
- **A_TM, HALT_TM** are RE but not decidable.
- **EQ_TM** is neither RE nor co-RE.
- **PCP** is undecidable; common reduction tool.
- **LBA = CSL.**
- **Chomsky hierarchy** is strict: Reg ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE.
- **Decidable** = recursive = halting on all inputs.
- **Decidable = RE ∩ co-RE.**
- **RE closed under union, intersection** but NOT complement.
- **Mapping reductions** preserve decidability and recognizability.
- **Universal TM** simulates any TM.

---

## 3. Short Notes

```
TM = (Q, Σ, Γ, δ, q₀, B, F)
 δ: Q × Γ → Q × Γ × {L, R, S}

OUTCOMES: accept, reject, loop

LANGUAGE CLASSES
 Recursive (decidable): TM halts on all
 RE (recognizable): TM accepts members
 co-RE: TM rejects non-members
 Decidable = RE ∩ co-RE

VARIANTS (same power)
 multi-tape, NTM, 2-way, multi-track

CHURCH-TURING THESIS:
 algorithm = TM

HALTING PROBLEM
 HALT_TM = {⟨M, w⟩ : M halts on w}
 undecidable (diagonalization)

OTHER UNDECIDABLE
 A_TM, E_TM, EQ_TM, REGULAR_TM, CFL_TM

RICE'S THEOREM
 non-trivial property of L(M) = undecidable

REDUCTIONS
 A ≤_m B (computable f)
 if A undecidable and A ≤_m B → B undecidable

LBA = CSL (Type 1)

CHOMSKY HIERARCHY
 Type 3: Regular (DFA, right-linear)
 Type 2: CFL (NPDA, CFG)
 Type 1: CSL (LBA, CSG)
 Type 0: RE (TM, unrestricted)

CLOSURE
 RE: ∪, ∩, concat, *, reverse, hom, inv-hom
 (NOT complement)
 Recursive: all + complement

DECIDABILITY TABLE
 regular: all decidable
 CFG: membership/empty/finite ✓; equiv ✗
 TM: all of A_TM, HALT, E, EQ undecidable

PCP (Post Correspondence)
 undecidable

UTM: simulates any TM
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | TM variants equivalent in power | ✅✅ |
| 2 | HALT_TM undecidable (Halting Problem) | ✅✅✅ |
| 3 | Rice's theorem | ✅✅ |
| 4 | A_TM ≤_m HALT_TM and vice versa | ✅ |
| 5 | Decidable = RE ∩ co-RE | ✅✅ |
| 6 | RE closed under ∪, ∩; NOT complement | ✅ |
| 7 | Chomsky: Reg ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE | ✅✅ |
| 8 | LBA recognizes CSL | ✅ |
| 9 | EQ_TM neither RE nor co-RE | ✅ |
| 10 | Mapping reduction A ≤_m B | ✅ |
| 11 | PCP undecidable | ✅ |
| 12 | Universal TM exists | ✅ |

### Tricks

- **For "is L decidable" questions:** check if it's a property of L(M) — if non-trivial, undecidable (Rice).
- **Reductions to prove undecidability:** reduce HALT or A_TM to your problem.
- **For "is L recognizable":** often easier than decidable — TM accepts members, may loop on non-members.
- **co-RE characterization:** check if non-members are recognizable.
- **Decidable problems for TM:** TM equivalence is the king of undecidability.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Halting problem:
**Solution.** Undecidable.

### Q2. (GATE CSE 2014)
Multi-tape TM equivalent to standard TM?
**Solution.** Yes, in power.

### Q3. (GATE CSE 2018)
Rice's theorem applies to:
**Solution.** Non-trivial language properties of TMs.

### Q4. (GATE CSE 2008)
Decidable = ?
**Solution.** RE ∩ co-RE.

### Q5. (GATE CSE 2010)
Chomsky type 0:
**Solution.** Recursively enumerable.

### Q6. (GATE CSE 2015)
LBA accepts:
**Solution.** Context-sensitive languages.

### Q7. (GATE CSE 2013)
RE closed under complement?
**Solution.** No.

### Q8. (GATE CSE 2007)
A_TM = "M accepts w" — decidable?
**Solution.** No (RE but not decidable).

### Q9. (GATE CSE 2003)
PCP is:
**Solution.** Undecidable.

### Q10. (GATE CSE 2009)
TM equivalence (EQ_TM):
**Solution.** Undecidable.

### Q11. (GATE CSE 2019)
NTM more powerful than DTM?
**Solution.** Same power.

### Q12. (GATE CSE 2020)
Universal TM:
**Solution.** Simulates any TM on any input.

### Q13. (GATE CSE 2021)
"L(M) = ∅" decidable?
**Solution.** No (Rice).

### Q14. (GATE CSE 2016)
Can we decide if L(M) is regular?
**Solution.** No.

### Q15. (GATE CSE 2011)
Reduction A ≤_m B implies:
**Solution.** B at least as hard as A.

---

## 6. Practice Questions (20+)

### Easy

**P1.** State Halting Problem.

**P2.** Recursive vs RE.

**P3.** Define decidable.

**P4.** What is Rice's Theorem?

**P5.** Chomsky type 1 = ?

**P6.** Universal TM definition.

**P7.** TM tape alphabet vs input alphabet?

**P8.** RE ∩ co-RE = ?

**P9.** Is A_TM in RE?

**P10.** What is LBA?

### Medium

**P11.** Show HALT undecidable via diagonalization.

**P12.** Is L(M) finite decidable?

**P13.** Is L(M) regular decidable?

**P14.** A_TM ≤_m HALT — show reduction.

**P15.** Show RE closed under union.

**P16.** Show RE not closed under complement.

**P17.** PCP example with 3 pairs.

**P18.** Show that EQ_TM neither RE nor co-RE.

**P19.** Compare DTM and NTM time-complexity.

**P20.** Decide if L(M) contains specific string w.

### Hard

**P21.** Prove Rice's Theorem.

**P22.** Show that the language L_TM = {⟨M⟩ : M loops on ε} is not RE.

**P23.** Reduce HALT to A_TM.

**P24.** Show that {⟨M, w⟩ : M halts on w in 100 steps} is decidable.

**P25.** Show that the set of regular languages is decidable, but "is L(M) regular?" is not.

**P26.** Show CSL closed under complement (Immerman-Szelepcsényi).

**P27.** Construct universal TM (high-level idea).

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | does TM M halt on input w? | direct |
| P2 | recursive halts; RE may loop on rejects | direct |
| P3 | TM halts on every input | direct |
| P4 | non-trivial property of L(M) is undecidable | direct |
| P5 | CSL | direct |
| P6 | TM that simulates any TM | direct |
| P7 | Σ ⊆ Γ | direct |
| P8 | decidable | direct |
| P9 | yes (semi-decidable) | direct |
| P10 | linear bounded automaton | direct |
| P11 | classic diagonal | direct |
| P12 | no (Rice) | direct |
| P13 | no | direct |
| P14 | construct M' that simulates M | direct |
| P15 | dovetail | direct |
| P16 | use HALT non-recognizability | direct |
| P17 | trace | direct |
| P18 | uses two-way reduction | direct |
| P19 | DTM polynomial vs NTM exponential simulation | direct |
| P20 | undecidable (Rice) | direct |
| P21 | reduce A_TM | direct |
| P22 | complement of HALT-style | direct |
| P23 | trivial reduction | direct |
| P24 | bounded simulation | direct |
| P25 | first decidable, second Rice | direct |
| P26 | classical | direct |
| P27 | encode M, simulate δ | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Assume HALT decidable | Famous undecidable. |
| 2 | Confuse decidable with RE | Decidable ⊊ RE. |
| 3 | Think NTM > DTM in power | Same power. |
| 4 | Apply Rice to syntactic property | Rice only for language property. |
| 5 | RE closed under complement | No (only decidable). |
| 6 | EQ_TM is RE | Neither RE nor co-RE. |
| 7 | LBA = TM | LBA is CSL only. |
| 8 | Treat Halting as decidable for finite M | M is infinite-state if needed. |
| 9 | Reductions reverse direction | A ≤_m B means B at least as hard. |
| 10 | Confuse mapping with Turing reductions | Mapping is one-way computable. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Halting problem" | Undecidable. |
| "Property of L(M)" | Rice → undecidable. |
| "TM equivalence" | Undecidable. |
| "Regular language equivalence" | Decidable. |
| "CFG equivalence" | Undecidable. |
| "RE" | Recognizer; may loop. |
| "Decidable" | Halts on every input. |
| "Reduce A to B" | A ≤_m B; if A undec, so is B. |
| "Variants of TM" | Same power. |
| "PCP" | Undecidable; reductions tool. |

---

## 9. Quick Revision

```
TM = (Q, Σ, Γ, δ, q₀, B, F)
δ: Q × Γ → Q × Γ × {L, R, S}

OUTCOMES: accept / reject / loop

CLASSES
 recursive (decidable): halts on all
 RE (recognizable): accepts members
 co-RE: rejects non-members
 decidable = RE ∩ co-RE

VARIANTS = same power: multi-tape, NTM, 2-way

CHURCH-TURING: algorithm = TM

HALTING PROBLEM: undecidable
A_TM, E_TM, EQ_TM, REGULAR_TM: all undecidable

RICE: non-trivial L(M) property → undecidable

REDUCTION: A ≤_m B
 A undec + A ≤_m B → B undec

LBA = CSL (Type 1)

CHOMSKY
 Type 3: regular (DFA)
 Type 2: CFL (NPDA)
 Type 1: CSL (LBA)
 Type 0: RE (TM)
 Reg ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE

CLOSURE
 RE: ∪, ∩, concat, *, reverse, hom, inv-hom
 (NOT complement)
 Recursive: all closures

PCP undecidable

UTM exists
```
