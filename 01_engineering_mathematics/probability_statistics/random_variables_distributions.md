# Random Variables & Distributions

> Subject: Engineering Mathematics → Probability & Statistics
> GATE weight: **2–4 marks** every year. PMF/PDF/CDF, expectation, common distributions (Bernoulli, Binomial, Poisson, Uniform, Exp, Normal).

---

## 1. Concept Explanation

### 1.1 Random Variable

A **random variable (RV)** X is a function from the sample space S to ℝ.

| Type | Range |
|---|---|
| Discrete | countable (e.g., ℕ, ℤ) |
| Continuous | uncountable (interval in ℝ) |
| Mixed | parts discrete, parts continuous |

### 1.2 Probability Mass Function (Discrete)

For a discrete RV X with values x₁, x₂, …:

`p(xᵢ) = P(X = xᵢ)`, where:
- p(xᵢ) ≥ 0
- `Σ p(xᵢ) = 1`

### 1.3 Probability Density Function (Continuous)

For a continuous RV X:

`f(x)` is the PDF if:
- f(x) ≥ 0
- `∫_{−∞}^∞ f(x) dx = 1`
- `P(a ≤ X ≤ b) = ∫_a^b f(x) dx`
- `P(X = c) = 0` for any single point c.

### 1.4 Cumulative Distribution Function (CDF)

For any RV X:
`F(x) = P(X ≤ x)`

| Property |
|---|
| F is non-decreasing |
| F(−∞) = 0, F(∞) = 1 |
| F is right-continuous |
| For continuous X: f(x) = F'(x) |
| For discrete X: F is a step function |
| P(a < X ≤ b) = F(b) − F(a) |

### 1.5 Expectation (Mean)

**Discrete:** `E[X] = Σ x · p(x)`.
**Continuous:** `E[X] = ∫ x · f(x) dx`.

| Property |
|---|
| E[c] = c |
| E[cX] = c · E[X] |
| E[X + Y] = E[X] + E[Y] (always linear) |
| E[g(X)] = Σ g(xᵢ) p(xᵢ) (or ∫) |

### 1.6 Variance & Standard Deviation

`Var(X) = E[(X − E[X])²] = E[X²] − (E[X])²`
`SD(X) = √Var(X)`

| Property |
|---|
| Var(c) = 0 |
| Var(cX) = c² · Var(X) |
| Var(X + c) = Var(X) |
| Var(X + Y) = Var(X) + Var(Y) if X ⊥ Y (independent) |
| Var(aX + bY) = a²Var(X) + b²Var(Y) + 2ab·Cov(X,Y) |

### 1.7 Common Discrete Distributions

| Name | PMF | E[X] | Var(X) |
|---|---|---|---|
| Bernoulli(p) | p, 1−p | p | p(1−p) |
| Binomial(n, p) | C(n,k)·pᵏ(1−p)^(n−k) | np | np(1−p) |
| Geometric(p) | (1−p)^(k−1) · p (k = 1, 2, …) | 1/p | (1−p)/p² |
| Poisson(λ) | e^(−λ) λᵏ/k! | λ | λ |
| Hypergeometric(N,K,n) | C(K,k)C(N−K,n−k)/C(N,n) | nK/N | nK(N−K)(N−n)/(N²(N−1)) |
| Negative Binomial(r,p) | C(k−1,r−1)pʳ(1−p)^(k−r) | r/p | r(1−p)/p² |
| Discrete Uniform(1..n) | 1/n | (n+1)/2 | (n²−1)/12 |

### 1.8 Common Continuous Distributions

| Name | PDF | E[X] | Var(X) |
|---|---|---|---|
| Uniform(a, b) | 1/(b−a) for x ∈ [a,b] | (a+b)/2 | (b−a)²/12 |
| Exponential(λ) | λe^(−λx), x ≥ 0 | 1/λ | 1/λ² |
| Normal(μ, σ²) | (1/(σ√2π)) e^(−(x−μ)²/2σ²) | μ | σ² |
| Standard Normal N(0,1) | (1/√2π) e^(−x²/2) | 0 | 1 |
| Chi-squared(k) | … | k | 2k |
| Gamma(α, β) | … | α/β | α/β² |

### 1.9 Bernoulli & Binomial

- **Bernoulli(p):** single trial; success (X=1) with prob p.
- **Binomial(n, p):** sum of n independent Bernoulli(p). PMF: `C(n,k) pᵏ (1−p)^(n−k)`.

**Mean = np, Variance = np(1−p).**

### 1.10 Geometric & Negative Binomial

- **Geometric(p):** trials until the **first success**.
  - PMF: `(1−p)^(k−1) p`, k = 1, 2, …
  - Memoryless: `P(X > m + n | X > m) = P(X > n)`.
- **Negative Binomial(r, p):** trials until r-th success.

### 1.11 Poisson Distribution

`P(X = k) = e^(−λ) λᵏ / k!` (k = 0, 1, …)

- **E[X] = Var(X) = λ**.
- Models: rare events in a fixed interval (calls per minute, errors per page).
- **Limit of Binomial(n, p):** when n → ∞, p → 0, np → λ → Binomial → Poisson(λ).
- **Sum:** X ~ Poisson(λ₁), Y ~ Poisson(λ₂), independent ⇒ X + Y ~ Poisson(λ₁ + λ₂).

### 1.12 Uniform Distribution

- **Discrete uniform on {1, …, n}:** mean (n+1)/2, var (n²−1)/12.
- **Continuous uniform on [a, b]:** mean (a+b)/2, var (b−a)²/12.

### 1.13 Exponential Distribution

`f(x) = λ e^(−λx)`, x ≥ 0.

- E[X] = 1/λ, Var = 1/λ².
- **Memoryless:** `P(X > s + t | X > s) = P(X > t)`.
- Models: time between Poisson events.

### 1.14 Normal (Gaussian) Distribution

`f(x) = (1/(σ√(2π))) · e^(−(x−μ)²/(2σ²))`

- Parameters: μ (mean), σ² (variance).
- Symmetric around μ.
- **Standardization:** Z = (X − μ)/σ ~ N(0, 1).

| Range | Probability |
|---|---|
| μ ± σ | ≈ 68% |
| μ ± 2σ | ≈ 95% |
| μ ± 3σ | ≈ 99.7% |

### 1.15 Joint Distributions

**Joint PMF/PDF:** `p(x, y)` or `f(x, y)`.

| Quantity | Definition |
|---|---|
| Marginal | p_X(x) = Σ_y p(x, y); f_X(x) = ∫ f(x, y) dy |
| Conditional | p(y | x) = p(x, y)/p_X(x) |
| Independence | p(x, y) = p_X(x) · p_Y(y) |
| Covariance | Cov(X,Y) = E[XY] − E[X]E[Y] |
| Correlation | ρ(X,Y) = Cov(X,Y)/(σ_X σ_Y) ∈ [−1, 1] |

### 1.16 Markov & Chebyshev Inequalities

- **Markov:** for X ≥ 0, P(X ≥ a) ≤ E[X]/a.
- **Chebyshev:** P(|X − μ| ≥ k σ) ≤ 1/k².

> **Summary:** Memorize the distribution table — Bernoulli → Binomial → Poisson, Uniform/Exp/Normal. Master CDF derivation, expectation linearity, variance addition (with independence). Use standardization for Normal questions.

---

## 2. Important Points

- For continuous X: P(X = c) = 0; intervals matter.
- CDF is always non-decreasing and right-continuous.
- For discrete X, P(X = a) = F(a) − F(a⁻) (jump size).
- **Memoryless** distributions: only Geometric (discrete) and Exponential (continuous).
- E[X] is **always linear**: E[aX + bY] = aE[X] + bE[Y] regardless of independence.
- Var is **not linear**; Var(X + Y) = Var(X) + Var(Y) **iff X, Y independent**.
- For Binomial(n, p): **mode** ≈ ⌊(n+1)p⌋.
- For Poisson(λ): when λ is integer, modes at λ−1 and λ.
- The sum of independent Binomials with same p: Binomial; same with Poisson, Normal.
- N(μ, σ²) + N(ν, τ²) (independent) = N(μ+ν, σ²+τ²).
- For normal X with mean μ, P(X > μ) = P(X < μ) = 0.5 by symmetry.
- Cov(X, X) = Var(X).
- Independent ⇒ Cov = 0; converse **false** in general.

---

## 3. Short Notes

```
RV TYPES
 discrete: PMF p(x); Σ = 1
 continuous: PDF f(x); ∫ = 1
 CDF F(x) = P(X ≤ x); F'=f (cont)

EXPECTATION
 discrete: Σ x·p(x)
 continuous: ∫ x f(x) dx
 linear: E[aX+bY] = aE[X] + bE[Y]
 E[g(X)] = Σ g(x)p(x) or ∫

VARIANCE
 Var = E[X²] − (E[X])²
 Var(c) = 0
 Var(cX) = c² Var
 Var(X+c) = Var
 X ⊥ Y: Var(X+Y) = Var(X) + Var(Y)

DISCRETE DISTROS
 Bernoulli(p):  E=p,  Var=p(1−p)
 Bin(n,p):      E=np, Var=np(1−p)
 Geom(p):       E=1/p, Var=(1−p)/p²; memoryless
 Poisson(λ):    E=Var=λ
 NB(r,p):       E=r/p, Var=r(1−p)/p²
 Hypergeom:     no replacement

CONTINUOUS DISTROS
 Unif(a,b):     E=(a+b)/2, Var=(b−a)²/12
 Exp(λ):        E=1/λ, Var=1/λ²; memoryless
 N(μ,σ²):       E=μ, Var=σ²; standardize Z=(X−μ)/σ

MEMORYLESS: Geom, Exp only

POISSON LIMIT:
 Bin(n,p) → Poisson(λ=np), n large p small

SUM (indep):
 Bin(n,p)+Bin(m,p) = Bin(n+m,p)
 Poisson(λ₁)+Poisson(λ₂) = Poisson(λ₁+λ₂)
 N(μ₁,σ₁²)+N(μ₂,σ₂²) = N(μ₁+μ₂, σ₁²+σ₂²)

JOINT
 marginal: sum/integrate other
 indep: p(x,y) = p_X p_Y
 Cov = E[XY]−E[X]E[Y]
 Corr = Cov/(σ_X σ_Y)

INEQUALITIES
 Markov: P(X≥a) ≤ E[X]/a (X≥0)
 Chebyshev: P(|X−μ|≥kσ) ≤ 1/k²

NORMAL
 68-95-99.7 rule
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | E[X] linearity | ✅✅✅ |
| 2 | Var = E[X²] − (E[X])² | ✅✅✅ |
| 3 | Independent sum: Var adds | ✅✅ |
| 4 | Bin(n,p): E=np, Var=np(1−p) | ✅✅ |
| 5 | Poisson(λ): E=Var=λ | ✅✅ |
| 6 | Geom(p): E=1/p, Var=(1−p)/p² | ✅ |
| 7 | Exp(λ): E=1/λ, Var=1/λ² | ✅✅ |
| 8 | Uniform[a,b]: E=(a+b)/2, Var=(b−a)²/12 | ✅✅ |
| 9 | Normal standardization Z=(X−μ)/σ | ✅✅ |
| 10 | 68-95-99.7 rule for Normal | ✅ |
| 11 | Memoryless property of Geom and Exp | ✅✅ |
| 12 | Poisson approx of Binomial | ✅ |
| 13 | Cov(X,Y) = E[XY] − E[X]E[Y] | ✅ |
| 14 | Markov & Chebyshev inequalities | ✅ |

### Tricks

- **Variance shortcut:** Var(X) = E[X²] − μ². Compute E[X²] directly.
- **Sum of distributions:** binomial+binomial / Poisson+Poisson / Normal+Normal stay in family if independent.
- **Memoryless:** for "given X > s, what's P(X > s + t)?" — equals P(X > t) for Geom/Exp.
- **Approximate Binomial(n large, p small) as Poisson(np)**.
- **Approximate Binomial(n large, p moderate) as Normal(np, np(1−p))**.
- **Symmetry shortcut for Normal:** P(X > μ) = P(X < μ) = 0.5.
- **Sum of n iid Bernoullis = Binomial**; **sum of n iid Exponentials = Erlang(n, λ)**.
- For uniform[0, 1]ⁿ continuous joint: P(X₁ < X₂ < … < Xₙ) = 1/n!.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A coin is tossed 4 times. Probability of getting exactly 2 heads?
**Solution.** Bin(4, 1/2): C(4,2)·(1/2)⁴ = 6/16 = 3/8.

### Q2. (GATE CSE 2014)
X ~ Poisson(3). P(X = 0) ?
**Solution.** e^(−3).

### Q3. (GATE CSE 2018)
X ~ Uniform[0, 4]. E[X²]?
**Solution.** ∫_0^4 x²·(1/4) dx = 16/3.

### Q4. (GATE CSE 2008)
X ~ N(0,1). P(X > 0) = ?
**Solution.** 0.5.

### Q5. (GATE CSE 2015)
X ~ Bin(10, 0.5). E[X] and Var(X)?
**Solution.** E = 5, Var = 2.5.

### Q6. (GATE CSE 2013)
A fair die is rolled. X = score. E[X] and Var(X).
**Solution.** E = 3.5, Var = 35/12 ≈ 2.917.

### Q7. (GATE CSE 2016)
Continuous RV X has PDF f(x) = 2x for 0 ≤ x ≤ 1, 0 elsewhere. E[X]?
**Solution.** ∫_0^1 x·2x dx = 2/3.

### Q8. (GATE CSE 2010)
X ~ Exponential(λ=2). P(X > 1)?
**Solution.** e^(−2).

### Q9. (GATE CSE 2007)
A coin is biased with P(H) = 1/3. Tossed until first head. E[# tosses]?
**Solution.** Geom: E = 1/p = 3.

### Q10. (GATE CSE 2003)
X uniform on {1, 2, …, 10}. E[X], Var(X).
**Solution.** E = 5.5, Var = (10²−1)/12 = 8.25.

### Q11. (GATE CSE 2009)
X ~ N(μ=10, σ²=4). P(X > 14) (approximately)?
**Solution.** Z = (14−10)/2 = 2; P(Z > 2) ≈ 0.0228.

### Q12. (GATE CSE 2019)
Calls arrive at rate 4 per hour (Poisson). P(exactly 2 calls in 30 min)?
**Solution.** In 30 min, mean = 2; P(X=2) = e^(−2)·4/2 = 2e^(−2) ≈ 0.27.

### Q13. (GATE CSE 2020)
X ~ Bin(n, p), Y ~ Bin(m, p), independent. Distribution of X + Y?
**Solution.** Bin(n + m, p).

### Q14. (GATE CSE 2021)
X ~ Exp(λ). Memoryless property: P(X > 5 | X > 2) = ?
**Solution.** P(X > 3) = e^(−3λ).

### Q15. (GATE CSE 2011)
X has PDF f(x) = c(1−x²) for −1 ≤ x ≤ 1. Find c.
**Solution.** ∫_{−1}^1 c(1−x²) dx = c · 4/3 = 1 ⇒ c = 3/4.

---

## 6. Practice Questions (20+)

### Easy

**P1.** X uniform on {1,…,6}. E[X]?

**P2.** X ~ Bernoulli(0.7). E[X]?

**P3.** X ~ Bin(5, 0.4). E[X]?

**P4.** X ~ Poisson(λ=2). P(X = 3)?

**P5.** X ~ Exp(λ=1). P(X > 2)?

**P6.** X ~ U(0, 5). E[X], Var(X)?

**P7.** X ~ N(0, 1). P(|X| < 2) ≈?

**P8.** X ~ Geom(1/4). E[X]?

**P9.** State 68-95-99.7 rule.

**P10.** X = score of fair die; Y = score of another. E[X + Y]?

### Medium

**P11.** A continuous RV has f(x) = kx² for 0 ≤ x ≤ 2, else 0. Find k.

**P12.** X ~ Bin(10, 0.5). P(X = 5)?

**P13.** X ~ Poisson(λ=4). E[X²]?

**P14.** X ~ U(2, 6). P(3 < X < 5)?

**P15.** Two independent Bin(5, 0.4). Distribution of sum?

**P16.** X is the number of tails before first head in tosses of a fair coin. E[X]?

**P17.** X ~ N(50, 100). Standardize to find P(X > 70).

**P18.** Show Var(aX + b) = a² Var(X).

**P19.** X uniform on [0, 10]. CDF F(x).

**P20.** A factory produces items with defect rate 0.01. In a batch of 200, P(at least 1 defective)?

### Hard

**P21.** X ~ Exp(λ). Find E[X²] and Var(X).

**P22.** Two iid Exp(λ) variables. Distribution of min(X₁, X₂)?

**P23.** X has PDF f(x) = λ²x e^(−λx) for x > 0 (Erlang-2). Find E[X].

**P24.** X ~ Bin(100, 0.5). Approximate P(X > 60) using Normal.

**P25.** X uniform on [0, 1]. Y = X². Find E[Y], Var(Y).

**P26.** X, Y iid Uniform[0,1]. Find E[max(X, Y)].

**P27.** A coin is tossed until 3 heads. Distribution of # tosses?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 3.5 | (1+6)/2 |
| P2 | 0.7 | Bern |
| P3 | 2 | np |
| P4 | e⁻²·8/6 = 4e⁻²/3 ≈ 0.180 | direct |
| P5 | e⁻² ≈ 0.135 | exp tail |
| P6 | E=2.5, Var=25/12 | uniform |
| P7 | ≈ 0.954 | 95% rule |
| P8 | 4 | 1/p |
| P9 | as in 1.14 | direct |
| P10 | 7 | linearity |
| P11 | k = 3/8 | ∫₀² 3x²/8 = 1 |
| P12 | C(10,5)·(1/2)¹⁰ = 252/1024 ≈ 0.246 | binomial |
| P13 | E[X²] = Var + (E)² = 4 + 16 = 20 | direct |
| P14 | 1/2 | uniform |
| P15 | Bin(10, 0.4) | sum same p |
| P16 | 1 | E = (1−p)/p = 1 |
| P17 | Z = 2; P ≈ 0.0228 | std Normal |
| P18 | direct | Var properties |
| P19 | x/10 for 0 ≤ x ≤ 10 | uniform CDF |
| P20 | 1 − (0.99)²⁰⁰ ≈ 1 − 0.134 = 0.866 | Bernoulli/binomial |
| P21 | E[X²] = 2/λ², Var = 1/λ² | by parts or formula |
| P22 | Exp(2λ) | min of independent Exps |
| P23 | E = 2/λ | Erlang formula |
| P24 | Z = (60−50)/5 = 2; P ≈ 0.0228 | normal approximation |
| P25 | E[Y] = 1/3, Var = 4/45 | ∫x², (∫x⁴ − 1/9) |
| P26 | 2/3 | E[max] = ∫P(max>x)dx = ∫(1−x²)dx |
| P27 | NB(3, 1/2): k tosses for 3 heads (k = 3, 4, …) | Negative Binomial |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting P(X = c) = 0 for continuous X | Use intervals. |
| 2 | Adding variances of dependent variables | Use Cov term: Var(X+Y) = VarX + VarY + 2Cov. |
| 3 | Confusing PDF with PMF | PDF can exceed 1; PMF cannot. |
| 4 | Using Var = E[X]² | Var = E[X²] − (E[X])². |
| 5 | Forgetting 1−p for Bernoulli/Geometric | "p of failure" vs "p of success". |
| 6 | Wrong mean for Geometric (k = 1, 2, …) | Mean = 1/p. |
| 7 | Treating Poisson and Binomial interchangeably without limit | Only when n large, p small. |
| 8 | Standardizing Normal incorrectly | Use Z = (X−μ)/σ, not σ². |
| 9 | Ignoring memoryless restriction | Only Exp and Geom have this. |
| 10 | Computing CDF without checking bounds | F = 0 for x < a, 1 for x > b in finite-support cases. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Number of successes in n trials" | Binomial. |
| "Trials until first success" | Geometric. |
| "Trials until r-th success" | Negative Binomial. |
| "Rare events / arrivals per time" | Poisson. |
| "Time between arrivals" | Exponential. |
| "Uniform random in [a, b]" | Uniform. |
| "Bell-curve / IQ / heights" | Normal. |
| "Memoryless?" | Geom (discrete) / Exp (continuous). |
| "P(X = k) for Poisson" | e^(−λ) λᵏ/k!. |
| "Compute E[X²]" | Use Var + μ². |
| "Sum of independent same-type" | Stays in same family for Bin/Poisson/Normal. |

---

## 9. Quick Revision

```
DISCRETE                    E       Var
 Bern(p)                    p       p(1−p)
 Bin(n,p)                   np      np(1−p)
 Geom(p) (k=1,2,…)          1/p     (1−p)/p²
 Poisson(λ)                 λ       λ
 NB(r,p)                    r/p     r(1−p)/p²
 Discrete Unif(1..n)        (n+1)/2 (n²−1)/12

CONTINUOUS                  E         Var
 Unif(a,b)                  (a+b)/2   (b−a)²/12
 Exp(λ)                     1/λ       1/λ²
 N(μ,σ²)                    μ         σ²

MEMORYLESS: Geom, Exp
SUMS (indep, same fam):
 Bin+Bin (same p), Poisson+Poisson, Normal+Normal stay in family

E LINEAR: E[aX+bY] = aE+bE
Var:  Var(cX) = c² Var
       Var(X+Y) = Var(X)+Var(Y) iff indep

NORMAL
 Z = (X−μ)/σ
 68%, 95%, 99.7%

CDF
 P(a<X≤b) = F(b)−F(a)
 cont: f = F'
 disc: jump = P(X=c)

POISSON LIMIT: Bin(n,p) → Poisson(np)
NORMAL APPROX: Bin(n,p) ≈ N(np, np(1−p)) for large n
```
