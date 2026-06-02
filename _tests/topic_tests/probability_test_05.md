# Topic Test 05 — Probability & Statistics (Basics · Distributions · Bayes/Stats)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Two fair dice rolled. P(sum = 8)?
(A) 5/36  (B) 1/6  (C) 6/36  (D) 1/9

**Q2.** [MCQ] P(A) = 0.6, P(B) = 0.5, P(A ∩ B) = 0.3. Are A, B independent?
(A) Yes  (B) No  (C) Cannot tell  (D) Mutually exclusive

**Q3.** [MCQ] P(A) = 0.4, P(B|A) = 0.5. P(A ∩ B)?
(A) 0.2  (B) 0.5  (C) 0.4  (D) 0.9

**Q4.** [MCQ] X ~ Bin(10, 0.5). E[X]?
(A) 2.5  (B) 5  (C) 10  (D) 0.5

**Q5.** [MCQ] X ~ Bin(10, 0.5). Var(X)?
(A) 2.5  (B) 5  (C) 10  (D) 1.25

**Q6.** [MCQ] X ~ Poisson(λ=2). P(X = 0)?
(A) 1  (B) 0  (C) e⁻²  (D) e²

**Q7.** [NAT] X ~ Uniform(0, 6). E[X] = `____`

**Q8.** [MCQ] X ~ Exp(λ=2). E[X]?
(A) 0.5  (B) 1  (C) 2  (D) 4

**Q9.** [MCQ] Memoryless property holds for:
(A) Binomial  (B) Poisson  (C) Geometric & Exponential  (D) Normal

**Q10.** [MCQ] X ~ N(0, 1). P(X > 0)?
(A) 0  (B) 0.25  (C) 0.5  (D) 1

**Q11.** [MCQ] If X ⊥ Y and Var(X) = 4, Var(Y) = 9, Var(X + Y) = ?
(A) 13  (B) 5  (C) √13  (D) 36

**Q12.** [MCQ] Cov(X, Y) for indep X, Y is:
(A) σ_X · σ_Y  (B) 0  (C) 1  (D) Var(X) + Var(Y)

**Q13.** [NAT] X ~ Bin(50, 0.4). E[X²] = `____`

**Q14.** [MCQ] By CLT, X̄ for n=100, σ²=25, μ=10 is approximately:
(A) N(10, 25)  (B) N(10, 0.25)  (C) N(10, 0.5)  (D) N(100, 25)

**Q15.** [MCQ] A test 95% accurate; disease prevalence 1%. Person tests positive. P(disease) ≈
(A) 95%  (B) 50%  (C) 16%  (D) 1%

---

## Section B — 2 marks each

**Q16.** [MCQ] Bag has 4R, 6B. Two drawn without replacement. P(both red)?
(A) 4/25  (B) 6/45 = 2/15  (C) 12/90 = 2/15  (D) 16/100

**Q17.** [NAT] At least one head in 4 tosses of fair coin (probability) = `____`

**Q18.** [MCQ] X ~ N(50, 16). P(X > 58) ≈
(A) 0.5  (B) 0.16  (C) 0.023  (D) 0.84

**Q19.** [MCQ] For Cov(X,Y) = 3, σ_X = 2, σ_Y = 5, ρ?
(A) 0.3  (B) 0.6  (C) 1.5  (D) 0.15

**Q20.** [MCQ] Three machines produce 50%, 30%, 20% of items. Defect rates 1%, 2%, 4%. Probability random item is defective?
(A) 1.5%  (B) 1.9%  (C) 2.5%  (D) 7%

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (A) 5/36 | (2,6),(3,5),(4,4),(5,3),(6,2) |
| 2 | (A) Yes | 0.6·0.5 = 0.3 ✓ |
| 3 | (A) 0.2 | P(A∩B) = P(B|A)·P(A) |
| 4 | (B) 5 | np |
| 5 | (A) 2.5 | np(1−p) |
| 6 | (C) e⁻² | Poisson PMF |
| 7 | 3 | (a+b)/2 |
| 8 | (A) 0.5 | 1/λ |
| 9 | (C) | only Geom and Exp |
| 10 | (C) 0.5 | symmetry |
| 11 | (A) 13 | indep |
| 12 | (B) 0 | indep ⇒ Cov = 0 |
| 13 | 156 | Var = np(1−p) = 12; (np)² = 400; E[X²] = 12 + 400 = 412. *Recompute*: np = 20, np(1−p) = 12; E[X²] = Var + (E[X])² = 12 + 400 = **412** |
| 14 | (B) | σ²/n = 25/100 = 0.25 |
| 15 | (C) 16% | 0.95·0.01/(0.95·0.01 + 0.05·0.99) ≈ 0.0095/0.0590 ≈ 0.161 |
| 16 | (C) 2/15 | (4/10)(3/9) = 12/90 |
| 17 | 0.9375 | 1 − (1/2)⁴ = 15/16 |
| 18 | (C) | Z = 8/4 = 2; P(Z > 2) ≈ 0.023 |
| 19 | (A) 0.3 | 3/10 |
| 20 | (B) 1.9% | 0.5·0.01 + 0.3·0.02 + 0.2·0.04 = 0.019 |

> **Note on Q13:** the correct numerical answer is **412** (not 156). Score against the working.

---

## Score Sheet

| | Score |
|---|---|
| Section A (15 × 1) | _ /15 |
| Section B (5 × 2)  | _ /10 |
| **Total**          | _ /25 |
| Time used          | _ min |

**Targets:**
- ≥ 22/25 in 25 min → mastery
- 18–21 → revise short notes + pattern recognition
- < 18 → re-do PYQs of all three probability topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
