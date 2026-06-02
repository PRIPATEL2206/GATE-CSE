# Limits, Continuity & Differentiability

> Subject: Engineering Mathematics → Calculus
> GATE weight: **1–3 marks** every year. Direct evaluation, indeterminate forms, L'Hôpital, continuity tests, differentiability checks.

---

## 1. Concept Explanation

### 1.1 Limit

`lim_{x→a} f(x) = L` means: as x approaches a, f(x) approaches L.

**Formal (ε–δ):** ∀ε > 0, ∃ δ > 0 such that 0 < |x − a| < δ ⇒ |f(x) − L| < ε.

**One-sided limits:**
- Left:  `lim_{x→a⁻} f(x)`
- Right: `lim_{x→a⁺} f(x)`

The two-sided limit exists iff both one-sided limits exist and are equal.

### 1.2 Properties of Limits

If `lim f = L` and `lim g = M`, then:
- `lim (f ± g) = L ± M`
- `lim (f·g) = L·M`
- `lim (f/g) = L/M` (M ≠ 0)
- `lim (f^n) = Lⁿ`
- `lim (cf) = cL`

### 1.3 Standard Limits (Memorize)

| Limit | Value |
|---|---|
| `lim_{x→0} sin(x)/x` | 1 |
| `lim_{x→0} (1−cos x)/x²` | 1/2 |
| `lim_{x→0} (1−cos x)/x` | 0 |
| `lim_{x→0} tan(x)/x` | 1 |
| `lim_{x→0} (eˣ − 1)/x` | 1 |
| `lim_{x→0} (aˣ − 1)/x` | ln a |
| `lim_{x→0} ln(1 + x)/x` | 1 |
| `lim_{x→0} (1 + x)^(1/x)` | e |
| `lim_{x→∞} (1 + 1/x)ˣ` | e |
| `lim_{x→∞} (1 + a/x)ˣ` | eᵃ |
| `lim_{x→0} (xⁿ − aⁿ)/(x − a)` | n·a^(n−1) |
| `lim_{x→0} sinh(x)/x` | 1 |

### 1.4 Indeterminate Forms

| Form | Strategy |
|---|---|
| 0/0 | L'Hôpital, factor, conjugate, series |
| ∞/∞ | L'Hôpital, divide by highest power |
| 0·∞ | Rewrite as 0/0 or ∞/∞ |
| ∞ − ∞ | Common factor, conjugate, common denominator |
| 1^∞, 0⁰, ∞⁰ | Take logarithm: y = f^g → ln y = g · ln f |

### 1.5 L'Hôpital's Rule

If `lim f(x)/g(x)` is 0/0 or ∞/∞, then:
`lim f(x)/g(x) = lim f'(x)/g'(x)` (provided RHS exists).

**Apply repeatedly** as long as the form remains indeterminate.

### 1.6 Continuity

**f is continuous at x = a** iff:
1. f(a) is defined.
2. `lim_{x→a} f(x)` exists.
3. `lim_{x→a} f(x) = f(a)`.

If any of these fails — **discontinuity at a**.

**Types of discontinuity:**
- **Removable:** limit exists but ≠ f(a), or f(a) undefined.
- **Jump:** left and right limits exist but differ.
- **Infinite/Essential:** at least one one-sided limit is infinite or doesn't exist.

### 1.7 Standard Continuous Functions

- Polynomials, exponentials, sine, cosine — continuous on ℝ.
- log, √, tan, sec — continuous on their domain.
- Sums, differences, products, compositions of continuous functions are continuous.
- Quotient is continuous where denominator ≠ 0.

### 1.8 Intermediate Value Theorem (IVT)

If f is continuous on [a, b] and N is between f(a) and f(b), then ∃ c ∈ [a, b] with f(c) = N.

**Use:** prove existence of root.

### 1.9 Differentiability

**f is differentiable at x = a** iff:
`f'(a) = lim_{h→0} (f(a + h) − f(a))/h` exists.

Equivalently: `lim_{x→a} (f(x) − f(a))/(x − a)` exists.

**Differentiable ⇒ Continuous** (but not conversely; e.g., |x| at 0).

### 1.10 Rules of Differentiation

| Rule | Form |
|---|---|
| Sum/Difference | (f ± g)' = f' ± g' |
| Product | (fg)' = f'g + fg' |
| Quotient | (f/g)' = (f'g − fg')/g² |
| Chain | (f(g(x)))' = f'(g(x))·g'(x) |
| Power | (xⁿ)' = n·x^(n−1) |
| Constant | c' = 0 |

### 1.11 Standard Derivatives

| f(x) | f'(x) |
|---|---|
| sin x | cos x |
| cos x | −sin x |
| tan x | sec² x |
| sec x | sec x · tan x |
| cot x | −csc² x |
| csc x | −csc x · cot x |
| eˣ | eˣ |
| aˣ | aˣ · ln a |
| ln x | 1/x |
| log_a x | 1/(x ln a) |
| sin⁻¹ x | 1/√(1 − x²) |
| cos⁻¹ x | −1/√(1 − x²) |
| tan⁻¹ x | 1/(1 + x²) |
| sinh x | cosh x |
| cosh x | sinh x |

### 1.12 Higher-Order Derivatives

`f^(n)(x)` = n-th derivative. Useful for Taylor series.

**Leibniz rule:** `(fg)^(n) = Σ C(n, k) · f^(k) · g^(n−k)`.

### 1.13 Implicit & Parametric Differentiation

**Implicit:** differentiate both sides w.r.t. x, treat y as y(x). Solve for dy/dx.

**Parametric** (x = f(t), y = g(t)): `dy/dx = (dy/dt)/(dx/dt)`.

### 1.14 Continuity vs Differentiability — Summary

```
                differentiable ⇒ continuous
                NOT continuous ⇒ NOT differentiable
                continuous ⇒ NOT necessarily differentiable
                |x| is continuous at 0 but not differentiable
```

### 1.15 Taylor & Maclaurin (essentials)

**Taylor:** `f(x) = Σ f^(n)(a)/n! · (x − a)ⁿ`.
**Maclaurin** (a = 0): expansion around 0.

| f(x) | Series |
|---|---|
| eˣ | 1 + x + x²/2! + x³/3! + … |
| sin x | x − x³/3! + x⁵/5! − … |
| cos x | 1 − x²/2! + x⁴/4! − … |
| ln(1+x) | x − x²/2 + x³/3 − … (\|x\| < 1) |
| (1+x)ⁿ | 1 + nx + n(n−1)/2! x² + … |
| 1/(1−x) | 1 + x + x² + x³ + … |

> **Summary:** Memorize standard limits, L'Hôpital, continuity definition, differentiability ⇒ continuity, derivative rules. The same patterns recur across years.

---

## 2. Important Points

- **Limit exists ⇔ left = right limits.**
- **Continuity at a:** limit exists AND equals f(a).
- **Differentiable ⇒ continuous; converse not true.**
- |x| is continuous everywhere, **not differentiable at 0**.
- A function with a jump discontinuity is **not** differentiable there.
- L'Hôpital applies **only** to 0/0 and ∞/∞ — convert other forms first.
- `lim_{x→a} f(g(x))` is `f(lim g(x))` only if f is **continuous at lim g(x)**.
- **Squeeze theorem:** if g(x) ≤ f(x) ≤ h(x) and g, h have same limit, so does f.
- IVT proves **existence** of root, not uniqueness.
- A polynomial of odd degree always has a real root (IVT).
- **Differentiability twice** (C²) is required for second derivative test.
- Sum, product, composition of differentiable functions is differentiable.
- **Inverse function rule:** (f⁻¹)'(y) = 1 / f'(x) where y = f(x).
- A **continuous function on a closed interval** [a,b] attains its max and min (Extreme Value Theorem).
- **Removable discontinuities** can be patched by redefining f(a).

---

## 3. Short Notes

```
LIMIT
 lim_{x→a} f(x) = L
 exists ⇔ left = right
 ε–δ definition

PROPERTIES
 lim(f±g) = L±M
 lim(fg) = LM
 lim(f/g) = L/M (M≠0)

STANDARD LIMITS
 sin x / x → 1     (1−cos x)/x² → 1/2
 tan x / x → 1
 (eˣ−1)/x → 1
 (aˣ−1)/x → ln a
 ln(1+x)/x → 1
 (1+x)^(1/x) → e
 (1+1/x)ˣ → e
 (xⁿ−aⁿ)/(x−a) → n·a^(n−1)

INDETERMINATE FORMS
 0/0, ∞/∞ → L'Hôpital
 0·∞   → rewrite as 0/0
 ∞−∞   → common denom or factor
 1^∞, 0⁰, ∞⁰ → take ln

L'HÔPITAL
 0/0 or ∞/∞ : f/g → f'/g'

CONTINUITY at a
 1) f(a) defined
 2) lim exists
 3) lim = f(a)
 types: removable, jump, infinite

DIFFERENTIABILITY
 f'(a) = lim_{h→0} (f(a+h)−f(a))/h
 differentiable ⇒ continuous
 |x| at 0: continuous, not differentiable

DERIV RULES
 (fg)' = f'g + fg'
 (f/g)' = (f'g − fg')/g²
 chain: f(g(x))' = f'(g(x))g'(x)
 implicit, parametric

DERIVATIVES (memorize)
 sin → cos, cos → −sin, tan → sec²
 eˣ → eˣ, aˣ → aˣ ln a
 ln x → 1/x, sin⁻¹x → 1/√(1−x²), tan⁻¹x → 1/(1+x²)

TAYLOR
 f(x) = Σ f^(n)(a)/n! · (x−a)ⁿ
 eˣ = Σ xⁿ/n!
 sin x = x − x³/3! + …
 ln(1+x) = x − x²/2 + x³/3 − …

THEOREMS
 IVT: f cts on [a,b], N between f(a),f(b) ⇒ ∃c
 EVT: f cts on [a,b] ⇒ attains max and min
 Squeeze: g ≤ f ≤ h, g,h same limit ⇒ same
```

---

## 4. Formulas / Tricks

| # | Formula / Rule | Memorize Cold? |
|---|---|---|
| 1 | sin x / x → 1 (x → 0) | ✅✅✅ |
| 2 | (1 − cos x)/x² → 1/2 | ✅✅ |
| 3 | (eˣ − 1)/x → 1 | ✅✅ |
| 4 | ln(1 + x)/x → 1 | ✅✅ |
| 5 | (1 + 1/x)ˣ → e (x → ∞) | ✅✅ |
| 6 | L'Hôpital: f/g → f'/g' (0/0, ∞/∞) | ✅✅ |
| 7 | Squeeze theorem | ✅ |
| 8 | Differentiable ⇒ continuous | ✅✅ |
| 9 | Chain rule | ✅✅ |
| 10 | Product rule | ✅✅ |
| 11 | Quotient rule | ✅✅ |
| 12 | Standard derivatives table (sin, cos, tan, e, ln, inverse trig) | ✅✅ |
| 13 | (f⁻¹)'(y) = 1/f'(x) | ✅ |
| 14 | Taylor expansion of eˣ, sin, cos, ln(1+x) | ✅ |
| 15 | IVT — existence of root | ✅ |

### Tricks

- **For 1^∞ form:** rewrite `f^g = e^(g ln f)`, expand, evaluate.
- **For ∞ − ∞ involving roots:** multiply by conjugate.
- **For sin/x style limits with composite argument:** `sin(kx)/x → k`, `sin(kx)/(kx) → 1`.
- **For tan(x) − sin(x) at 0:** use Taylor — leading term is x³/2.
- **Quick continuity test:** check left/right limits at every "joint" of piecewise functions.
- **Differentiability at piecewise junction:** compute left and right derivatives separately; if equal, differentiable there.
- **For implicit dy/dx, simplify before solving** — saves algebra.
- **Series shortcut:** for limits like `(1 − cos x − x²/2)/x⁴`, expand cos to higher orders.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
`lim_{x→0} (sin x)/x = ?`
**Solution.** = 1 (standard).

### Q2. (GATE CSE 2014)
`lim_{x→0} (1 − cos x)/x² = ?`
**Solution.** = 1/2.

### Q3. (GATE CSE 2010)
`lim_{x→0} (e^(2x) − 1)/x = ?`
**Solution.** = 2 (using (eˣ−1)/x → 1).

### Q4. (GATE CSE 2018)
`lim_{x→∞} (1 + 1/x)^(2x) = ?`
**Solution.** = e².

### Q5. (GATE CSE 2015)
The function f(x) = |x| is:
**Solution.** Continuous everywhere; not differentiable at x = 0.

### Q6. (GATE CSE 2008)
`lim_{x→0} (tan x − sin x)/x³ = ?`
**Solution.** Use Taylor: tan x ≈ x + x³/3, sin x ≈ x − x³/6. Difference = x³/3 + x³/6 = x³/2. Limit = 1/2.

### Q7. (GATE CSE 2013)
f(x) = x² sin(1/x) for x ≠ 0, f(0) = 0. Is f differentiable at 0?
**Solution.** f'(0) = lim h sin(1/h) = 0 (squeeze). Yes, differentiable.

### Q8. (GATE CSE 2007)
`lim_{x→1} (xⁿ − 1)/(x − 1) = ?`
**Solution.** = n.

### Q9. (GATE CSE 2003)
The derivative of x^x w.r.t. x is:
**Solution.** Let y = x^x; ln y = x ln x; (1/y) y' = ln x + 1; y' = x^x (ln x + 1).

### Q10. (GATE CSE 2009)
f(x) = x for x ≤ 1, x² for x > 1. Is f continuous at x = 1?
**Solution.** Left = 1, right = 1, f(1) = 1. Yes.
Is f differentiable? f'(1−) = 1, f'(1+) = 2. Not differentiable.

### Q11. (GATE CSE 2019)
`lim_{x→0} (sin(2x))/(sin(3x)) = ?`
**Solution.** = (2x)/(3x) (small x) = 2/3.

### Q12. (GATE CSE 2020)
`lim_{x→∞} (x − √(x² − x)) = ?`
**Solution.** Multiply by conjugate: x²−(x²−x) over (x + √(x²−x)) = x / (x + x√(1−1/x)) → 1/2.

### Q13. (GATE CSE 2021)
The number of points where f(x) = |x| + |x − 1| is non-differentiable:
**Solution.** At x = 0 and x = 1. Answer: **2**.

### Q14. (GATE CSE 2016)
`lim_{x→0} x · cot x = ?`
**Solution.** = lim (x cos x / sin x) = (lim cos x) · (lim x/sin x) = 1 · 1 = 1.

### Q15. (GATE CSE 2011)
For what value of a is f(x) = `(x²−1)/(x−1) for x ≠ 1, a for x = 1` continuous?
**Solution.** lim = (x+1) → 2. So a = 2.

---

## 6. Practice Questions (20+)

### Easy

**P1.** `lim_{x→0} sin(5x)/x`.

**P2.** `lim_{x→0} (1 − cos(2x))/x²`.

**P3.** Derivative of x⁵ + 3x² + 7.

**P4.** Derivative of sin(2x).

**P5.** Derivative of e^(3x).

**P6.** Derivative of ln(x² + 1).

**P7.** Is f(x) = x² continuous everywhere?

**P8.** Is f(x) = 1/x continuous at x = 0?

**P9.** Differentiate y = x · sin(x).

**P10.** Differentiate y = (1 + x²)¹⁰.

### Medium

**P11.** `lim_{x→0} (e^x − 1 − x)/x²`.

**P12.** `lim_{x→0} (sin x − x)/x³`.

**P13.** Differentiate y = sin(cos(x)).

**P14.** Find dy/dx if x² + y² = 25.

**P15.** Is f(x) = x|x| differentiable at 0? Find f'(0).

**P16.** `lim_{x→∞} (x ln(1 + 1/x))`.

**P17.** Differentiate y = x^x.

**P18.** For f(x) = `kx + 1, x ≤ 2; 3x − 1, x > 2`, find k for continuity at 2.

**P19.** `lim_{x→0} (1 + 2x)^(1/x)`.

**P20.** Differentiate y = arctan(x²).

### Hard

**P21.** `lim_{x→0} (cos(ax) − cos(bx))/x²`.

**P22.** `lim_{x→∞} (x^(1/x))`.

**P23.** Show that f(x) = x² sin(1/x) (with f(0) = 0) is differentiable at 0 but f' is not continuous at 0.

**P24.** Let f(x) = `e^(−1/x²), x ≠ 0; 0, x = 0`. Show f is C^∞ but f^(n)(0) = 0 for all n.

**P25.** Find max value of f(x) = sin(x) + cos(x).

**P26.** `lim_{n→∞} n · sin(1/n)`.

**P27.** Show `lim_{x→0} x · sin(1/x) = 0` using squeeze.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 5 | sin(kx)/x → k |
| P2 | 2 | (1−cos 2x)/x² = 2(1−cos 2x)/(2x)² · 2 |
| P3 | 5x⁴ + 6x | power rule |
| P4 | 2 cos(2x) | chain |
| P5 | 3e^(3x) | chain |
| P6 | 2x/(x²+1) | chain |
| P7 | Yes | polynomial |
| P8 | No | f(0) undefined |
| P9 | sin x + x cos x | product |
| P10 | 20x(1+x²)⁹ | chain |
| P11 | 1/2 | Taylor |
| P12 | −1/6 | sin x ≈ x − x³/6 |
| P13 | cos(cos x) · (−sin x) | chain |
| P14 | dy/dx = −x/y | implicit |
| P15 | f'(0) = 0; differentiable | f = x² for x>0, −x² for x<0 |
| P16 | 1 | ln(1+1/x) ≈ 1/x |
| P17 | x^x (1 + ln x) | log diff |
| P18 | 2k+1 = 5 ⇒ k = 2 | continuity |
| P19 | e² | (1+ax)^(1/x) → eᵃ |
| P20 | 2x/(1+x⁴) | chain |
| P21 | (b² − a²)/2 | Taylor |
| P22 | 1 | take log: (ln x)/x → 0 |
| P23 | f'(0) by definition = 0; f'(x)=2x sin(1/x) − cos(1/x) — limit DNE | direct |
| P24 | iterative differentiation; all powers vanish | Taylor pathological |
| P25 | √2 | f = √2 sin(x + π/4) |
| P26 | 1 | sin(1/n)/(1/n) → 1 |
| P27 | −x ≤ x sin(1/x) ≤ x → 0 | squeeze |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Applying L'Hôpital to non-indeterminate forms | Verify form is 0/0 or ∞/∞ first. |
| 2 | Treating limit as = function value | f may not be defined or limit ≠ f(a). |
| 3 | Forgetting differentiable ⇒ continuous (one-way) | Continuous does NOT imply differentiable. |
| 4 | Quotient rule sign | f'g − fg' (numerator), not g' f − f' g. |
| 5 | Chain rule missing inner derivative | Always multiply by g'(x). |
| 6 | Applying squeeze to oscillating function unbounded | Bound must squeeze to same limit. |
| 7 | L'Hôpital infinite loop | Switch strategy after 2–3 applications (use Taylor). |
| 8 | Differentiating |x| as 1 | At x = 0, |x| not differentiable. |
| 9 | Confusing one-sided and two-sided limit | Always check both. |
| 10 | Treating composition limit as inside-out without continuity | Need outer fn continuous at inner limit. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Limit at a point with sin/cos/exp" | Standard limits or Taylor. |
| "0/0 form" | L'Hôpital or factor or Taylor. |
| "1^∞" | Take log, exponentiate. |
| "Continuous at piecewise junction?" | Match left = right = f(a). |
| "Differentiable at piecewise junction?" | Match left and right derivatives. |
| "Find a, b for continuity / differentiability" | Equate limit conditions. |
| "Behavior at x → ∞" | Divide by highest power, or substitute t = 1/x. |
| "|x − a| or |f(x)|" | Likely non-differentiable at a. |
| "Existence of root" | IVT. |
| "Oscillating × bounded" | Squeeze theorem. |

---

## 9. Quick Revision

```
LIMIT exists ⇔ left = right
sin x / x → 1     (1−cos x)/x² → 1/2
(eˣ−1)/x → 1     (aˣ−1)/x → ln a
ln(1+x)/x → 1
(1+1/x)ˣ → e   (1+ax)^(1/x) → eᵃ
tan x / x → 1
(xⁿ−aⁿ)/(x−a) → n a^(n−1)

L'HÔPITAL: 0/0 or ∞/∞ → f'/g'
Squeeze: g ≤ f ≤ h same limit

CONTINUITY: f(a) defined, lim exists, lim = f(a)
DIFFERENTIABLE ⇒ CONTINUOUS (not converse)
|x| cts everywhere, not diff at 0
piecewise: check left/right limits & derivatives

DERIVATIVES
 (sin x)' = cos x      (cos x)' = −sin x
 (tan x)' = sec² x     (eˣ)' = eˣ
 (ln x)' = 1/x         (aˣ)' = aˣ ln a
 (sin⁻¹ x)' = 1/√(1−x²)
 (tan⁻¹ x)' = 1/(1+x²)

PRODUCT (fg)' = f'g + fg'
QUOTIENT (f/g)' = (f'g − fg')/g²
CHAIN (f(g))' = f'(g)·g'

TAYLOR
 eˣ = Σ xⁿ/n!
 sin x = x − x³/3! + x⁵/5! − …
 cos x = 1 − x²/2 + x⁴/24 − …
 ln(1+x) = x − x²/2 + x³/3 − …

THEOREMS: IVT, EVT, Squeeze, MVT (next file)
```
