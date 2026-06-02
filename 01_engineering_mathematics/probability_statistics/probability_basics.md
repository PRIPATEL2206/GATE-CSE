# Probability Basics & Conditional Probability

> Subject: Engineering Mathematics → Probability & Statistics
> GATE weight: **2–4 marks** every year. Sample space, conditional, independence, Bayes — directly tested.

---

## 1. Concept Explanation

### 1.1 Random Experiment & Sample Space

- **Random experiment:** outcome cannot be predicted with certainty.
- **Sample space S:** set of all possible outcomes.
- **Event:** subset of S.

Example: tossing two coins → S = {HH, HT, TH, TT}. Event "at least one head" = {HH, HT, TH}.

### 1.2 Probability Axioms (Kolmogorov)

For any event A ⊆ S:
1. P(A) ≥ 0
2. P(S) = 1
3. For mutually exclusive A₁, A₂, …: `P(∪Aᵢ) = Σ P(Aᵢ)`

**Consequences:**
- P(∅) = 0
- 0 ≤ P(A) ≤ 1
- P(Aᶜ) = 1 − P(A)
- P(A ∪ B) = P(A) + P(B) − P(A ∩ B)
- P(A ∩ Bᶜ) = P(A) − P(A ∩ B)
- A ⊆ B ⇒ P(A) ≤ P(B)

### 1.3 Equally Likely Outcomes (Classical)

If S has n equally likely outcomes:
`P(A) = (# favorable outcomes) / (# total outcomes) = |A|/|S|`

### 1.4 Inclusion–Exclusion (Probability)

`P(A ∪ B ∪ C) = P(A) + P(B) + P(C) − P(A∩B) − P(B∩C) − P(A∩C) + P(A∩B∩C)`

General: alternating signs.

### 1.5 Conditional Probability

`P(A | B) = P(A ∩ B) / P(B)` (when P(B) > 0).

**Multiplication rule:**
- `P(A ∩ B) = P(A | B) · P(B) = P(B | A) · P(A)`
- General: `P(A₁ ∩ A₂ ∩ … ∩ Aₙ) = P(A₁) · P(A₂|A₁) · P(A₃|A₁∩A₂) · …`

### 1.6 Independence

Events A, B are **independent** iff:
`P(A ∩ B) = P(A) · P(B)`

Equivalently (when P(B) > 0): `P(A | B) = P(A)`.

**Important:** independence ≠ mutually exclusive.
- Mutually exclusive: A ∩ B = ∅, so P(A∩B) = 0 — **dependent** unless one is empty.
- Independence: knowing B happened doesn't change P(A).

**Pairwise vs Mutual Independence:**
- Pairwise: every pair independent.
- Mutually independent: every subset satisfies the product rule.
- Mutual ⇒ pairwise; **converse false**.

### 1.7 Total Probability Theorem

If A₁, A₂, …, Aₙ partition S (disjoint, union = S, P(Aᵢ) > 0), then for any B:

`P(B) = Σᵢ P(B | Aᵢ) · P(Aᵢ)`

### 1.8 Bayes' Theorem

For a partition {A₁, …, Aₙ} of S and event B with P(B) > 0:

`P(Aᵢ | B) = (P(B | Aᵢ) · P(Aᵢ)) / Σⱼ P(B | Aⱼ) · P(Aⱼ)`

**Use:** flip the conditioning. Given evidence B, what's the probability of cause Aᵢ?

### 1.9 Common Patterns

**Drawing from urns:** `P = C(favorable) / C(total)`.

**Sequential events with replacement:** events independent.
**Without replacement:** dependent; use multiplication rule with updated probabilities.

**Birthday problem:** P(at least 2 of n people share a birthday) = 1 − (365 · 364 · … · (365 − n + 1))/365ⁿ.

### 1.10 Set-Theoretic Identities (Probability)

| Identity |
|---|
| P(Aᶜ) = 1 − P(A) |
| P(A ∪ B) = P(A) + P(B) − P(A ∩ B) |
| P(A − B) = P(A) − P(A ∩ B) |
| P(A △ B) = P(A) + P(B) − 2P(A ∩ B) |

### 1.11 Geometric Probability

When sample space is continuous (line, area, volume):
`P = (favorable region size) / (total region size)`

Example: a point thrown uniformly in [0, 1]; P(point < 1/3) = 1/3.

### 1.12 Conditional with Boolean Logic

| If A and B are independent |
|---|
| Aᶜ and B are independent |
| A and Bᶜ are independent |
| Aᶜ and Bᶜ are independent |

> **Summary:** Memorize axioms, conditional formula, multiplication rule, total probability, Bayes. Independence ≠ exclusivity. Most PYQs reduce to a careful application of one of these.

---

## 2. Important Points

- `P(A) + P(Aᶜ) = 1` — always.
- `P(A ∪ B) ≤ P(A) + P(B)` (Boole's inequality).
- For **disjoint** events: `P(A ∪ B) = P(A) + P(B)`.
- For **independent** events: `P(A ∩ B) = P(A) · P(B)`.
- `P(A | B) ≠ P(B | A)` in general (different conditioning).
- **"At least one"** trick: use complement — `P(at least 1) = 1 − P(none)`.
- Independent A, B with P(A) > 0, P(B) > 0 cannot be disjoint.
- Mutually exclusive ⇒ at most one can occur.
- For *n* independent events: `P(none occur) = ∏(1 − pᵢ)`.
- For *n* iid events with prob p: `P(none) = (1 − p)ⁿ`.
- Conditional probability is a probability measure (satisfies axioms).
- **Chain rule** (multiplication rule) used for sequences without replacement.
- Bayes inverts the direction: P(cause | effect) from P(effect | cause).
- For **uniform geometric** problems, ratios of areas / lengths / volumes give probabilities.
- The **prior** P(Aᵢ) and **likelihood** P(B | Aᵢ) combine to give the **posterior** P(Aᵢ | B).

---

## 3. Short Notes

```
AXIOMS
 P(A) ≥ 0
 P(S) = 1
 P(∪disjoint) = Σ P

CONSEQUENCES
 P(∅) = 0; 0 ≤ P ≤ 1
 P(Aᶜ) = 1 − P(A)
 P(A∪B) = P(A) + P(B) − P(A∩B)
 PIE: alternating signs

CLASSICAL
 P(A) = |A| / |S| (equally likely)

CONDITIONAL
 P(A|B) = P(A∩B)/P(B), P(B)>0
 P(A∩B) = P(A|B)·P(B) = P(B|A)·P(A)

INDEPENDENCE
 P(A∩B) = P(A)·P(B)
 ⇔ P(A|B) = P(A)
 mutually exclusive ≠ independent

TOTAL PROB
 partition {Aᵢ}: P(B) = Σ P(B|Aᵢ)·P(Aᵢ)

BAYES
 P(Aᵢ|B) = P(B|Aᵢ)·P(Aᵢ) / Σⱼ P(B|Aⱼ)·P(Aⱼ)

CHAIN RULE
 P(A₁∩...∩Aₙ) = ∏ P(Aᵢ | A₁∩...∩Aᵢ₋₁)

AT LEAST ONE TRICK
 P(≥1) = 1 − P(none)

GEOMETRIC PROB
 P = favorable size / total size

INDEPENDENCE PRESERVATION
 A ⊥ B ⇒ A ⊥ Bᶜ, Aᶜ ⊥ B, Aᶜ ⊥ Bᶜ
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | P(Aᶜ) = 1 − P(A) | ✅✅ |
| 2 | P(A ∪ B) = P(A) + P(B) − P(A ∩ B) | ✅✅ |
| 3 | PIE for 3 events | ✅✅ |
| 4 | P(A | B) = P(A ∩ B) / P(B) | ✅✅✅ |
| 5 | P(A ∩ B) = P(A | B) · P(B) | ✅✅ |
| 6 | Independence: P(A ∩ B) = P(A) · P(B) | ✅✅ |
| 7 | Total prob: P(B) = Σ P(B | Aᵢ) P(Aᵢ) | ✅✅ |
| 8 | Bayes: P(Aᵢ | B) = (likelihood × prior)/evidence | ✅✅✅ |
| 9 | "At least one" complement | ✅ |
| 10 | Geometric probability ratio | ✅ |
| 11 | Chain rule for sequences | ✅ |
| 12 | If A ⊥ B then Aᶜ ⊥ B etc. | ✅ |

### Tricks

- **"At least one":** always try `1 − P(none)` first.
- **Tree diagrams** for sequential / Bayes problems are clearer than equations.
- **Independence test:** check `P(A ∩ B) = P(A)·P(B)`. If unsure, expand carefully.
- **Bayes shortcut** for binary: `P(A|B) = (P(B|A) · P(A)) / (P(B|A) P(A) + P(B|Aᶜ) P(Aᶜ))`.
- **Defective products / disease testing**: classic Bayes setup.
- **For "exactly k of n events":** binomial-like enumeration with PIE.
- **Symmetry trick:** in symmetric setups (e.g., "Alice or Bob wins"), ratios cancel.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Two fair dice are rolled. Probability sum is 7?
**Solution.** Favorable: (1,6),(2,5),(3,4),(4,3),(5,2),(6,1) = 6. Total = 36. P = 6/36 = 1/6.

### Q2. (GATE CSE 2014)
A card drawn from a 52-card deck. Probability red and king?
**Solution.** 2 red kings out of 52 ⇒ 1/26.

### Q3. (GATE CSE 2018)
P(A) = 0.5, P(B) = 0.4, P(A ∩ B) = 0.2. Find P(A | B).
**Solution.** 0.2 / 0.4 = 0.5.

### Q4. (GATE CSE 2008)
A is independent of B. P(A) = 0.4, P(B) = 0.5. P(A ∪ B)?
**Solution.** P(A ∩ B) = 0.4·0.5 = 0.2. P(A ∪ B) = 0.4 + 0.5 − 0.2 = 0.7.

### Q5. (GATE CSE 2010)
Two coins are tossed. Given that at least one is head, probability both are heads?
**Solution.** P(HH | ≥1 H) = (1/4) / (3/4) = 1/3.

### Q6. (GATE CSE 2013)
P(A) = 0.6, P(B) = 0.5, P(A ∩ B) = 0.3. Are A, B independent?
**Solution.** P(A)·P(B) = 0.3 = P(A∩B) ⇒ Yes.

### Q7. (GATE CSE 2015)
Probability a randomly chosen 3-digit number is divisible by 5?
**Solution.** Divisible by 5: ends in 0 or 5. Total 3-digit numbers: 900 (100–999). Favorable: 180. P = 180/900 = 1/5.

### Q8. (GATE CSE 2007)
A box contains 5 red, 4 blue balls. Two drawn without replacement. P(both red)?
**Solution.** (5/9)·(4/8) = 20/72 = 5/18.

### Q9. (GATE CSE 2019)
A test is 95% accurate. Disease prevalence 1%. Person tests positive. What's the probability they have the disease?
**Solution.** Bayes:
P(D|+) = (0.95·0.01)/(0.95·0.01 + 0.05·0.99) = 0.0095/(0.0095 + 0.0495) ≈ 0.161 ≈ 16.1%.

### Q10. (GATE CSE 2009)
Three machines produce 50%, 30%, 20% of items. Defect rates: 1%, 2%, 4%. Probability random item is defective?
**Solution.** Total prob: 0.5·0.01 + 0.3·0.02 + 0.2·0.04 = 0.005 + 0.006 + 0.008 = 0.019.

### Q11. (GATE CSE 2003)
A point is chosen uniformly in a unit square. Probability x + y > 1?
**Solution.** Area of region = 1/2.

### Q12. (GATE CSE 2011)
A coin is tossed until first head. Probability needs more than 3 tosses?
**Solution.** = P(first 3 tails) = (1/2)³ = 1/8.

### Q13. (GATE CSE 2020)
P(A) = 0.7, P(A ∩ B) = 0.4. Find P(B | A).
**Solution.** 0.4 / 0.7 = 4/7.

### Q14. (GATE CSE 2016)
A bag has 4 red, 6 white, and 5 black balls. Three drawn without replacement. P(all white)?
**Solution.** C(6,3)/C(15,3) = 20/455 = 4/91.

### Q15. (GATE CSE 2021)
P(A) = 1/3, P(B) = 2/3, P(A ∩ B) = 1/4. Find P(A | Bᶜ).
**Solution.** P(Bᶜ) = 1/3; P(A ∩ Bᶜ) = 1/3 − 1/4 = 1/12; P(A|Bᶜ) = (1/12)/(1/3) = 1/4.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Roll a fair die. P(even number)?

**P2.** Two coins tossed. P(at least one head)?

**P3.** P(A) = 0.3, P(B) = 0.4, A ∩ B = ∅. P(A ∪ B)?

**P4.** P(A) = 0.5. P(Aᶜ)?

**P5.** Card from a deck. P(face card)?

**P6.** Two dice. P(sum = 4)?

**P7.** Ball drawn from urn 3 red 2 blue 5 white. P(blue)?

**P8.** A is sure. P(A)?

**P9.** P(A ∪ B) = 0.7, P(A) = 0.5, P(B) = 0.4. P(A ∩ B)?

**P10.** Are mutually exclusive events independent (in general)?

### Medium

**P11.** Bag: 3R, 5B. Draw two without replacement. P(both red).

**P12.** Bag: 3R, 5B. Draw two with replacement. P(one of each color in either order).

**P13.** Three independent events with probs 0.2, 0.3, 0.4. P(none occur).

**P14.** Three independent events probs 0.2, 0.3, 0.4. P(at least one).

**P15.** Four students each have 0.7 probability of solving a problem. P(at least one solves)?

**P16.** P(A | B) = 0.5, P(B) = 0.4. P(A ∩ B)?

**P17.** Box 1 has 2R 3B, Box 2 has 4R 1B. Box chosen at random; ball drawn. P(red)?

**P18.** In Q17, given red, P(from Box 2)?

**P19.** A coin is tossed 5 times. P(exactly 3 heads)?

**P20.** A point chosen uniformly in [0, 2]². P(x² + y² ≤ 1)?

### Hard

**P21.** Birthday problem: in a group of 23, P(at least two share a birthday)?

**P22.** A fair coin tossed until 2 heads. Expected # tosses?

**P23.** Three urns: U1 with 2R 1B, U2 with 1R 2B, U3 with 3R. An urn picked uniformly; ball drawn red. P(from U1)?

**P24.** Among 100 students, 30 take Math, 40 Physics, 20 both. Random student. P(neither)?

**P25.** Three students given a problem. Probabilities of solving: 1/2, 1/3, 1/4 independently. P(only one solves)?

**P26.** 10 people enter a raffle independently with P = 0.1 each. P(exactly 2 win)?

**P27.** A point inside a square of side 2. P(it's within distance 1 from a corner)?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 1/2 | 3/6 |
| P2 | 3/4 | 1 − 1/4 |
| P3 | 0.7 | additive |
| P4 | 0.5 | complement |
| P5 | 12/52 = 3/13 | 12 face cards |
| P6 | 3/36 = 1/12 | (1,3),(2,2),(3,1) |
| P7 | 2/10 = 1/5 | direct |
| P8 | 1 | certain event |
| P9 | 0.2 | inclusion-exclusion |
| P10 | No | mutually exclusive ⇒ dependent if both > 0 |
| P11 | 3/28 | (3/8)(2/7) |
| P12 | 2 · (3/8)(5/8) = 15/32 | with replacement |
| P13 | (0.8)(0.7)(0.6) = 0.336 | none |
| P14 | 1 − 0.336 = 0.664 | complement |
| P15 | 1 − (0.3)⁴ = 1 − 0.0081 = 0.9919 | complement |
| P16 | 0.2 | direct |
| P17 | (1/2)(2/5) + (1/2)(4/5) = 3/5 | total prob |
| P18 | (4/10)/(6/10) = 2/3 | Bayes |
| P19 | C(5,3)·(1/2)⁵ = 10/32 = 5/16 | binomial |
| P20 | π/16 ≈ 0.196 (quarter circle in [0,2]²) | area ratio = π/4 in [0,1]², scaled |
| P21 | ≈ 0.507 | 1 − 365!/(342! · 365²³) |
| P22 | 4 | NB(2, 1/2): mean = 2/p = 4 |
| P23 | (1/3)(2/3) / [(1/3)(2/3 + 1/3 + 1)] = (2/9)/(6/9) = 1/3 | Bayes; total prob denom = (2/9 + 1/9 + 3/9) = 6/9 |
| P24 | (100 − 30 − 40 + 20)/100 = 50/100 = 1/2 | PIE |
| P25 | sum over each "only one"|: (1/2)(2/3)(3/4) + (1/2)(1/3)(3/4) + (1/2)(2/3)(1/4) | = 1/4 + 1/8 + 1/12 = 11/24 |
| P26 | C(10,2)·(0.1)²·(0.9)⁸ ≈ 0.1937 | binomial |
| P27 | Quarter circles at each corner = π/4 union; total area where union excluding overlaps... approximate ≈ π/4 ≈ 0.785 (assuming corners don't overlap) | geometric prob |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing independent and mutually exclusive | They're often opposites! |
| 2 | Forgetting that conditional probability is in [0, 1] | Same axioms apply. |
| 3 | Adding probabilities without checking disjointness | Use PIE if events overlap. |
| 4 | Bayes denominator omitting a partition | Use total probability for denominator. |
| 5 | Treating P(A|B) = P(B|A) | They're different. |
| 6 | "At least one" without complement | Almost always faster via complement. |
| 7 | Using replacement when problem says "without" | Rewrite each probability after the previous draw. |
| 8 | Pairwise independence implying mutual | Pairwise ≠ mutual. |
| 9 | Counting outcomes ignoring order when it matters | Permutations vs combinations. |
| 10 | Forgetting that conditional changes the sample space | Condition on event B → restrict to B. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "At least one of n events" | 1 − P(none). |
| "Exactly k of n independent events" | Binomial. |
| "Given X, find P(Y)" | Conditional or Bayes. |
| "Total probability of an event" | Total probability theorem (partition). |
| "Defect / disease / signal source" | Bayes. |
| "Two independent events" | Multiply probs. |
| "Drawing without replacement" | Multiplication rule with updated counts. |
| "Probability of a region" | Geometric probability (ratio of areas). |
| "Symmetric setup" | Often probability = 1/n by symmetry. |
| "Birthday-like collision" | 1 − ∏(1 − k/N). |

---

## 9. Quick Revision

```
AXIOMS
 P ≥ 0, P(S) = 1, σ-additivity

P(Aᶜ) = 1 − P(A)
P(A ∪ B) = P(A) + P(B) − P(A ∩ B)
PIE for 3: Σ P − Σ P(pairs) + P(triple)

CLASSICAL: P = |A|/|S|

CONDITIONAL: P(A|B) = P(A∩B)/P(B)
MULT: P(A∩B) = P(A|B)·P(B)
INDEPENDENT: P(A∩B) = P(A)·P(B)
mutually excl ≠ independent

TOTAL PROB: P(B) = Σ P(B|Aᵢ)·P(Aᵢ)
BAYES: P(Aᵢ|B) = (P(B|Aᵢ)·P(Aᵢ))/Σ ...

AT LEAST ONE: 1 − P(none)
N IID with prob p: P(none) = (1−p)ⁿ

INDEPENDENCE PRESERVATION
 A ⊥ B ⇒ A ⊥ Bᶜ, Aᶜ ⊥ B, Aᶜ ⊥ Bᶜ

GEOMETRIC P = favorable / total area

CHAIN RULE
 P(A₁∩…∩Aₙ) = ∏ P(Aᵢ | A₁∩…∩Aᵢ₋₁)
```
