# Mean, Variance, Bayes & Statistics

> Subject: Engineering Mathematics → Probability & Statistics
> GATE weight: **2–3 marks** every year. Sample statistics, estimation, Bayes (deep), CLT, hypothesis testing basics.

---

## 1. Concept Explanation

### 1.1 Population vs Sample

- **Population:** entire collection of items of interest. Parameters (μ, σ²) are fixed (often unknown).
- **Sample:** subset of population. Statistics (x̄, s²) are random (computed from sample).

### 1.2 Sample Mean & Variance

For a sample x₁, x₂, …, xₙ:

**Sample mean:** `x̄ = (1/n) Σ xᵢ`.

**Sample variance:** `s² = (1/(n − 1)) Σ (xᵢ − x̄)²`.

(Divide by n−1 for **unbiased** estimator; by n is the *biased* maximum-likelihood version.)

**Sample standard deviation:** `s = √s²`.

### 1.3 Properties of Sample Statistics

If X₁, …, Xₙ are iid with mean μ, variance σ²:

| Quantity | E | Var |
|---|---|---|
| X̄ (sample mean) | μ | σ²/n |
| S² (sample variance, n−1 denom) | σ² | — |
| nX̄ | nμ | nσ² |

**Standard error of mean:** `SE = σ/√n`.

### 1.4 Expectation Properties (Recap & Extend)

| Rule | Form |
|---|---|
| Linearity (always) | E[aX + bY + c] = aE[X] + bE[Y] + c |
| LOTUS | E[g(X)] = Σ g(x)p(x) or ∫ |
| Tower / Iterated | E[X] = E[E[X | Y]] |
| For independent X, Y | E[XY] = E[X]·E[Y] |
| Indicator | E[1_A] = P(A) |

### 1.5 Variance Properties (Recap & Extend)

| Rule | Form |
|---|---|
| Var = E[X²] − (E[X])² | always |
| Var(c) = 0 | constant |
| Var(aX + b) = a² Var(X) | shift/scale |
| Var(X + Y) = Var(X) + Var(Y) + 2Cov(X,Y) | general |
| Independence ⇒ Cov = 0 | sufficient |
| Var(X − Y) = Var(X) + Var(Y) − 2Cov(X,Y) | difference |
| Var of sum of n iid: nσ² | iid |
| Var of mean of n iid: σ²/n | iid |

### 1.6 Covariance & Correlation

`Cov(X, Y) = E[XY] − E[X]·E[Y]`

| Property |
|---|
| Cov(X, X) = Var(X) |
| Cov(aX + b, cY + d) = ac · Cov(X, Y) |
| Cov(X, Y + Z) = Cov(X,Y) + Cov(X,Z) |
| Independent ⇒ Cov = 0 (converse false) |
| ρ = Cov/(σ_X σ_Y) ∈ [−1, 1] |
| ρ = ±1 iff Y = aX + b (perfect linear) |

### 1.7 Bayes' Theorem (deep dive)

`P(Aᵢ | B) = P(B | Aᵢ) P(Aᵢ) / Σⱼ P(B | Aⱼ) P(Aⱼ)`

| Term | Name |
|---|---|
| P(Aᵢ) | Prior |
| P(B | Aᵢ) | Likelihood |
| P(Aᵢ | B) | Posterior |
| Σⱼ P(B | Aⱼ) P(Aⱼ) | Evidence (normalization) |

**Bayes for continuous parameters:**
`f(θ | data) ∝ f(data | θ) · f(θ)`

### 1.8 Law of Large Numbers (LLN)

For iid X₁, X₂, … with mean μ:
`X̄ₙ → μ` as n → ∞ (in probability / almost surely).

**Implication:** sample mean converges to population mean.

### 1.9 Central Limit Theorem (CLT)

For iid X₁, …, Xₙ with mean μ and variance σ² (finite):

`(X̄ − μ)/(σ/√n) → N(0, 1)` as n → ∞.

**Use:** for large n (typically n ≥ 30), sample mean is approximately Normal regardless of distribution.

### 1.10 Hypothesis Testing (basics)

- **H₀:** null hypothesis (status quo).
- **H₁:** alternative.
- **Test statistic:** computed from sample (e.g., z, t).
- **p-value:** P(observe statistic as extreme | H₀).
- Reject H₀ if p < α (significance level, often 0.05).

**Errors:**
- **Type I (α):** reject H₀ when true.
- **Type II (β):** fail to reject H₀ when false.
- **Power:** 1 − β.

### 1.11 Confidence Interval (essentials)

For sample mean (large n): `x̄ ± z_(α/2) · σ/√n`.

For unknown σ (Student's t): `x̄ ± t_(α/2, n−1) · s/√n`.

### 1.12 Estimators

- **Bias:** Bias(θ̂) = E[θ̂] − θ.
- **Unbiased:** Bias = 0.
- **Consistent:** θ̂ₙ → θ as n → ∞.
- **MLE (Maximum Likelihood Estimate):** maximizes likelihood L(θ; data).
- **MSE:** E[(θ̂ − θ)²] = Var(θ̂) + Bias².

### 1.13 Common Tests (overview)

| Test | When |
|---|---|
| Z-test | known σ, large n |
| t-test | unknown σ, small n |
| Chi-squared | goodness of fit, variance |
| F-test | comparing variances |

### 1.14 Tower Property / Conditional Expectation

`E[E[X | Y]] = E[X]`

`Var(X) = E[Var(X | Y)] + Var(E[X | Y])` (law of total variance).

> **Summary:** Memorize sample mean/variance formulas, expectation linearity, variance addition with independence, Bayes (deep), CLT. Recognize when to use t vs z. Master the tower/iterated expectation for composite RVs.

---

## 2. Important Points

- **Sample variance uses n − 1**, not n (Bessel's correction → unbiased).
- For **iid sum**, Var(Sₙ) = nσ²; for sample mean Var = σ²/n.
- **Standard error** decreases as 1/√n — diminishing returns.
- E[X+Y] = E[X] + E[Y] **always**, regardless of independence.
- Cov(X, Y) = 0 doesn't imply independence in general.
- **CLT** requires finite mean and variance.
- **Bayes:** prior · likelihood / evidence — normalize by total probability.
- **Indicator trick:** E[# of events] = Σ P(event) — even when events overlap.
- **Tower property:** condition on a partition Y, then average.
- For Bernoulli sum (Binomial), `E[XY] = E[X²]` if X = Y, but otherwise need joint distribution.
- For uniform ordered statistics: E[X₍ₖ₎] = k/(n+1) for U[0,1].
- The MSE of sample mean for iid is σ²/n (unbiased).
- **Markov / Chebyshev** give bounds without knowing the full distribution.

---

## 3. Short Notes

```
SAMPLE STATS (n samples)
 sample mean: x̄ = (1/n) Σ xᵢ
 sample var: s² = (1/(n−1)) Σ (xᵢ − x̄)²
 SE = σ/√n

ESTIMATOR PROPS
 unbiased: E[θ̂] = θ
 consistent: θ̂ₙ → θ
 MSE = Var + Bias²

EXPECTATION
 linear (always)
 LOTUS: E[g(X)] = Σ g·p
 indep: E[XY] = E[X]E[Y]
 indicator: E[1_A] = P(A)
 tower: E[E[X|Y]] = E[X]

VARIANCE
 Var = E[X²] − μ²
 Var(aX+b) = a² Var
 Var(X+Y) = Var(X)+Var(Y)+2Cov
 indep: Cov = 0; Var sums
 Var of mean of iid n: σ²/n
 law of total var: Var = E[Var(X|Y)] + Var(E[X|Y])

COVARIANCE
 Cov = E[XY] − E[X]E[Y]
 Cov(X,X) = Var(X)
 Cov(aX, cY) = ac Cov
 ρ = Cov/(σXσY) ∈ [−1,1]
 ρ = ±1 ⇔ linear

BAYES
 posterior ∝ likelihood × prior
 P(Aᵢ|B) = P(B|Aᵢ)·P(Aᵢ) / Σ P(B|Aⱼ)·P(Aⱼ)
 continuous: f(θ|data) ∝ f(data|θ)·f(θ)

LLN: X̄ₙ → μ
CLT: (X̄−μ)/(σ/√n) → N(0,1)

HYPOTHESIS TESTING
 H₀, H₁
 type I (α): reject true H₀
 type II (β): accept false H₀
 power = 1 − β
 p-value < α ⇒ reject H₀

CONFIDENCE INTERVAL
 known σ: x̄ ± z·σ/√n
 unknown σ: x̄ ± t·s/√n

INEQUALITIES
 Markov (X≥0): P(X≥a) ≤ E/a
 Chebyshev: P(|X−μ|≥kσ) ≤ 1/k²
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | x̄ = (1/n) Σ xᵢ | ✅✅ |
| 2 | s² = (1/(n−1)) Σ (xᵢ − x̄)² | ✅✅ |
| 3 | Var(X̄) = σ²/n | ✅✅ |
| 4 | Cov(X, Y) = E[XY] − E[X]E[Y] | ✅✅ |
| 5 | ρ = Cov/(σXσY); ∈ [−1, 1] | ✅✅ |
| 6 | Bayes: posterior ∝ likelihood × prior | ✅✅✅ |
| 7 | Tower: E[X] = E[E[X|Y]] | ✅ |
| 8 | Total Var: Var(X) = E[Var(X|Y)] + Var(E[X|Y]) | ✅ |
| 9 | CLT: X̄ ≈ N(μ, σ²/n) for large n | ✅✅ |
| 10 | Markov, Chebyshev | ✅ |
| 11 | LLN: X̄ → μ | ✅ |
| 12 | Indicator: E[Σ 1_A] = Σ P(A) | ✅ |
| 13 | MSE = Var(θ̂) + Bias² | ✅ |

### Tricks

- **Indicator decomposition:** for "expected number of X" problems, write as sum of indicator vars.
- **Tower for nested random:** condition on outer, take expectation, then re-take.
- **Bayes table** (2×2): organize as P(B|A) P(A) and P(B|Aᶜ) P(Aᶜ); divide by sum.
- **CLT for Binomial:** Bin(n, p) ≈ N(np, np(1−p)) for n large.
- **For ratios of iid:** use symmetry — e.g., P(X < Y) for iid continuous = 1/2.
- **MSE shortcut:** for unbiased estimator, MSE = Var.
- **Covariance bilinearity:** decompose Cov(aX + bY, cZ + dW) into 4 terms.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A coin is biased: P(H) = 0.6. Tossed 100 times. Expected # heads and variance?
**Solution.** E = 60, Var = 100·0.6·0.4 = 24.

### Q2. (GATE CSE 2014)
A test for a disease has 99% accuracy. Disease prevalence 0.1%. Person tests positive. P(disease)?
**Solution.** Bayes: 0.99·0.001/(0.99·0.001 + 0.01·0.999) ≈ 0.099 (about 9.9%).

### Q3. (GATE CSE 2018)
X uniform on [0,1]. Y = X². E[Y] and Var(Y)?
**Solution.** E[Y] = ∫_0^1 x² dx = 1/3. E[Y²] = ∫_0^1 x⁴ dx = 1/5. Var = 1/5 − 1/9 = 4/45.

### Q4. (GATE CSE 2015)
X, Y iid ~ Uniform[0,1]. P(X + Y < 1)?
**Solution.** Triangle area in unit square: 1/2.

### Q5. (GATE CSE 2008)
Cov(X, X) = ?
**Solution.** Var(X).

### Q6. (GATE CSE 2010)
A sample of 16 has mean 50, std dev 8. 95% CI for population mean (assume σ known)?
**Solution.** 50 ± 1.96·8/√16 = 50 ± 3.92.

### Q7. (GATE CSE 2013)
Two iid Bin(n, p). E[X · Y]?
**Solution.** Independent ⇒ E[XY] = E[X]·E[Y] = (np)².

### Q8. (GATE CSE 2009)
Bag has 4 white, 6 black. Two drawn without replacement. X = # white. E[X]?
**Solution.** Linearity using indicators: E[X] = 2·(4/10) = 4/5 = 0.8.

### Q9. (GATE CSE 2003)
A random variable has Var = 4. Var(2X + 3) = ?
**Solution.** 4·4 = 16.

### Q10. (GATE CSE 2019)
Roll a fair die n times. X̄ → ? as n → ∞.
**Solution.** E[X] = 3.5 (LLN).

### Q11. (GATE CSE 2007)
Roll a fair die. X = score. Sample mean of 100 rolls. Approximate distribution?
**Solution.** N(3.5, σ²/100) where σ² = 35/12. So N(3.5, 35/1200).

### Q12. (GATE CSE 2020)
Indicator-method: in n bit binary strings, expected # positions where bit is 1 (uniformly random)?
**Solution.** n · 1/2 = n/2.

### Q13. (GATE CSE 2021)
X ~ Bin(n, p). Var(X/n)?
**Solution.** (1/n²)·np(1−p) = p(1−p)/n.

### Q14. (GATE CSE 2011)
Two unbiased coins. X = # heads, Y = # tails. Cov(X, Y)?
**Solution.** Y = 2 − X. Cov(X, 2 − X) = −Var(X) = −(2·0.5·0.5) = −0.5.

### Q15. (GATE CSE 2016)
A jar has 3 red, 7 blue balls. n balls drawn without replacement, X = # red. E[X]?
**Solution.** E = n·(3/10) = 3n/10.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Sample {2, 4, 6, 8}. Mean and variance (n−1 denom).

**P2.** State linearity of expectation.

**P3.** State variance of sum (independent case).

**P4.** Compute Cov(X, X) for X ~ Bin(n, p).

**P5.** Sample size n = 100, σ = 10. SE of mean?

**P6.** Var(2X − 3Y) when X, Y independent, Var = 4 and 9 respectively?

**P7.** Bayes scenario: P(A) = 0.3, P(B|A) = 0.8, P(B|Aᶜ) = 0.2. P(B)?

**P8.** Same as P7. P(A | B)?

**P9.** Var(X̄) for n = 25, σ = 5?

**P10.** State CLT in one sentence.

### Medium

**P11.** A fair coin tossed 100 times. Approximate P(# heads > 60).

**P12.** X uniform[0, 4]. Y = X − 1. E[Y], Var(Y).

**P13.** A fair die rolled 5 times. E[number of sixes]?

**P14.** A bag has 3 red, 5 blue, 2 green. Random draw with replacement, 4 times. E[# reds]?

**P15.** Cov(aX + b, cY + d).

**P16.** Two iid N(0, 1). Distribution of X + Y, X − Y?

**P17.** A coin biased P(H) = 0.4. P(at least 1 head in 5 tosses)?

**P18.** Cov(X, Y) = 2, Var(X) = 4, Var(Y) = 9. ρ?

**P19.** X ~ Bin(10, 0.5). Approximate by Normal: P(X ≤ 3)?

**P20.** Use indicator method to find E[# common elements in two random subsets of size k from {1,…,n}].

### Hard

**P21.** X ~ Geom(p). Verify memoryless: P(X > m + n | X > m) = P(X > n).

**P22.** Tower property example: N ~ Poisson(λ); given N, X | N ~ Bin(N, p). Find E[X], Var(X).

**P23.** Two iid Exp(λ). E[max(X, Y)].

**P24.** A sample of size 25 has mean 100, sample std 10. 95% CI (use t with df = 24, t ≈ 2.064).

**P25.** Var(X̄) − Var(X) — relate to n.

**P26.** Show E[X²] ≥ (E[X])² (variance ≥ 0).

**P27.** An urn has K white balls and N − K black. n balls drawn without replacement. Distribution of X = # white?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | mean = 5, var = 20/3 | (4 + 0 + 1 + 9)/3 wait recompute (xᵢ−5)² = 9,1,1,9 → 20/3 |
| P2 | as in 1.4 | direct |
| P3 | Var(X+Y) = Var(X)+Var(Y) | direct |
| P4 | np(1−p) | Var(X) |
| P5 | 1 | 10/√100 |
| P6 | 4·4 + 9·9 = 16 + 81 = 97 | indep |
| P7 | 0.3·0.8 + 0.7·0.2 = 0.38 | total prob |
| P8 | 0.24/0.38 ≈ 0.632 | Bayes |
| P9 | 1 | 25/25 |
| P10 | "Sample mean is approximately Normal for large n" | direct |
| P11 | Z = (60 − 50)/5 = 2; P(X > 60) ≈ 0.023 (use cont. correction Z = 10.5/5 ≈ 2.1) | Normal approx |
| P12 | E = 1, Var = 16/12 = 4/3 | shift |
| P13 | 5/6 | linearity |
| P14 | 4 · 0.3 = 1.2 | linearity |
| P15 | ac · Cov(X,Y) | bilinearity |
| P16 | both N(0, 2) | sum/diff of indep Normals |
| P17 | 1 − (0.6)⁵ = 1 − 0.07776 ≈ 0.922 | complement |
| P18 | 2/(2·3) = 1/3 | direct |
| P19 | Z = (3.5−5)/√2.5 = −0.949; P ≈ 0.171 | normal with cont correction |
| P20 | Σ P(i in both) = n · (k/n)² = k²/n | indicator |
| P21 | direct calc | memoryless |
| P22 | E = λp; Var = λp + (something via tower) | tower |
| P23 | 3/(2λ) | E[max] = E[X] + E[Y] − E[min]; min ~ Exp(2λ), E = 1/(2λ); so max = 1/λ + 1/λ − 1/(2λ) = 3/(2λ) |
| P24 | 100 ± 2.064·10/5 = 100 ± 4.128 | t-CI |
| P25 | Var(X̄) = Var(X)/n | iid |
| P26 | Var(X) = E[X²] − (E[X])² ≥ 0 | direct |
| P27 | Hypergeometric | C(K,k)C(N−K,n−k)/C(N,n) |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Using n instead of n−1 in sample variance | n−1 for unbiased. |
| 2 | Treating sample mean as the population mean | Sample is a random estimate. |
| 3 | Forgetting Var(X̄) = σ²/n (not σ/n) | Variance scales with 1/n; SE with 1/√n. |
| 4 | Bayes denominator missing terms | Always include all partition members. |
| 5 | Using CLT for n < 30 | Borderline; check distribution. |
| 6 | Treating Cov = 0 as independence | Implication only one way. |
| 7 | Mixing z and t intervals | z when σ known, t when only s known. |
| 8 | Type I and Type II errors swapped | I = false reject; II = false accept. |
| 9 | Forgetting bias in MSE | MSE = Var + Bias². |
| 10 | Using law of total variance incorrectly | Var(X) = E[Var(X|Y)] + Var(E[X|Y]). |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Sample mean / SE" | x̄ = Σ/n; SE = σ/√n. |
| "Posterior probability" | Bayes. |
| "Disease test / defect / signal source" | Bayes table. |
| "Expected number of …" | Indicator method + linearity. |
| "Approximate Binomial for large n" | Normal (or Poisson if p small). |
| "CLT problem" | X̄ ≈ N(μ, σ²/n). |
| "Confidence interval" | x̄ ± z·SE (or t·SE). |
| "Hypothesis test, large n, σ known" | z-test. |
| "Hypothesis test, small n, σ unknown" | t-test. |
| "Compound RV: N first, then Y depends on N" | Tower property. |

---

## 9. Quick Revision

```
SAMPLE STATS
 x̄ = Σ/n
 s² = Σ(xᵢ−x̄)²/(n−1)
 SE = σ/√n

EXPECTATION
 linear
 indicator: E[1_A] = P(A)
 tower: E[X] = E[E[X|Y]]
 indep: E[XY] = E[X]E[Y]

VARIANCE
 Var = E[X²] − μ²
 Var(aX+b) = a² Var
 Var(X+Y) = VarX + VarY + 2Cov
 indep ⇒ Cov = 0
 iid sum: nσ²; mean: σ²/n

COVARIANCE / CORR
 Cov = E[XY] − E[X]E[Y]
 ρ = Cov/(σXσY) ∈ [−1,1]

BAYES
 P(Aᵢ|B) = P(B|Aᵢ)P(Aᵢ) / Σⱼ P(B|Aⱼ)P(Aⱼ)
 posterior ∝ likelihood × prior

LLN: X̄ₙ → μ
CLT: (X̄−μ)/(σ/√n) → N(0,1)
 typical n ≥ 30

HYPOTHESIS TEST
 type I: α (reject true H₀)
 type II: β
 power = 1 − β
 reject if p < α

CONFIDENCE INTERVAL
 known σ: x̄ ± z·σ/√n
 unknown σ: x̄ ± t·s/√n

ESTIMATOR
 MSE = Var + Bias²
 unbiased ⇒ MSE = Var
 MLE: maximize likelihood

INEQUALITIES
 Markov: P(X≥a) ≤ E/a
 Chebyshev: P(|X−μ|≥kσ) ≤ 1/k²

LAW OF TOTAL VARIANCE
 Var(X) = E[Var(X|Y)] + Var(E[X|Y])
```
