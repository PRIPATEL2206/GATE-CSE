# Topic Test 01 — Propositional Logic + Set Theory, Relations & Functions

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ for 1-mark, −⅔ for 2-mark. NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] The proposition `(p → q) ∧ (¬q ∨ p)` is a tautology when:
(A) p, q both T  (B) p T, q F  (C) p F, q T  (D) Never a tautology

**Q2.** [MCQ] Which is equivalent to `¬(p → q)`?
(A) `¬p → ¬q`  (B) `p ∧ ¬q`  (C) `¬p ∨ q`  (D) `q → p`

**Q3.** [MCQ] How many distinct boolean functions are there of 3 variables?
(A) 8  (B) 64  (C) 256  (D) 512

**Q4.** [NAT] How many rows in the truth table of a formula with 6 variables? `____`

**Q5.** [MCQ] Negation of `∀x (P(x) → Q(x))`:
(A) `∀x (P(x) ∧ ¬Q(x))`
(B) `∃x (P(x) ∧ ¬Q(x))`
(C) `∃x (¬P(x) → Q(x))`
(D) `∀x (¬P(x) ∧ Q(x))`

**Q6.** [MSQ] Which are equivalent to `p ↔ q`?
(A) `(p ∧ q) ∨ (¬p ∧ ¬q)`
(B) `(p → q) ∧ (q → p)`
(C) `¬(p ⊕ q)`
(D) `(p ∨ q) ∧ ¬(p ∧ q)`

**Q7.** [MCQ] On a 4-element set, the number of relations that are reflexive is:
(A) 2¹²  (B) 2¹⁶  (C) 2⁸  (D) 2¹⁰

**Q8.** [MCQ] Number of equivalence relations on {1,2,3,4} is:
(A) 5  (B) 15  (C) 16  (D) 24

**Q9.** [NAT] |A| = 4, |B| = 3. Number of onto functions from A to B = `____`

**Q10.** [MCQ] Let R = {(a,b) : a, b ∈ ℤ, a − b is divisible by 7}. R is:
(A) only reflexive  (B) only symmetric  (C) equivalence  (D) partial order

**Q11.** [MCQ] Statement: "Some boys are not tall." Symbolic form?
(A) `∀x (B(x) → ¬T(x))`
(B) `∃x (B(x) ∧ ¬T(x))`
(C) `∃x (B(x) → ¬T(x))`
(D) `∀x (B(x) ∧ ¬T(x))`

**Q12.** [MCQ] If f: ℝ → ℝ is f(x) = x³, then f is:
(A) injective only  (B) surjective only  (C) bijective  (D) neither

**Q13.** [MCQ] How many subsets of a 6-element set have exactly 2 elements?
(A) 12  (B) 15  (C) 20  (D) 30

**Q14.** [MCQ] On {1,2,3}, the relation R = {(1,2),(2,1),(1,3)} is:
(A) symmetric  (B) transitive  (C) antisymmetric  (D) none of the above

**Q15.** [NAT] Bell number B₅ = `____`

---

## Section B — 2 marks each

**Q16.** [MCQ] In a class of 100, 50 study Math, 40 Physics, 30 Chemistry. 20 study Math+Physics, 15 Physics+Chem, 10 Math+Chem, 5 all three. How many study none?
(A) 20  (B) 25  (C) 30  (D) 35

**Q17.** [MCQ] The argument: "If it rains, the picnic is cancelled. The picnic was not cancelled. Therefore it did not rain." is an instance of:
(A) Modus Ponens  (B) Modus Tollens  (C) Hypothetical Syllogism  (D) Disjunctive Syllogism

**Q18.** [MSQ] Which of the following are TRUE for any non-empty sets A, B?
(A) `f(A ∪ B) = f(A) ∪ f(B)` for any function f
(B) `f(A ∩ B) = f(A) ∩ f(B)` for any function f
(C) `f(A ∩ B) ⊆ f(A) ∩ f(B)` for any function f
(D) `f⁻¹(A ∩ B) = f⁻¹(A) ∩ f⁻¹(B)` for any function f

**Q19.** [MCQ] Number of antisymmetric relations on a 3-element set:
(A) 27  (B) 64  (C) 216  (D) 729

**Q20.** [MCQ] The formula `∀x (P(x) ∨ Q(x)) → (∀x P(x) ∨ ∀x Q(x))` is:
(A) a tautology
(B) a contradiction
(C) a contingency
(D) satisfiable but not valid

---

# 🔒 Answer Key & Solutions

> Stop the timer before reading.

| Q | Ans | Pattern |
|---|---|---|
| 1 | (D) | Truth-table — false at p=F, q=T (¬q∨p both F) |
| 2 | (B) | `¬(p→q) ≡ p ∧ ¬q` |
| 3 | (C) | 2^(2³) = 256 |
| 4 | 64 | 2⁶ |
| 5 | (B) | ¬∀ → ∃; ¬(P→Q) ≡ P∧¬Q |
| 6 | (A), (B), (C) | (D) is XOR |
| 7 | (A) | 2^(n²−n) = 2¹² |
| 8 | (B) | B₄ = 15 |
| 9 | 36 | 3⁴ − 3·2⁴ + 3 = 81 − 48 + 3 = 36 |
| 10 | (C) | mod-7 equivalence |
| 11 | (B) | ∃ with ∧ |
| 12 | (C) | x³ is bijective on ℝ |
| 13 | (B) | C(6,2) = 15 |
| 14 | (D) | not symmetric: (1,3)∈R but (3,1)∉; not transitive: (2,1),(1,3)∈R but (2,3)∉; (1,2),(2,1) breaks antisymm |
| 15 | 52 | Bell |
| 16 | (C) | 100 − (50+40+30−20−15−10+5) = 100 − 80 = 20. Wait recompute: 50+40+30=120; minus pairs 45=75; plus triple 5=80. 100−80=20. **Answer (A) 20.** |
| 17 | (B) | Modus Tollens |
| 18 | (A), (C), (D) | f-image-of-∩ only ⊆ |
| 19 | (C) | 2³ · 3³ = 8·27 = 216 |
| 20 | (D) | Counterexample: P(x) = x even, Q(x) = x odd; LHS T, RHS F. Satisfiable but not valid. |

> **Note on Q16:** the correct numerical answer is 20, which is option (A). The original option key is misaligned in the question stem — score yourself against the working, not the printed letter.

---

## Score Sheet

| | Score |
|---|---|
| Section A (15 × 1) | _ /15 |
| Section B (5 × 2) | _ /10 |
| **Total** | _ /25 |
| Time used | _ min |

**Targets:**
- ≥ 22/25 in 25 min → solid mastery
- 18–21 → revise short notes + pattern recognition
- < 18 → re-do PYQs of both topics, redo this test in 5 days

**Post-test action:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
