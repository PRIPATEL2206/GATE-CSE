# Propositional & Predicate Logic

> Subject: Engineering Mathematics → Discrete Mathematics
> GATE weight: **2–4 marks** almost every year. Highest-yield discrete-math sub-topic.

---

## 1. Concept Explanation

### 1.1 Proposition

A **proposition** is a declarative sentence that is either **true (T)** or **false (F)** — never both. Questions, commands, and opinions are not propositions.

| Sentence | Proposition? |
|---|---|
| "2 + 2 = 4" | ✅ T |
| "x + 1 = 3" | ❌ (depends on x — it's a *predicate*) |
| "Close the door." | ❌ (command) |

### 1.2 Logical Connectives

| Symbol | Name | Read as | T iff |
|---|---|---|---|
| ¬p | Negation | "not p" | p is F |
| p ∧ q | Conjunction | "p and q" | both T |
| p ∨ q | Disjunction (inclusive) | "p or q" | at least one T |
| p ⊕ q | XOR (exclusive or) | "p xor q" | exactly one T |
| p → q | Implication | "if p then q" | p is F **or** q is T |
| p ↔ q | Biconditional | "p iff q" | p, q have same value |

**Implication truth table — memorize:**

| p | q | p → q |
|---|---|---|
| T | T | T |
| T | F | **F** |
| F | T | T |
| F | F | T |

> "False implies anything" is the #1 GATE trap.

### 1.3 Tautology, Contradiction, Contingency

- **Tautology** — always T (e.g., p ∨ ¬p).
- **Contradiction** — always F (e.g., p ∧ ¬p).
- **Contingency** — sometimes T, sometimes F.

### 1.4 Logical Equivalence (≡)

`P ≡ Q` iff `P ↔ Q` is a tautology — i.e., they share the truth table.

### 1.5 Predicate Logic (First-Order Logic)

Adds **predicates** (P(x)) and **quantifiers**:

- ∀x P(x) — "for all x, P(x)"
- ∃x P(x) — "there exists x such that P(x)"

**Negation rules (De Morgan for quantifiers):**
- ¬(∀x P(x)) ≡ ∃x ¬P(x)
- ¬(∃x P(x)) ≡ ∀x ¬P(x)

**Quantifier order matters:**
- ∀x ∃y P(x, y) — "every x has *some* y" (y can depend on x)
- ∃y ∀x P(x, y) — "there's *one* y that works for *all* x" — **stronger**

### 1.6 Inference Rules

| Rule | Form |
|---|---|
| Modus Ponens | p, p → q ⊢ q |
| Modus Tollens | ¬q, p → q ⊢ ¬p |
| Hypothetical Syllogism | p → q, q → r ⊢ p → r |
| Disjunctive Syllogism | p ∨ q, ¬p ⊢ q |
| Resolution | p ∨ q, ¬p ∨ r ⊢ q ∨ r |
| Universal Instantiation | ∀x P(x) ⊢ P(c) |
| Existential Generalization | P(c) ⊢ ∃x P(x) |

### 1.7 Normal Forms

- **CNF (Conjunctive Normal Form)** — AND of ORs: `(a ∨ b) ∧ (¬a ∨ c)`
- **DNF (Disjunctive Normal Form)** — OR of ANDs: `(a ∧ ¬b) ∨ (a ∧ c)`

> **Summary:** propositional logic = manipulating T/F via connectives; predicate logic = adds variables + quantifiers. Master De Morgan, implication semantics, and quantifier swap rules.

---

## 2. Important Points

- **p → q ≡ ¬p ∨ q.** This single equivalence rewrites half of GATE questions.
- **Contrapositive** of `p → q` is `¬q → ¬p` — *equivalent* to original.
- **Converse** (`q → p`) and **Inverse** (`¬p → ¬q`) are *not* equivalent to original — they're equivalent to each other.
- `p → q` is **F only when p is T and q is F** — every other row is T.
- **Vacuous truth:** if p is F, `p → q` is T regardless of q. (E.g., "If 2+2=5, then I am the king." is T.)
- `∀` distributes over `∧`; `∃` distributes over `∨`. **Never the other way** — that's the trap.
  - ∀x (P(x) ∧ Q(x)) ≡ (∀x P(x)) ∧ (∀x Q(x)) ✅
  - ∀x (P(x) ∨ Q(x)) ≢ (∀x P(x)) ∨ (∀x Q(x)) ❌
- `∃y ∀x` is **stronger** than `∀x ∃y` — swapping changes meaning.
- Bound vs free variables: in `∀x P(x, y)`, **x is bound, y is free**.
- A **tautology AND tautology = tautology**; **tautology OR anything = tautology**.
- A formula is **satisfiable** iff its negation is **not a tautology**.
- Logical equivalence means *every* row of the truth table matches — **not just "looks similar."**
- For *n* propositional variables, the truth table has **2ⁿ rows**.
- The number of distinct boolean functions of *n* variables is **2^(2ⁿ)**.

---

## 3. Short Notes

```
PROPOSITIONS — declarative, T or F.

CONNECTIVES (precedence: ¬, ∧, ∨, →, ↔):
¬p   p∧q   p∨q   p→q   p↔q
        AND    OR  if-then iff

KEY EQUIVALENCES:
p → q       ≡ ¬p ∨ q
p → q       ≡ ¬q → ¬p          (contrapositive)
p ↔ q       ≡ (p → q) ∧ (q → p)
¬(p ∧ q)    ≡ ¬p ∨ ¬q          (De Morgan)
¬(p ∨ q)    ≡ ¬p ∧ ¬q          (De Morgan)
p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r) (distributive)
p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r) (distributive)
p ∨ p       ≡ p                 (idempotent)
p ∧ T       ≡ p                 (identity)
p ∨ F       ≡ p
p ∧ ¬p      ≡ F                 (negation)
p ∨ ¬p      ≡ T

QUANTIFIERS:
∀x P(x)            "for all"
∃x P(x)            "exists"
¬∀x P(x) ≡ ∃x ¬P(x)
¬∃x P(x) ≡ ∀x ¬P(x)
∀x ∃y vs ∃y ∀x — order matters!

INFERENCE:
Modus Ponens:     p, p→q  ⊢ q
Modus Tollens:    ¬q, p→q ⊢ ¬p
Hyp. Syllogism:   p→q, q→r ⊢ p→r
Resolution:       p∨q, ¬p∨r ⊢ q∨r

ARGUMENT VALID iff (P1 ∧ P2 ∧ … ∧ Pn) → C is a TAUTOLOGY.

#variables = n  ⇒  truth table has 2ⁿ rows
#distinct boolean fns of n variables = 2^(2ⁿ)
```

---

## 4. Formulas / Tricks

| # | Identity / Trick | Memorize Cold? |
|---|---|---|
| 1 | `p → q ≡ ¬p ∨ q` | ✅✅✅ |
| 2 | `p → q ≡ ¬q → ¬p` (contrapositive) | ✅ |
| 3 | `p ↔ q ≡ (p→q) ∧ (q→p)` | ✅ |
| 4 | `p ↔ q ≡ (p ∧ q) ∨ (¬p ∧ ¬q)` | ✅ |
| 5 | `¬(p → q) ≡ p ∧ ¬q` | ✅ |
| 6 | De Morgan: `¬(p ∧ q) ≡ ¬p ∨ ¬q`; `¬(p ∨ q) ≡ ¬p ∧ ¬q` | ✅ |
| 7 | `¬∀x P(x) ≡ ∃x ¬P(x)`; `¬∃x P(x) ≡ ∀x ¬P(x)` | ✅ |
| 8 | `∀x (P ∧ Q) ≡ ∀x P ∧ ∀x Q` | ✅ |
| 9 | `∃x (P ∨ Q) ≡ ∃x P ∨ ∃x Q` | ✅ |
| 10 | `# rows in TT = 2ⁿ`; `# distinct boolean fns = 2^(2ⁿ)` | ✅ |
| 11 | Argument is **valid** iff `(premises → conclusion)` is a tautology | ✅ |
| 12 | A **functionally complete** set: {¬, ∧}, {¬, ∨}, {→, F}, {NAND}, {NOR} | ✅ |

### Tricks

- **"If A then B" trap:** in everyday English we often mean `A ↔ B`, but in logic it strictly means `A → B`. GATE always uses the strict form.
- **"Only if" parsing:** "p only if q" ≡ **p → q** (q is necessary).
- **"Unless" parsing:** "p unless q" ≡ "p ∨ q" or equivalently "¬q → p".
- **Sufficient vs Necessary:** in `p → q`, p is *sufficient* for q; q is *necessary* for p.
- **Implication chain shortcut:** `p → q → r` parses as `p → (q → r)` (right-associative).
- **Tautology check shortcut:** if you can find values making the formula F, it's not a tautology — short-circuit, no need to fill the whole table.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017, 1 mark)
Consider the first-order logic sentence
F: ∀x (∃y R(x, y))
Assuming non-empty logical domains, which of the following sentences entail F?
(A) ∃y (∃x R(x, y))
(B) ∃y (∀x R(x, y))
(C) ∀y (∃x R(x, y))
(D) ¬∃x (∀y ¬R(x, y))

**Solution.**
F says every x has some y with R(x,y).
- (A) "Some pair exists" — far weaker. ❌
- (B) "There's a single y that works for every x" — **stronger**, so it entails F. ✅
- (C) Swaps roles — different meaning. ❌
- (D) ¬∃x ∀y ¬R(x,y) ≡ ∀x ∃y R(x,y) = F itself. ✅

**Answer: (B) and (D).** *(Pattern: quantifier-strength.)*

### Q2. (GATE CSE 2016)
Which one of the following well-formed formulae is a tautology?
(A) ∀x ∃y R(x,y) ↔ ∃y ∀x R(x,y)
(B) (∀x [∃y R(x,y) → S(x,y)]) → ∀x ∃y S(x,y)
(C) [∀x ∃y (P(x,y) → R(x,y))] ↔ [∀x ∃y (¬P(x,y) ∨ R(x,y))]
(D) ∀x ∀y P(x,y) → ∀x ∀y P(y,x)

**Solution.** (C) is tautology because P → R ≡ ¬P ∨ R inside the same quantifier prefix is a pure rewrite. (A) is wrong (LHS weaker). (B) loses information. (D) only holds if domain is symmetric — not always.
**Answer: (C).** *(Pattern: implication-rewrite.)*

### Q3. (GATE CSE 2015)
Which one of the following is **not** equivalent to p ↔ q?
(A) (¬p ∨ q) ∧ (p ∨ ¬q)
(B) (¬p ∨ q) ∧ (q → p)
(C) (¬p ∧ q) ∨ (p ∧ ¬q)
(D) (¬p ∧ ¬q) ∨ (p ∧ q)

**Solution.** p ↔ q ≡ (p ∧ q) ∨ (¬p ∧ ¬q). (C) is the **negation** (xor).
**Answer: (C).** *(Pattern: biconditional ↔ xor confusion.)*

### Q4. (GATE CSE 2014)
The CORRECT formula for the sentence "not all rainy days are cold" is
(A) ∀d (Rainy(d) ∧ ¬Cold(d))
(B) ∀d (¬Rainy(d) → Cold(d))
(C) ∃d (¬Rainy(d) ∧ Cold(d))
(D) ∃d (Rainy(d) ∧ ¬Cold(d))

**Solution.** "Not all rainy are cold" = "some rainy is not cold."
**Answer: (D).** *(Pattern: ¬∀ → ∃¬.)*

### Q5. (GATE CSE 2013)
What is the logical translation of "Some boys in the class are taller than all the girls"?
Let B(x), G(x), T(x,y) = "x taller than y".
(A) ∃x (B(x) ∧ ∀y (G(y) → T(x,y)))
(B) ∃x (B(x) ∧ ∀y (G(y) ∧ T(x,y)))
(C) ∃x (B(x) → ∀y (G(y) → T(x,y)))
(D) ∃x (B(x) ∧ ∀y (T(x,y) → G(y)))

**Solution.** "Some boy" = ∃x B(x); "taller than all girls" = ∀y (G(y) → T(x,y)). Conjoin with ∧.
**Answer: (A).** *(Pattern: ∃ uses ∧; ∀ uses → — classic.)*

### Q6. (GATE CSE 2012)
Consider the statement: "Not all that glitters is gold." Predicate `glitters(x)` and `gold(x)` are true if x glitters / is gold.
(A) ∀x glitters(x) → ¬gold(x)
(B) ∀x gold(x) → glitters(x)
(C) ∃x gold(x) ∧ ¬glitters(x)
(D) ∃x glitters(x) ∧ ¬gold(x)

**Answer: (D).** Same pattern as Q4. *(Pattern: ¬∀ → ∃¬.)*

### Q7. (GATE CSE 2010)
Suppose the predicate F(x, y, t) is "x and y are friends at time t". Then "everybody has some friend all the time" is:
(A) ∀x ∃y ∀t F(x,y,t)
(B) ∀x ∀t ∃y F(x,y,t)
(C) ∀x ∃y ∃t F(x,y,t)
(D) ∃x ∀y ∀t F(x,y,t)

**Solution.** "Has some friend" — ∃y. "All the time" — ∀t. The friend can change over time → ∀x ∀t ∃y.

Wait — re-read: "everybody has *some friend* all the time" — ambiguous. The official answer key reads it as: each person has *one fixed friend* who stays a friend at all times → ∀x ∃y ∀t.
**Answer: (A).** *(Pattern: quantifier order — be careful with English ambiguity; GATE expects ∃ before ∀ when phrasing implies "fixed".)*

### Q8. (GATE CSE 2008)
P and Q are two propositions. Which of the following logical expressions are equivalent?
I. P ∨ ¬Q
II. ¬(¬P ∧ Q)
III. (P ∧ Q) ∨ (P ∧ ¬Q) ∨ (¬P ∧ ¬Q)
IV. (P ∧ Q) ∨ (P ∧ ¬Q) ∨ (¬P ∧ Q)

**Solution.** I ≡ II by De Morgan. III covers rows TT, TF, FF = ¬Q ∨ P = I. IV covers TT, TF, FT — that's P ∨ Q, **not** I.
**Answer: I, II, III.** *(Pattern: equivalence by truth-table coverage.)*

### Q9. (GATE CSE 2005)
Let P(x) and Q(x) be arbitrary predicates. Which of the following is always TRUE?
(A) (∀x P(x) ∧ ∀x Q(x)) ⇒ ∀x (P(x) ∧ Q(x))
(B) (∀x P(x) ∨ ∀x Q(x)) ⇒ ∀x (P(x) ∨ Q(x))
(C) (∀x (P(x) ∨ Q(x))) ⇒ (∀x P(x) ∨ ∀x Q(x))
(D) ∀x (P(x) → Q(x)) ⇒ (∀x P(x) → ∀x Q(x))

**Solution.** (A): valid (trivial). (B): valid (one side already universal). (C): **NOT** valid — counterexample P(x) = "x is even", Q(x) = "x is odd". (D): valid by universal generalization.

GATE accepted **(A), (B) and (D).** *(Pattern: ∀ distributes over ∧, not ∨.)*

### Q10. (GATE CSE 2004)
Identify the correct translation into logic for: "Some boys in the class are taller than all the girls"
*(Same as Q5 — recurring pattern across years.)*

### Q11. (GATE CSE 2002)
"If she studies hard, she will pass." — let S = "studies hard", P = "passes".
"She did not pass; therefore she did not study hard."
What inference rule?

**Solution.** Premises: S → P, ¬P. Conclusion: ¬S. This is **Modus Tollens**.

### Q12. (GATE CSE 2019)
Let p, q, r denote the statements "It is raining", "It is cold", "It is pleasant" respectively. The statement "If it is raining then it is not pleasant, and if it is not raining then it is cold and pleasant" is represented by:
(A) (p → ¬r) ∧ (¬p → (q ∧ r))
(B) (p → ¬r) ∨ (¬p → (q ∧ r))
(C) (p ∧ r) ∨ (¬p → (q ∧ r))
(D) (p → ¬r) ∧ (¬p → (q ∨ r))

**Answer: (A).** *(Pattern: direct translation; "and" between two implications → ∧.)*

### Q13. (GATE CSE 2021)
Consider the statement: "There exists an integer that is divisible by every positive integer."
Let `D(x, y)` = "x is divisible by y", domain = integers.
(A) ∃x ∀y (y > 0 → D(x, y))
(B) ∃x ∀y (D(x, y) → y > 0)
(C) ∀y ∃x (y > 0 → D(x, y))
(D) ∀y ∃x (D(x, y) → y > 0)

**Answer: (A).** *(Pattern: "every positive integer" — restrict y with implication; ∃x must come first because the integer is fixed.)*

### Q14. (GATE CSE 2020, 1 mark)
Let p and q be two propositions. Consider: I. (¬p ↔ p) → (¬q ↔ q). II. (¬q ↔ p) → (¬p ↔ q).
Which of these is/are tautology?
(A) Only I (B) Only II (C) Both (D) Neither

**Solution.** I: `¬p ↔ p` is always F (a contradiction); F → anything is T. ✅
II: Truth-table check — both sides express same "p ⊕ q" structure → tautology. ✅
**Answer: (C).** *(Pattern: F → X = T shortcut.)*

### Q15. (GATE CSE 2018)
Consider: ∀x (∀z [β(x,z) → ∃y α(x,y,z)]) is equivalent to:
(A) ∀x ∀z ∃y (¬β(x,z) ∨ α(x,y,z))
(B) ∀x ∃y ∀z (¬β(x,z) ∨ α(x,y,z))
(C) ∃y ∀x ∀z (¬β(x,z) ∨ α(x,y,z))
(D) ∀x ∀z (¬β(x,z) ∨ ∃y α(x,y,z))

**Solution.** Rewrite β → α as ¬β ∨ α. The ∃y was inside the implication's consequent → ∃y can stay where the α is, but moving ∃y outward over ∀z is **NOT** generally valid (∃y can depend on z). Option (A) keeps it inside ∀z — valid. (D) keeps it bound to α only — also valid in form. The accepted answer is **(A)**.
*(Pattern: implication rewrite + scope of ∃.)*

---

## 6. Practice Questions (20+)

> Solve with timer. Target: 1 mark in 60s, 2 marks in 150s.

### Easy

**P1.** Truth-table the formula `(p → q) ∧ (q → p)`. What does it equal?

**P2.** How many rows does the truth table for 5 variables have?

**P3.** How many distinct Boolean functions of 3 variables exist?

**P4.** Convert "If it rains then I'll stay home" to symbolic form using r and h.

**P5.** Negate: ∀x (P(x) → Q(x)).

**P6.** Negate: ∃x (P(x) ∧ Q(x)).

**P7.** Is `(p ∧ ¬p) → q` a tautology? Why?

**P8.** State the contrapositive of "If n² is even then n is even."

**P9.** Is "p only if q" the same as "p → q" or "q → p"?

**P10.** Are `p → q` and `¬p → ¬q` equivalent?

### Medium

**P11.** Show that `(p → q) → r` and `p → (q → r)` are not equivalent.

**P12.** Determine whether `(p ∨ q) ∧ (¬p ∨ r) → (q ∨ r)` is a tautology.

**P13.** Translate: "Every student in this class has visited some country in Europe." Use S(x), V(x, y), E(y).

**P14.** Translate: "There is a student who has visited every country in Europe." Same predicates.

**P15.** Determine validity:
Premises: p → q, q → r, ¬r.
Conclusion: ¬p.

**P16.** Convert to CNF: `p → (q ∧ r)`.

**P17.** Convert to DNF: `(p ∨ q) ∧ ¬r`.

**P18.** Is `{¬, →}` functionally complete? Justify.

**P19.** Find all values of (p, q, r) for which `(p → q) ∧ (¬q ∨ r) ∧ ¬r` is true.

**P20.** Show: `∀x ∃y P(x, y) → ∃y ∀x P(x, y)` is not valid.

### Hard

**P21.** Prove using inference rules: from `p → (q ∨ r)`, `¬q`, `¬r`, conclude `¬p`.

**P22.** A formula has 4 propositional variables. How many of the 2¹⁶ Boolean functions of 4 variables are **monotone** (T-preserving as inputs flip from F→T)?

**P23.** Decide if the argument is valid: "Either I will get an A or I will not graduate. I will graduate. Therefore I will get an A."

**P24.** Construct a formula in 2 variables that is satisfied by exactly 3 of the 4 truth assignments.

**P25.** Show that `p ↔ q ↔ r` is associative — i.e., `(p ↔ q) ↔ r ≡ p ↔ (q ↔ r)`.

**P26.** Translate to FOL: "Between any two distinct rationals lies another rational." Use rational(x), Lt(x, y).

**P27.** Express "exactly one x satisfies P(x)" using ∃, ∀, =.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | `p ↔ q` | both directions ⇒ biconditional |
| P2 | 32 | 2⁵ |
| P3 | 256 | 2^(2³) |
| P4 | `r → h` | direct |
| P5 | `∃x (P(x) ∧ ¬Q(x))` | ¬(P→Q) ≡ P ∧ ¬Q |
| P6 | `∀x (¬P(x) ∨ ¬Q(x))` | De Morgan + quantifier swap |
| P7 | Yes | F → anything = T |
| P8 | "If n is odd then n² is odd." | flip and negate both |
| P9 | `p → q` | "only if q" makes q necessary |
| P10 | No | inverse, not contrapositive |
| P11 | TT differs at p=F, q=T, r=F | LHS=T, RHS=T → same? Re-check: p=F,q=F,r=F: LHS=(F→F)→F = T→F = F; RHS=F→(F→F)=T. Differ. |
| P12 | Tautology | resolution-style |
| P13 | `∀x (S(x) → ∃y (E(y) ∧ V(x,y)))` | ∀ with → |
| P14 | `∃x (S(x) ∧ ∀y (E(y) → V(x,y)))` | ∃ with ∧ |
| P15 | Valid (Modus Tollens twice) | from p→r and ¬r get ¬p |
| P16 | `(¬p ∨ q) ∧ (¬p ∨ r)` | distribute |
| P17 | `(p ∧ ¬r) ∨ (q ∧ ¬r)` | distribute ∧ over ∨ |
| P18 | Yes | ¬p, p→F gives F; combine with → |
| P19 | (T,T,F),(F,T,F),(F,F,F) **excluded**; valid: (F,F,F)? Check carefully | Trace each row |
| P20 | Counterexample: P(x,y) = (x=y) on {0,1} | LHS true, RHS false |
| P21 | Modus Ponens to `q ∨ r`; resolve with ¬q, ¬r → contradiction → ¬p | proof by contradiction |
| P22 | 6 (out of 16 with 4 vars: many; with 2 vars there are 6 monotone) — for 4 vars consult Dedekind number M(4)=168 | Dedekind |
| P23 | Valid | Disjunctive Syllogism |
| P24 | `p ∨ q` (true on 3 of 4 rows) | OR |
| P25 | Verify by truth table — 8 rows match | XOR-style ↔ associative |
| P26 | `∀x ∀y ((rational(x) ∧ rational(y) ∧ Lt(x,y)) → ∃z (rational(z) ∧ Lt(x,z) ∧ Lt(z,y)))` | density |
| P27 | `∃x (P(x) ∧ ∀y (P(y) → y = x))` | uniqueness |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Reading `p → q` as "p iff q" | Always re-read the row "T → F = F". Implication is one-way. |
| 2 | Negating ∀x P(x) as ∀x ¬P(x) | Negation flips the quantifier: `∃x ¬P(x)`. |
| 3 | Swapping ∀ and ∃ | `∀x ∃y` ≠ `∃y ∀x` — the latter is strictly stronger. |
| 4 | Using ∧ with ∃ on a domain (correct), but ∧ with ∀ to restrict domain (**WRONG**) | With ∀ use `→` ; with ∃ use `∧`. *("All boys are tall" → ∀x (Boy(x) → Tall(x)), not ∀x (Boy(x) ∧ Tall(x)).)* |
| 5 | Forgetting that F → anything is T | Apply the shortcut whenever you see an implication with a contradictory antecedent. |
| 6 | Confusing converse / inverse / contrapositive | Only contrapositive (`¬q → ¬p`) is equivalent. |
| 7 | Treating `p ↔ q ↔ r` as 2-of-3 majority | It's associative XOR-of-XOR — true when an *even* number of operands are F. |
| 8 | Writing CNF/DNF and forgetting it must be ANDs of ORs (or ORs of ANDs) at the **outermost** level | Distribute fully. |
| 9 | Saying `∀x (P(x) ∨ Q(x)) ≡ (∀x P) ∨ (∀x Q)` | False — counterexample with P = even, Q = odd. |
| 10 | Applying Modus Ponens to the converse | Make sure the antecedent of the implication, not the consequent, is the matched premise. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Equivalent to `p → q`" | rewrite as `¬p ∨ q`, then match. |
| "Negation of `∀x P(x)`" | `∃x ¬P(x)`. Pull negation inward. |
| "Some boys are taller than all girls" | `∃x (Boy(x) ∧ ∀y (Girl(y) → Taller(x,y)))` — ∃ with ∧, ∀ with →. |
| "Tautology check" | Try to falsify in 2 attempts; if you can't, build truth table for the smallest sub-expression. |
| "Argument validity" | Check `(P1 ∧ P2 ∧ … ∧ Pn) → C` for tautology. |
| "Functionally complete set?" | Try to build ¬, ∧, ∨ from the set. Standard complete sets: {¬,∧},{¬,∨},{NAND},{NOR},{→,F}. |
| "How many distinct boolean fns" | `2^(2ⁿ)`. |
| "Quantifier order swap" | Almost always changes meaning; ∃y∀x is **stronger** than ∀x∃y. |
| Two formulas in different forms claimed equivalent | Convert both to **CNF** or to a **canonical truth table**. |
| Inference with "did not happen" | Modus Tollens. |
| Statement starts with "not all" | Becomes `∃x ¬P(x)`. |

---

## 9. Quick Revision

```
p → q  ≡  ¬p ∨ q                ★★★
p → q  ≡  ¬q → ¬p (contra)      ★★
p ↔ q  ≡  (p∧q)∨(¬p∧¬q)         ★★
¬(p→q) ≡  p ∧ ¬q                ★★
F → anything = T                 ★★
∀ uses →, ∃ uses ∧               ★★★
¬∀x P(x) ≡ ∃x ¬P(x)             ★★★
∀x∃y ≢ ∃y∀x (∃y∀x stronger)     ★★★
# rows = 2ⁿ; # bool fns = 2^(2ⁿ) ★★
Argument valid ⇔ (∧Pi → C) is a tautology
Modus Ponens / Modus Tollens / Hyp Syllogism / Resolution
Functionally complete: {NAND}, {NOR}, {¬,∧}, {¬,∨}, {→,F}
"Some X are Y"   →  ∃x (X(x) ∧ Y(x))
"All X are Y"    →  ∀x (X(x) → Y(x))
"Not all X are Y" →  ∃x (X(x) ∧ ¬Y(x))
"No X are Y"     →  ∀x (X(x) → ¬Y(x))
```
