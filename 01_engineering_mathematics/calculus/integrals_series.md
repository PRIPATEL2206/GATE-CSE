# Definite/Indefinite Integrals & Series

> Subject: Engineering Mathematics → Calculus
> GATE weight: **2–4 marks** every year. Integration techniques, definite integral properties, convergence of series.

---

## 1. Concept Explanation

### 1.1 Indefinite Integral

An **antiderivative** F of f is a function with F' = f. The **indefinite integral** is:
`∫ f(x) dx = F(x) + C`
where C is the constant of integration.

### 1.2 Standard Integrals (Memorize)

| Integrand | Antiderivative |
|---|---|
| xⁿ (n ≠ −1) | x^(n+1)/(n+1) |
| 1/x | ln \|x\| |
| eˣ | eˣ |
| aˣ | aˣ/ln a |
| sin x | −cos x |
| cos x | sin x |
| sec² x | tan x |
| csc² x | −cot x |
| sec x · tan x | sec x |
| csc x · cot x | −csc x |
| tan x | −ln \|cos x\| = ln \|sec x\| |
| cot x | ln \|sin x\| |
| sec x | ln \|sec x + tan x\| |
| csc x | ln \|csc x − cot x\| |
| 1/√(1 − x²) | sin⁻¹ x |
| 1/(1 + x²) | tan⁻¹ x |
| 1/(x √(x² − 1)) | sec⁻¹ x |
| 1/√(a² − x²) | sin⁻¹(x/a) |
| 1/(a² + x²) | (1/a) tan⁻¹(x/a) |
| 1/√(x² + a²) | ln(x + √(x² + a²)) |
| 1/√(x² − a²) | ln(x + √(x² − a²)) |

### 1.3 Integration Techniques

**1. Substitution** (u-sub):
If u = g(x), du = g'(x) dx.
`∫ f(g(x)) g'(x) dx = ∫ f(u) du`.

**2. Integration by Parts:**
`∫ u dv = uv − ∫ v du`.

**LIATE rule** for choosing u: **L**ogarithm > **I**nverse trig > **A**lgebraic > **T**rig > **E**xponential.

**3. Partial Fractions:**
For rational functions P(x)/Q(x), decompose:
`(linear factor x − a)^k → A₁/(x−a) + A₂/(x−a)² + … + Aₖ/(x−a)ᵏ`
`(irreducible quadratic ax² + bx + c) → (Bx + C)/(ax² + bx + c)`

**4. Trigonometric Substitutions:**
| Form | Substitution |
|---|---|
| √(a² − x²) | x = a sin θ |
| √(a² + x²) | x = a tan θ |
| √(x² − a²) | x = a sec θ |

**5. Reduction Formulas:**
`∫ sinⁿ x dx`, `∫ cosⁿ x dx`, etc., via recursion.

### 1.4 Definite Integral

`∫_a^b f(x) dx` = signed area under curve from a to b.

**Fundamental Theorem of Calculus (FTC):**
- **Part 1:** `d/dx ∫_a^x f(t) dt = f(x)` (integrand evaluated at upper limit).
- **Part 2:** `∫_a^b f(x) dx = F(b) − F(a)` where F is any antiderivative.

### 1.5 Properties of Definite Integrals

| Property |
|---|
| `∫_a^a f = 0` |
| `∫_a^b f = −∫_b^a f` |
| `∫_a^c f = ∫_a^b f + ∫_b^c f` |
| `∫_a^b (f + g) = ∫_a^b f + ∫_a^b g` |
| `∫_a^b k·f = k · ∫_a^b f` |
| `∫_0^a f(x) dx = ∫_0^a f(a − x) dx` (King property) |
| `∫_{−a}^a f(x) dx = 2∫_0^a f(x) dx` if f even; = 0 if f odd |
| `∫_0^(2a) f(x) dx = 2∫_0^a f(x) dx` if f(2a−x) = f(x) |
| Periodic: `∫_0^(nT) f(x) dx = n ∫_0^T f(x) dx` if f has period T |

### 1.6 Improper Integrals

**Type 1 (infinite limit):**
`∫_a^∞ f(x) dx = lim_{b→∞} ∫_a^b f(x) dx`.

**Type 2 (unbounded integrand):**
`∫_a^b f(x) dx` where f has vertical asymptote at a or b — split and take limits.

**Convergence test for `∫_1^∞ 1/xᵖ dx`:** converges iff p > 1.

### 1.7 Applications of Definite Integrals

| Quantity | Formula |
|---|---|
| Area between curves | `∫_a^b (f(x) − g(x)) dx` for f ≥ g |
| Volume of revolution (disk) | `π ∫_a^b [f(x)]² dx` (around x-axis) |
| Volume (shell) | `2π ∫_a^b x · f(x) dx` (around y-axis) |
| Arc length | `∫_a^b √(1 + (f'(x))²) dx` |
| Average value of f on [a, b] | `(1/(b−a)) ∫_a^b f(x) dx` |

### 1.8 Sequences and Series

**Sequence** {aₙ}: ordered infinite list. Converges to L iff lim aₙ = L.

**Series** Σ aₙ: sum of an infinite sequence. Convergence based on partial sums Sₙ.

### 1.9 Convergence Tests

| Test | When to use |
|---|---|
| **n-th term test** | If lim aₙ ≠ 0, series diverges. (Necessary condition only.) |
| **Geometric series** | Σ rⁿ converges iff \|r\| < 1; sum = a/(1−r). |
| **p-series** | Σ 1/nᵖ converges iff p > 1. |
| **Comparison test** | aₙ ≤ bₙ; if Σbₙ converges, so does Σaₙ. |
| **Limit comparison** | lim (aₙ/bₙ) = c > 0; same convergence. |
| **Ratio test** | L = lim \|aₙ₊₁/aₙ\|; converges if L < 1, diverges if L > 1, inconclusive if L = 1. |
| **Root test** | L = lim ⁿ√\|aₙ\|; same rules. |
| **Integral test** | Σ aₙ converges iff `∫_1^∞ f(x) dx` converges (f decreasing positive). |
| **Alternating series test** | Σ (−1)ⁿ aₙ converges if aₙ ↓ 0. |

### 1.10 Power Series

`Σ aₙ (x − x₀)ⁿ`. Converges within radius of convergence R.

`R = 1/lim sup ⁿ√\|aₙ\| = lim \|aₙ/aₙ₊₁\|`.

| Function | Series | Radius |
|---|---|---|
| eˣ | Σ xⁿ/n! | ∞ |
| sin x | Σ (−1)ⁿ x^(2n+1)/(2n+1)! | ∞ |
| cos x | Σ (−1)ⁿ x^(2n)/(2n)! | ∞ |
| ln(1+x) | Σ (−1)^(n−1) xⁿ/n | 1 (\|x\|<1) |
| 1/(1−x) | Σ xⁿ | 1 |
| (1+x)^α | Σ C(α, n) xⁿ | 1 |

### 1.11 Sum of Standard Series

| Series | Sum |
|---|---|
| `Σ_{k=1}^n k` | n(n+1)/2 |
| `Σ_{k=1}^n k²` | n(n+1)(2n+1)/6 |
| `Σ_{k=1}^n k³` | (n(n+1)/2)² |
| `Σ_{k=0}^n rᵏ` | (1−r^(n+1))/(1−r) |
| `Σ_{k=0}^∞ rᵏ`, \|r\|<1 | 1/(1−r) |
| `Σ_{k=1}^∞ 1/k²` | π²/6 |

### 1.12 Multiple Integrals (essentials)

Double integral: `∬_R f(x, y) dA = ∫∫ f(x, y) dx dy`.

**Fubini:** under reasonable conditions, can swap order:
`∫_a^b ∫_c^d f dy dx = ∫_c^d ∫_a^b f dx dy`.

**Polar:** `dA = r dr dθ`.

> **Summary:** Memorize standard integrals + techniques (sub, by-parts, partial fractions, trig sub). Master FTC and definite-integral properties. Series convergence: ratio + root + p-series + geometric cover most cases.

---

## 2. Important Points

- Antiderivative is unique up to constant; always write +C in indefinite.
- Definite integral is a number; indefinite integral is a function family.
- For continuous f, `∫_a^b f exists`.
- **King property** `∫_0^a f(x) dx = ∫_0^a f(a−x) dx` — extremely useful for symmetric problems.
- **Even/odd** simplifies definite integrals around symmetric intervals.
- Improper integral may be **divergent** even if integrand → 0.
- Geometric series sum: a/(1−r) only when |r| < 1.
- p-series converges iff p > 1; harmonic series (p=1) diverges.
- Ratio test inconclusive at L = 1; switch to root or p-series compare.
- Convergence: Σ aₙ converges ⇒ aₙ → 0. Converse false.
- A series can be **conditionally convergent** (alternating but Σ|aₙ| diverges) or **absolutely convergent**.
- Power series can be differentiated/integrated term-by-term within radius of convergence.
- ∫₀^∞ e^(−x) dx = 1; ∫₀^∞ e^(−x²) dx = √π/2.
- For double integral, swapping order may simplify.
- Volume of revolution: disk method around horizontal axis is cleanest.

---

## 3. Short Notes

```
INDEFINITE
 ∫ xⁿ dx = x^(n+1)/(n+1) + C  (n ≠ −1)
 ∫ 1/x dx = ln|x|
 ∫ eˣ dx = eˣ
 ∫ sin x = −cos x
 ∫ cos x = sin x
 ∫ sec² x = tan x
 ∫ 1/(1+x²) = tan⁻¹ x
 ∫ 1/√(1−x²) = sin⁻¹ x

TECHNIQUES
 substitution u = g(x)
 by parts: ∫u dv = uv − ∫v du  (LIATE)
 partial fractions
 trig sub: √(a²−x²): x=a sinθ
            √(a²+x²): x=a tanθ
            √(x²−a²): x=a secθ

DEFINITE
 FTC: ∫_a^b f = F(b) − F(a)
 ∫_a^b f = −∫_b^a f
 ∫_0^a f(x) dx = ∫_0^a f(a−x) dx  (King)
 even: ∫_{−a}^a 2 ∫_0^a; odd: 0
 periodic T: ∫_0^(nT) = n·∫_0^T

IMPROPER
 ∫_1^∞ 1/xᵖ converges ⇔ p>1
 type 1: ∞ limit
 type 2: unbounded integrand

APPLICATIONS
 area = ∫(f − g)
 vol disk: π ∫f² dx
 vol shell: 2π ∫x f dx
 arc len: ∫√(1+f'²)
 avg = (1/(b−a)) ∫f

SERIES TESTS
 nth term: aₙ ↛ 0 ⇒ diverge
 geometric: |r|<1 ⇒ a/(1−r)
 p-series: 1/nᵖ converges ⇔ p>1
 ratio: L<1 conv, L>1 div
 root: L<1 conv
 integral test
 alternating: aₙ ↓ 0

SUMS
 Σ k = n(n+1)/2
 Σ k² = n(n+1)(2n+1)/6
 Σ k³ = (n(n+1)/2)²
 Σ rᵏ (geom finite/infinite)
 Σ 1/k² = π²/6

POWER SERIES
 R = lim |aₙ/aₙ₊₁|
 eˣ = Σ xⁿ/n!  R=∞
 sin x = Σ (−1)ⁿ x^(2n+1)/(2n+1)!
 cos x = Σ (−1)ⁿ x^(2n)/(2n)!
 ln(1+x): R=1
 1/(1−x) = Σxⁿ: R=1

DOUBLE INT
 ∬f dA = ∫∫ f dx dy
 Fubini: swap order
 polar: dA = r dr dθ
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | ∫ xⁿ dx (n ≠ −1) = x^(n+1)/(n+1) | ✅✅ |
| 2 | ∫ 1/x dx = ln \|x\| | ✅✅ |
| 3 | ∫ eˣ dx = eˣ | ✅✅ |
| 4 | ∫ sin x = −cos x; ∫ cos x = sin x | ✅✅ |
| 5 | ∫ 1/(1 + x²) = tan⁻¹ x | ✅ |
| 6 | ∫ 1/√(1 − x²) = sin⁻¹ x | ✅ |
| 7 | Integration by parts: ∫u dv = uv − ∫v du; LIATE | ✅✅ |
| 8 | King: ∫_0^a f(x) = ∫_0^a f(a−x) | ✅✅ |
| 9 | Even / odd shortcut on symmetric intervals | ✅ |
| 10 | Geometric: \|r\|<1 ⇒ a/(1−r) | ✅✅ |
| 11 | p-series convergence | ✅✅ |
| 12 | Ratio test | ✅✅ |
| 13 | Σ k, Σ k², Σ k³ formulas | ✅✅ |
| 14 | eˣ, sin x, cos x, ln(1+x), 1/(1−x) Maclaurin series | ✅ |
| 15 | ∫₀^∞ e^(−x²) = √π/2 | ✅ |
| 16 | Reduction formula for sinⁿ x | ✅ |
| 17 | FTC: d/dx ∫_a^x f(t) dt = f(x) | ✅✅ |

### Tricks

- **King's property + symmetric interval:** drastically simplifies many definite integrals.
- **Even/odd substitution:** turn integrals to half their range.
- **Algebraic substitution:** for `∫ x · f(x²) dx`, use u = x² ⇒ du = 2x dx.
- **By parts twice:** for products like `eˣ · sin x` — use it twice and solve algebraically.
- **For `∫ ln(x)`:** use by parts with u = ln x, dv = dx.
- **Partial fractions shortcut:** plug in roots to find coefficients quickly (cover-up method).
- **For series convergence at L = 1:** ratio test fails; switch to p-series compare or alternating test.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Evaluate `∫_0^1 x · eˣ dx`.
**Solution.** By parts: u = x, dv = eˣ dx ⇒ du = dx, v = eˣ.
= x eˣ \|_0^1 − ∫_0^1 eˣ dx = e − (e − 1) = 1.
**Answer: 1.**

### Q2. (GATE CSE 2014)
`∫_0^∞ e^(−x²) dx = ?`
**Answer: √π/2.**

### Q3. (GATE CSE 2018)
`∫_0^π sin² x dx = ?`
**Solution.** Use sin² x = (1 − cos 2x)/2; integrate: π/2.

### Q4. (GATE CSE 2008)
Series `Σ 1/n²` converges to:
**Answer: π²/6.**

### Q5. (GATE CSE 2010)
For what p does `Σ 1/nᵖ` converge?
**Solution.** p > 1.

### Q6. (GATE CSE 2015)
`∫_0^1 1/(1 + x²) dx = ?`
**Solution.** = tan⁻¹(1) − tan⁻¹(0) = π/4.

### Q7. (GATE CSE 2007)
`Σ_{n=0}^∞ 1/2ⁿ = ?`
**Solution.** Geometric: 1/(1 − 1/2) = 2.

### Q8. (GATE CSE 2013)
Apply ratio test to `Σ nⁿ/n!`. Converges?
**Solution.** Ratio: ((n+1)^(n+1)/(n+1)!) / (nⁿ/n!) = (n+1)/(n+1) · ((n+1)/n)ⁿ → e > 1. **Diverges.**

### Q9. (GATE CSE 2003)
`∫ ln(x) dx = ?`
**Solution.** By parts (u = ln x, dv = dx): x ln x − x + C.

### Q10. (GATE CSE 2009)
Area between y = x² and y = x from 0 to 1:
**Solution.** ∫_0^1 (x − x²) dx = 1/2 − 1/3 = 1/6.

### Q11. (GATE CSE 2019)
`∫_0^(π/2) sin⁴(x) dx`:
**Solution.** Wallis: 3π/16.

### Q12. (GATE CSE 2020)
`Σ_{n=1}^∞ (−1)^(n−1)/n = ?`
**Answer: ln 2.**

### Q13. (GATE CSE 2021)
`∫_0^1 x · sin(πx) dx`:
**Solution.** By parts: u = x, dv = sin(πx) dx; v = −(1/π)cos(πx); = −(x/π)cos(πx)\|₀¹ + (1/π) ∫ cos(πx) dx = 1/π + 0 = 1/π.

### Q14. (GATE CSE 2016)
Volume of revolution of y = x², 0 ≤ x ≤ 1, around x-axis:
**Solution.** π ∫_0^1 x⁴ dx = π/5.

### Q15. (GATE CSE 2011)
`Σ 1/n` (harmonic series) is:
**Answer: divergent.**

---

## 6. Practice Questions (20+)

### Easy

**P1.** `∫ x² dx`.

**P2.** `∫ 1/x dx`.

**P3.** `∫ eˣ dx`.

**P4.** `∫ sin x dx`.

**P5.** `∫_0^1 (2x + 1) dx`.

**P6.** `∫_0^π sin x dx`.

**P7.** `Σ_{k=1}^{10} k`.

**P8.** Sum of geometric series 1 + 1/2 + 1/4 + ….

**P9.** Does `Σ 1/n` converge?

**P10.** Does `Σ 1/n²` converge? To what?

### Medium

**P11.** `∫ x · cos x dx`.

**P12.** `∫ ln x dx`.

**P13.** `∫ 1/(x² + 4) dx`.

**P14.** `∫_0^(π/2) sin² x dx`.

**P15.** Use partial fractions: `∫ 1/(x² − 1) dx`.

**P16.** Apply ratio test to `Σ n/2ⁿ`.

**P17.** Sum of `1 − 1/2 + 1/4 − 1/8 + …`.

**P18.** Find Maclaurin of `1/(1+x)`.

**P19.** Compute `∫_0^1 x²/(1+x³) dx`.

**P20.** `∫_0^∞ e^(−2x) dx`.

### Hard

**P21.** `∫_0^(π/2) sin⁵ x · cos² x dx` (Wallis).

**P22.** Sum of `Σ_{n=1}^∞ n/2ⁿ`.

**P23.** Volume of revolution of y = sin x, 0 ≤ x ≤ π, around x-axis.

**P24.** `∫_0^1 ln(x)/(1−x) dx` (use series).

**P25.** Determine convergence of `Σ (n!)²/(2n)!`.

**P26.** Compute `∫∫_R xy dA` where R: 0 ≤ x ≤ 1, 0 ≤ y ≤ 2.

**P27.** Evaluate `∫_0^1 1/(√(1−x²)) dx`.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | x³/3 + C | power |
| P2 | ln \|x\| + C | log |
| P3 | eˣ + C | exp |
| P4 | −cos x + C | trig |
| P5 | 2 | direct |
| P6 | 2 | direct |
| P7 | 55 | n(n+1)/2 |
| P8 | 2 | a/(1−r) |
| P9 | No | harmonic |
| P10 | Yes; π²/6 | p-series |
| P11 | x sin x + cos x + C | by parts |
| P12 | x ln x − x + C | by parts |
| P13 | (1/2) tan⁻¹(x/2) + C | direct |
| P14 | π/4 | half-angle |
| P15 | (1/2) ln \|(x−1)/(x+1)\| + C | partial frac |
| P16 | converges (L = 1/2) | ratio |
| P17 | 2/3 | geometric a=1, r=−1/2 |
| P18 | Σ (−1)ⁿ xⁿ | binomial |
| P19 | (1/3) ln 2 | u = 1+x³ |
| P20 | 1/2 | direct |
| P21 | 8/105 | Wallis or substitution |
| P22 | 2 | known sum |
| P23 | π²/2 | π ∫sin² = π²/2 |
| P24 | π²/6 | dilog |
| P25 | Converges (ratio = 1/4) | ratio |
| P26 | ∫_0^1 ∫_0^2 xy dy dx = ∫_0^1 2x dx = 1 | direct |
| P27 | π/2 | sin⁻¹(1) |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting +C | Always include in indefinite. |
| 2 | Misapplying by-parts choice (u, dv) | Use LIATE order. |
| 3 | Treating improper integral as ordinary | Take limits explicitly. |
| 4 | Confusing area with integral (signed) | Use absolute value if needed. |
| 5 | Series convergence: forgetting nth-term test | If aₙ ↛ 0, immediately diverge. |
| 6 | Misapplying p-series test | Critical p = 1. |
| 7 | Geometric sum without \|r\| < 1 check | Otherwise series diverges. |
| 8 | Power series outside radius | Check x's location. |
| 9 | Substitution forgetting du | Always express dx in terms of du. |
| 10 | Treating non-uniform convergence as differentiable termwise | Need uniform convergence for swaps. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "∫ polynomial · trig" | By parts; LIATE. |
| "∫ logarithm" | By parts (u = ln x, dv = dx). |
| "Rational function" | Partial fractions. |
| "√(a² ± x²)" | Trig substitution. |
| "Integrate from 0 to a; symmetric" | King property. |
| "Even/odd integrand on [−a, a]" | 2× or 0. |
| "Series Σ 1/nᵖ" | p-series. |
| "Series with factorials/exponential" | Ratio test. |
| "Series sum to closed form" | Geometric, telescoping, or known identity. |
| "Volume of revolution" | π ∫ f² dx (disk). |
| "Average of f on [a,b]" | (1/(b−a)) ∫. |
| "Improper integral convergence" | Compare to 1/xᵖ. |

---

## 9. Quick Revision

```
∫ xⁿ = x^(n+1)/(n+1) (n≠−1)
∫ 1/x = ln|x|     ∫ eˣ = eˣ
∫ sin = −cos     ∫ cos = sin
∫ sec² = tan     ∫ 1/(1+x²) = tan⁻¹ x

BY PARTS: ∫u dv = uv − ∫v du   (LIATE)
TRIG SUB
 √(a²−x²): x = a sinθ
 √(a²+x²): x = a tanθ
 √(x²−a²): x = a secθ

DEFINITE
 FTC: ∫_a^b f = F(b)−F(a)
 King: ∫_0^a f(x) = ∫_0^a f(a−x)
 even on [−a,a]: 2∫_0^a; odd: 0
 periodic: ∫_0^(nT) = n ∫_0^T

IMPROPER ∫_1^∞ 1/xᵖ : conv ⇔ p>1

GEOMETRIC: |r|<1 ⇒ a/(1−r)
p-SERIES: conv ⇔ p>1
RATIO: lim |aₙ₊₁/aₙ| < 1 conv

SUMS
 Σ k = n(n+1)/2
 Σ k² = n(n+1)(2n+1)/6
 Σ k³ = (Σk)²
 Σ 1/k² = π²/6

MACLAURIN
 eˣ = Σ xⁿ/n!
 sin x = Σ (−1)ⁿ x^(2n+1)/(2n+1)!
 cos x = Σ (−1)ⁿ x^(2n)/(2n)!
 ln(1+x) = Σ (−1)^(n−1) xⁿ/n
 1/(1−x) = Σ xⁿ

APPLICATIONS
 area ∫(f−g)
 vol disk π ∫f²
 vol shell 2π ∫xf
 arc len ∫ √(1+f'²)
 avg (1/(b−a)) ∫f
```
