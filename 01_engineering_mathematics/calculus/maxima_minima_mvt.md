# Maxima/Minima & Mean Value Theorems

> Subject: Engineering Mathematics → Calculus
> GATE weight: **1–3 marks** every year. Optimization, MVT, Rolle, Taylor.

---

## 1. Concept Explanation

### 1.1 Critical Points

For f(x) on interval I, **critical point** c ∈ I means:
- f'(c) = 0, **or**
- f'(c) does not exist (cusp / corner / vertical tangent).

All local extrema of differentiable f occur at critical points (Fermat's Theorem).

### 1.2 Local vs Global Extrema

- **Local maximum** at c: f(c) ≥ f(x) for x in some open neighborhood of c.
- **Local minimum** at c: f(c) ≤ f(x) similarly.
- **Global (absolute) max/min** on [a, b]: largest/smallest f-value in entire interval.

By **Extreme Value Theorem (EVT):** continuous f on [a, b] attains both global max and min.

### 1.3 Tests for Local Extrema

**First Derivative Test:**
- f'(c) = 0 (or undefined).
- f' changes sign + → − at c ⇒ local max.
- f' changes sign − → + at c ⇒ local min.
- No sign change ⇒ saddle / inflection.

**Second Derivative Test:**
- f'(c) = 0 and f''(c) > 0 ⇒ local min.
- f'(c) = 0 and f''(c) < 0 ⇒ local max.
- f''(c) = 0 ⇒ inconclusive (use higher derivatives or first-derivative test).

### 1.4 Procedure for Global Extrema on [a, b]

1. Find all critical points in (a, b).
2. Evaluate f at critical points and at endpoints a, b.
3. Largest value = global max; smallest = global min.

### 1.5 Concavity & Inflection Points

- f''(x) > 0 ⇒ **concave up** (cup-shaped).
- f''(x) < 0 ⇒ **concave down**.
- **Inflection point**: where concavity changes sign (f'' changes sign).

### 1.6 Rolle's Theorem

If f is:
1. Continuous on [a, b].
2. Differentiable on (a, b).
3. f(a) = f(b).

Then ∃ c ∈ (a, b) with `f'(c) = 0`.

### 1.7 Mean Value Theorem (MVT, Lagrange)

If f is:
1. Continuous on [a, b].
2. Differentiable on (a, b).

Then ∃ c ∈ (a, b) with:

`f'(c) = (f(b) − f(a))/(b − a)`

Geometric: a tangent line is parallel to the chord.

### 1.8 Cauchy's Mean Value Theorem (Generalized MVT)

If f, g continuous on [a,b], differentiable on (a,b), and g'(x) ≠ 0:

`(f(b) − f(a))/(g(b) − g(a)) = f'(c)/g'(c)` for some c ∈ (a,b).

### 1.9 Taylor's Theorem

For f differentiable n+1 times on (a, b) and x₀ ∈ (a, b):

`f(x) = Σ_{k=0}^n f^(k)(x₀)/k! · (x − x₀)ᵏ + R_n(x)`

where remainder `R_n(x) = f^(n+1)(ξ)/(n+1)! · (x − x₀)^(n+1)` for some ξ between x₀ and x.

**Maclaurin** = Taylor at x₀ = 0.

### 1.10 Multivariable Optimization (essentials for GATE)

For `f(x, y)`:

**Critical points:** `∂f/∂x = 0` and `∂f/∂y = 0`.

**Hessian** `H = [[fxx, fxy],[fxy, fyy]]`.

**Discriminant** `D = fxx·fyy − fxy²`.

| D > 0 and fxx > 0 | Local minimum |
|---|---|
| D > 0 and fxx < 0 | Local maximum |
| D < 0 | Saddle point |
| D = 0 | Inconclusive |

### 1.11 Lagrange Multipliers

Optimize f(x, y) subject to g(x, y) = c:
`∇f = λ ∇g` along with `g(x, y) = c`.

### 1.12 Word-Problem Optimization Recipe

1. Identify variables and the quantity to optimize.
2. Write objective function.
3. Write constraint(s).
4. Reduce to one variable (substitute) or use Lagrange.
5. Find critical points.
6. Verify with 1st/2nd derivative test.
7. Check endpoints / domain.

> **Summary:** Critical points come from f' = 0 or undefined. 1st/2nd derivative tests classify. MVT and Rolle assert existence — they're for proofs and applications. Taylor gives polynomial approximation + error bound.

---

## 2. Important Points

- **Fermat:** local extremum ⇒ critical point (necessary, not sufficient).
- **Endpoints can be extrema** even if f' ≠ 0 there.
- f''(c) = 0 does **not** mean inflection; check sign change.
- **Saddle point** in single-variable: critical point that's neither max nor min (uncommon — usually inflection).
- **Strict vs non-strict** extrema: be careful with constant pieces.
- For closed bounded interval, EVT guarantees max/min exist.
- For open interval / unbounded domain, max/min may not exist.
- **MVT is for differentiable functions only**, not just continuous ones.
- Rolle is a special case of MVT with f(a) = f(b).
- For Lagrange: first verify constraint is a regular surface (∇g ≠ 0).
- The **Hessian determinant** sign decides max/min vs saddle in 2 variables.
- Taylor remainder bound: `|R_n| ≤ M · |x − x₀|^(n+1) / (n+1)!` where M = max |f^(n+1)|.
- **Concave up + concave down = inflection** if both happen at the same point.
- **Symmetry shortcut:** for symmetric f, extrema at center of symmetry.

---

## 3. Short Notes

```
CRITICAL POINTS
 f'(c) = 0 OR f'(c) undefined
 Fermat: local extremum ⇒ critical (necessary)

FIRST DERIVATIVE TEST
 f' : + → −  ⇒ local max
 f' : − → +  ⇒ local min
 no sign change ⇒ inflection

SECOND DERIVATIVE TEST
 f'(c)=0, f''(c) > 0 ⇒ local min
 f'(c)=0, f''(c) < 0 ⇒ local max
 f''(c)=0 ⇒ inconclusive

GLOBAL EXTREMA on [a,b]
 1) critical pts in (a,b)
 2) endpoints a, b
 3) compare

CONCAVITY
 f''>0: concave up
 f''<0: concave down
 inflection: f'' changes sign

ROLLE  (f cts [a,b], diff (a,b), f(a)=f(b))
 ∃ c: f'(c) = 0

MVT (LAGRANGE)
 ∃ c: f'(c) = (f(b)−f(a))/(b−a)

CAUCHY MVT
 (f(b)−f(a))/(g(b)−g(a)) = f'(c)/g'(c)

TAYLOR
 f(x) = Σ f^(k)(x₀)/k! (x−x₀)ᵏ + Rₙ
 Rₙ = f^(n+1)(ξ)/(n+1)! · (x−x₀)^(n+1)

MULTIVARIABLE
 ∂f/∂x = 0, ∂f/∂y = 0
 D = fxx·fyy − fxy²
 D>0, fxx>0: min
 D>0, fxx<0: max
 D<0: saddle
 D=0: inconclusive

LAGRANGE MULT
 ∇f = λ ∇g, g = c

WORD PROBLEMS
 1) variables, objective
 2) constraints
 3) reduce to one var or Lagrange
 4) f'=0
 5) verify (2nd deriv)
 6) check endpoints
```

---

## 4. Formulas / Tricks

| # | Rule / Formula | Memorize Cold? |
|---|---|---|
| 1 | f'(c) = 0 ⇒ critical point | ✅✅ |
| 2 | 2nd derivative test (sign of f'') | ✅✅ |
| 3 | EVT: continuous on [a,b] ⇒ attains max, min | ✅ |
| 4 | Rolle: f(a)=f(b) ⇒ ∃ c with f'(c)=0 | ✅✅ |
| 5 | MVT: f'(c) = (f(b)−f(a))/(b−a) | ✅✅ |
| 6 | Cauchy MVT for ratios | ✅ |
| 7 | Taylor remainder | ✅ |
| 8 | Hessian D = fxx·fyy − fxy² | ✅✅ |
| 9 | Lagrange ∇f = λ ∇g | ✅ |
| 10 | Inflection: f'' sign change | ✅ |

### Tricks

- **Closed interval:** always check endpoints.
- **Symmetric polynomials:** extrema at center.
- **For optimization with one constraint:** substitute, single-variable optimize.
- **For "minimize fence/area/cost":** check which variable is constrained, write objective in terms of free variable.
- **MVT applications:** prove inequalities like `|sin x − sin y| ≤ |x − y|`.
- **Rolle's theorem trick:** if f has 2 zeros, f' has at least one zero between them. By induction, polynomial of degree n has at most n real roots.
- **For multivariable saddle:** D < 0 ⇒ saddle, no further test needed.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Find local extrema of f(x) = x³ − 3x² + 4 on [0, 3].
**Solution.** f'(x) = 3x² − 6x = 3x(x − 2). Critical: 0, 2. f(0)=4, f(2)=0, f(3)=4. Global min = 0 at x=2; global max = 4 at x=0 or x=3.

### Q2. (GATE CSE 2014)
The maximum value of f(x) = x · (1 − x) on [0, 1]:
**Solution.** f' = 1 − 2x = 0 ⇒ x = 1/2; f(1/2) = 1/4.

### Q3. (GATE CSE 2008)
A function f(x) = x³ − 6x² + 9x + 1 has local max at:
**Solution.** f' = 3x² − 12x + 9 = 3(x−1)(x−3). f''(1) = 6 − 12 = −6 < 0 ⇒ local max at x = 1.

### Q4. (GATE CSE 2018)
For f(x) = x⁴ − 4x³, find inflection points:
**Solution.** f''(x) = 12x² − 24x = 12x(x − 2). Sign changes at 0 and 2. **Inflection points at x = 0, 2.**

### Q5. (GATE CSE 2010)
Apply Rolle's theorem to f(x) = x² − 4x + 3 on [1, 3]:
**Solution.** f(1) = 0 = f(3). f'(x) = 2x − 4 = 0 ⇒ x = 2.

### Q6. (GATE CSE 2015)
For f(x) = x² on [0, 2], find c by MVT:
**Solution.** f'(c) = (f(2) − f(0))/(2 − 0) = (4 − 0)/2 = 2; f'(c) = 2c = 2 ⇒ c = 1.

### Q7. (GATE CSE 2003)
The minimum value of f(x) = x² + 2x + 5:
**Solution.** f' = 2x + 2 = 0 ⇒ x = −1. f(−1) = 1 − 2 + 5 = 4.

### Q8. (GATE CSE 2007)
For Taylor expansion of e^x around 0 up to 2nd order, eˣ ≈ 1 + x + x²/2. Error in approximating e^(0.1):
**Solution.** R₂ = e^ξ · 0.001/6 for some ξ ∈ (0, 0.1). Bound by e^(0.1) · 0.001/6 ≈ 1.84 × 10⁻⁴.

### Q9. (GATE CSE 2009)
A rectangle has perimeter 20 m. What dimensions maximize area?
**Solution.** 2(l + w) = 20 ⇒ l + w = 10. Area = lw = l(10−l). dA/dl = 10 − 2l = 0 ⇒ l = 5. Square 5×5, area = 25.

### Q10. (GATE CSE 2013)
f(x, y) = x² + y² − 4x − 6y + 13. Local extremum?
**Solution.** ∂x = 2x − 4 = 0 ⇒ x=2; ∂y = 2y − 6 = 0 ⇒ y = 3. fxx=2, fyy=2, fxy=0. D = 4 > 0, fxx > 0 ⇒ local min.

### Q11. (GATE CSE 2011)
Number of real roots of `f(x) = x³ − 3x + 1`:
**Solution.** f' = 3x² − 3 = 0 ⇒ x = ±1. f(−1) = 3, f(1) = −1. Both extrema have opposite signs ⇒ **3 real roots**.

### Q12. (GATE CSE 2019)
For f(x) = ln(x) on [1, e], find c by MVT:
**Solution.** f(e)−f(1) = 1, b−a = e−1; f'(c) = 1/c = 1/(e−1) ⇒ c = e − 1.

### Q13. (GATE CSE 2020)
Maximum value of x · y subject to x + y = 4, x, y > 0:
**Solution.** Lagrange or substitute: y = 4 − x; xy = x(4−x); max at x = 2 ⇒ max = 4.

### Q14. (GATE CSE 2021)
The function f(x) = x − sin(x) on ℝ is:
(A) increasing  (B) decreasing  (C) constant  (D) neither

**Solution.** f'(x) = 1 − cos(x) ≥ 0 ⇒ non-decreasing; strictly increasing.

### Q15. (GATE CSE 2016)
Saddle point of f(x, y) = x² − y²:
**Solution.** ∂x = 2x = 0, ∂y = −2y = 0 ⇒ (0, 0). D = (2)(−2) − 0 = −4 < 0 ⇒ saddle.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Find critical points of f(x) = x² − 4x + 5.

**P2.** Find local max of f(x) = −x² + 6x − 5.

**P3.** Find global min of f(x) = x³ − 12x on [−2, 2].

**P4.** Find inflection points of f(x) = x³.

**P5.** State Rolle's theorem.

**P6.** Verify MVT for f(x) = x² on [0, 4].

**P7.** Maximum value of sin(x) on ℝ.

**P8.** Minimum value of x² + y² with constraint x + y = 1.

**P9.** Is x³ increasing on ℝ?

**P10.** Find local extrema of f(x) = x · eˣ.

### Medium

**P11.** A box with square base and open top has volume 32. Minimize surface area.

**P12.** Find absolute extrema of f(x) = x · ln(x) on [1, e].

**P13.** Find the extrema of f(x, y) = x² + y² − 2x − 4y + 5.

**P14.** Use Taylor to approximate sin(0.1) up to 3rd order; bound error.

**P15.** Find c in MVT for f(x) = √x on [1, 4].

**P16.** Number of real roots of x³ − 6x² + 9x + 2 = 0?

**P17.** Find max of f(x, y) = xy with x + 2y = 8, x, y > 0.

**P18.** Find inflection points of f(x) = x⁴ − 6x².

**P19.** Apply Cauchy MVT to f = sin x, g = cos x on [0, π/2].

**P20.** Find local extrema of f(x) = sin(x) + cos(x) on [0, 2π].

### Hard

**P21.** Find the rectangle of maximum area inscribed in a circle of radius r.

**P22.** Show using MVT: |sin x − sin y| ≤ |x − y|.

**P23.** Find minimum of f(x, y) = x² + y² subject to x + y + z = 1, xyz = 1 (Lagrange or elimination).

**P24.** A wire of length 10 is cut into two pieces; one is bent into a square, the other into a circle. Where to cut to minimize total area? maximize?

**P25.** Show: x³ − 3x has exactly one real root in (1, 2).

**P26.** Find max value of x + y + z subject to x² + y² + z² = 12.

**P27.** Apply Taylor to ln(1.1) up to 4th order; bound error.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | x = 2 (min) | f'=2x−4 |
| P2 | x = 3, max = 4 | parabola |
| P3 | f(2)= −16, f(−2) = 16; min = −16 | end + critical |
| P4 | x = 0 | f''=6x changes sign |
| P5 | as in 1.6 | direct |
| P6 | f'(c) = 4 ⇒ 2c = 4 ⇒ c = 2 | direct |
| P7 | 1 | sin bound |
| P8 | 1/2 | Lagrange |
| P9 | Yes | f'=3x²≥0 |
| P10 | f' = eˣ(1+x) = 0 ⇒ x=−1; min | product |
| P11 | x²·h = 32; A = x² + 4xh; minimize → x=4, h=2; A=48 | optimization |
| P12 | f' = ln x + 1 = 0 ⇒ x=1/e (outside [1,e]). Endpoints: f(1) = 0, f(e)=e. min=0, max=e | endpoint check |
| P13 | (1,2), value −1; min (D>0, fxx>0) | direct |
| P14 | sin(0.1) ≈ 0.1 − 0.001/6 ≈ 0.09983; error ≤ 0.1⁵/120 | Taylor |
| P15 | f'(c) = 1/(2√c) = 1/3 ⇒ c = 9/4 | direct |
| P16 | 3 real roots — check sign of extrema | f' factor |
| P17 | y = 2; x = 4; max = 8 | Lagrange |
| P18 | x = ±1 | f''=12x²−12 |
| P19 | sin(π/2)−sin 0 = 1; cos(π/2)−cos 0 = −1; ratio −1 = cot c | direct |
| P20 | x = π/4 max √2; x = 5π/4 min −√2 | derivative |
| P21 | side 2r/√2; max area = 2r² (square) | constraint optimization |
| P22 | apply MVT to sin: ∃c, sin x − sin y = (x−y)·cos c, |cos c|≤1 | MVT |
| P23 | use Lagrange to derive constraint then minimize | substitution |
| P24 | Set up A(x); take derivative; min when one piece longer | calculus |
| P25 | f(1) = −2 < 0, f(2) = 2 > 0, IVT; f' > 0 on (1,2) | IVT + monotonic |
| P26 | by Cauchy-Schwarz, max = √(3·12) = 6 | inequality |
| P27 | ln(1.1) ≈ 0.1 − 0.005 + ... | Taylor |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting endpoints on closed interval | Always evaluate f at endpoints. |
| 2 | Treating f'' = 0 as inflection | Inflection requires sign change. |
| 3 | Using Rolle without checking f(a) = f(b) | All three hypotheses needed. |
| 4 | Applying MVT to non-differentiable function | Differentiability on (a,b) is required. |
| 5 | Forgetting strict vs non-strict in inequalities | "Increasing" can be strict or non-strict. |
| 6 | Saddle in multivariable misclassified as inflection | Use Hessian discriminant. |
| 7 | Lagrange without verifying ∇g ≠ 0 | Check that constraint is regular. |
| 8 | Taylor remainder used as approximation | It's an error bound, not the function. |
| 9 | Optimization domain off | Some critical points fall outside problem's domain. |
| 10 | Treating "max" as one specific x value | Could be at endpoints, multiple points, or unbounded. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Local max / min of f(x)" | f'(x) = 0; 2nd derivative test. |
| "Global max / min on [a, b]" | Critical points + endpoints. |
| "Inflection points" | f''(x) = 0 + sign change. |
| "Apply Rolle / MVT" | Verify hypotheses, find c. |
| "Optimization word problem" | Define vars, objective, constraint, reduce to 1 var. |
| "Constrained optimization" | Lagrange or substitute. |
| "Multivariable extrema" | Set ∂f/∂x = 0, ∂f/∂y = 0; Hessian. |
| "Inequality proof using calculus" | Apply MVT or monotonicity. |
| "Number of real roots of polynomial" | Use Rolle / IVT / discriminant. |
| "Bound error of Taylor approximation" | Use remainder formula. |

---

## 9. Quick Revision

```
CRITICAL POINTS: f'(c) = 0 or undefined

1st-deriv test
 + → − : local max
 − → + : local min
 no change: inflection

2nd-deriv test (f'(c)=0)
 f''(c) > 0 : local min
 f''(c) < 0 : local max
 f''(c) = 0 : inconclusive

GLOBAL on [a,b]
 critical + endpoints

CONCAVE up: f''>0
inflection: f'' sign change

ROLLE: f(a)=f(b), cts, diff ⇒ ∃c f'(c)=0
MVT: f'(c) = (f(b)−f(a))/(b−a)
CAUCHY MVT: ratio version

TAYLOR
 f(x) = Σ f^(k)(x₀)/k! (x−x₀)ᵏ + Rₙ
 |Rₙ| ≤ M |x−x₀|^(n+1)/(n+1)!

MULTIVARIABLE
 ∂x = ∂y = 0
 D = fxx·fyy − fxy²
 D>0, fxx>0: min
 D>0, fxx<0: max
 D<0: saddle

LAGRANGE: ∇f = λ ∇g, g = c

WORD: vars → obj → constr → reduce → f'=0 → verify
```
