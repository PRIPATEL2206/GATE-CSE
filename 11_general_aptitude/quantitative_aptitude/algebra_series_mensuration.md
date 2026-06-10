# Algebra, Series & Mensuration

> Subject: General Aptitude — Quantitative
> GATE weight: **2–3 marks** every year. Linear/quadratic equations, AP/GP/HP, mensuration formulas.

---

## 1. Concept Explanation

### 1.1 Linear Equations

`ax + b = 0` → `x = −b/a`.

**System:**
- 2 unknowns: substitution / elimination / Cramer's rule.
- Infinite or no solution if equations dependent or inconsistent.

### 1.2 Quadratic Equation

`ax² + bx + c = 0`

**Quadratic formula:** `x = (−b ± √(b² − 4ac)) / 2a`.

**Discriminant** D = b² − 4ac:
- D > 0: 2 distinct real roots.
- D = 0: 1 repeated real root.
- D < 0: 2 complex roots.

**Vieta's formulas:**
- Sum of roots = −b/a.
- Product = c/a.

### 1.3 Polynomial Identities

| Identity |
|---|
| (a + b)² = a² + 2ab + b² |
| (a − b)² = a² − 2ab + b² |
| (a + b)(a − b) = a² − b² |
| (a + b)³ = a³ + 3a²b + 3ab² + b³ |
| (a − b)³ = a³ − 3a²b + 3ab² − b³ |
| a³ + b³ = (a + b)(a² − ab + b²) |
| a³ − b³ = (a − b)(a² + ab + b²) |
| a³ + b³ + c³ − 3abc = (a+b+c)(a² + b² + c² − ab − bc − ca) |

### 1.4 Inequalities

- Adding constant: preserve direction.
- Multiplying by positive: preserve.
- Multiplying by negative: **flip**.
- Squaring inequality: only if both sides non-negative.

### 1.5 AM ≥ GM ≥ HM

For positive numbers a, b:
- **AM** = (a + b)/2.
- **GM** = √(ab).
- **HM** = 2ab/(a + b).

**Equality iff a = b.**

For n numbers:
- AM = Σx_i / n.
- GM = (∏ x_i)^(1/n).
- HM = n / Σ(1/x_i).

### 1.6 Arithmetic Progression (AP)

`a, a+d, a+2d, …`

- **n-th term:** `a_n = a + (n−1)d`.
- **Sum of n terms:** `S_n = n/2 · (2a + (n−1)d) = n/2 · (a + a_n)`.
- **AM of AP:** middle term.

### 1.7 Geometric Progression (GP)

`a, ar, ar², …`

- **n-th term:** `a_n = a·r^(n−1)`.
- **Sum of n terms:** `S_n = a(rⁿ − 1)/(r − 1)` for r ≠ 1.
- **Sum to infinity (|r| < 1):** `S_∞ = a/(1 − r)`.
- **GM of GP:** geometric mean of two terms.

### 1.8 Harmonic Progression (HP)

Reciprocals form AP.
- **n-th term:** 1 / (a + (n−1)d).

### 1.9 Common Sums

| Sum | Formula |
|---|---|
| Σ k from 1 to n | n(n+1)/2 |
| Σ k² | n(n+1)(2n+1)/6 |
| Σ k³ | (n(n+1)/2)² |
| Σ (2k−1) (odds) | n² |
| Σ 2k (evens) | n(n+1) |

### 1.10 Mensuration: 2D Shapes

| Shape | Area | Perimeter |
|---|---|---|
| Square (s) | s² | 4s |
| Rectangle (l, w) | lw | 2(l+w) |
| Triangle (b, h) | (1/2)bh | sum of sides |
| Equilateral (s) | (√3/4)s² | 3s |
| Right (a, b) | (1/2)ab | a+b+√(a²+b²) |
| Circle (r) | πr² | 2πr |
| Sector (r, θ rad) | (1/2)r²θ | r(θ+2) |
| Parallelogram | bh | sum |
| Rhombus (d₁, d₂) | (1/2)d₁d₂ | 4·side |
| Trapezium (a, b, h) | (1/2)(a+b)h | sum of sides |
| Regular n-gon | (1/4)n·s²·cot(π/n) | n·s |

### 1.11 Heron's Formula (triangle from sides)

For a, b, c sides; s = (a+b+c)/2:
`Area = √(s(s−a)(s−b)(s−c))`.

### 1.12 Mensuration: 3D Shapes

| Solid | Volume | Surface Area |
|---|---|---|
| Cube (s) | s³ | 6s² |
| Cuboid (l, b, h) | lbh | 2(lb+bh+hl) |
| Cylinder (r, h) | πr²h | 2πr(r+h) |
| Cone (r, h, l) | (1/3)πr²h | πr(r+l), l = slant |
| Sphere (r) | (4/3)πr³ | 4πr² |
| Hemisphere | (2/3)πr³ | 3πr² (curved + base) |
| Prism | base area · h | 2·base + lateral |

### 1.13 Pythagorean Triples

Common: 3-4-5, 5-12-13, 8-15-17, 7-24-25, 20-21-29.

### 1.14 Coordinate Geometry Basics

- **Distance:** √((x₂−x₁)² + (y₂−y₁)²).
- **Midpoint:** ((x₁+x₂)/2, (y₁+y₂)/2).
- **Slope:** (y₂−y₁)/(x₂−x₁).
- **Line equation:** y − y₁ = m(x − x₁).

### 1.15 Trigonometry Basics

| Angle | sin | cos | tan |
|---|---|---|---|
| 0° | 0 | 1 | 0 |
| 30° | 1/2 | √3/2 | 1/√3 |
| 45° | √2/2 | √2/2 | 1 |
| 60° | √3/2 | 1/2 | √3 |
| 90° | 1 | 0 | ∞ |

**Identities:**
- sin² + cos² = 1.
- 1 + tan² = sec².
- 1 + cot² = csc².

### 1.16 Logarithms

`log_a(b) = log_c(b)/log_c(a)`.

| Property |
|---|
| log(ab) = log a + log b |
| log(a/b) = log a − log b |
| log(a^n) = n log a |
| log_a(a) = 1 |
| log_a(1) = 0 |

Default base 10 in aptitude.

### 1.17 Exponents

`a^m · a^n = a^(m+n)`
`a^m / a^n = a^(m−n)`
`(a^m)^n = a^(mn)`

### 1.18 Common Tricks

- For sum of AP, use (first + last)·n/2.
- For mensuration of compound shapes, decompose.
- For Pythagoras, recognize triples instantly.

> **Summary:** Master quadratic formula, polynomial identities, AP/GP/HP, common sums, mensuration 2D/3D formulas. Pythagorean triples save time.

---

## 2. Important Points

- **Discriminant** decides nature of roots.
- **AM ≥ GM ≥ HM**, equality iff all equal.
- AP n-th: a + (n−1)d.
- GP sum: a(rⁿ−1)/(r−1); infinite |r|<1: a/(1−r).
- Heron's formula uses semi-perimeter.
- Common Pythagorean triples should be memorized.
- Sphere volume: (4/3)πr³; surface 4πr².
- Cylinder volume: πr²h; surface: 2πr(r+h).
- log identities for fast computation.
- For coordinate geometry, distance and slope are basics.

---

## 3. Short Notes

```
QUADRATIC: ax² + bx + c = 0
 x = (−b ± √(b²−4ac))/2a
 sum = −b/a; product = c/a
 D > 0: 2 real; D = 0: 1; D < 0: complex

IDENTITIES
 (a±b)² = a² ± 2ab + b²
 a² − b² = (a+b)(a−b)
 (a+b)³, (a−b)³
 a³ ± b³

AM ≥ GM ≥ HM
 AM = (a+b)/2; GM = √(ab); HM = 2ab/(a+b)

AP
 a_n = a + (n−1)d
 S_n = n/2 (2a + (n−1)d) = n/2 (a + a_n)

GP
 a_n = a r^(n−1)
 S_n = a(rⁿ−1)/(r−1)
 S_∞ = a/(1−r), |r|<1

HP: reciprocals are AP

SUMS
 Σk = n(n+1)/2
 Σk² = n(n+1)(2n+1)/6
 Σk³ = (Σk)²
 Σ odd = n²; Σ even = n(n+1)

MENSURATION 2D
 square s: s², 4s
 rectangle: lw, 2(l+w)
 triangle: bh/2
 equilateral: (√3/4)s²
 circle: πr², 2πr
 sector: r²θ/2

HERON: √(s(s−a)(s−b)(s−c))

MENSURATION 3D
 cube: s³, 6s²
 cuboid: lbh, 2(lb+bh+hl)
 cylinder: πr²h, 2πr(r+h)
 cone: πr²h/3, πr(r+l)
 sphere: 4πr³/3, 4πr²
 hemisphere: 2πr³/3, 3πr²

PYTHAGOREAN: 3-4-5, 5-12-13, 8-15-17

COORD GEO
 distance, midpoint, slope, line eq

TRIG (0°, 30°, 45°, 60°, 90°)

LOG
 log(ab) = log a + log b
 log(a^n) = n log a
 base change: log_a b = log_c b / log_c a

EXPONENTS: a^m · a^n = a^(m+n)
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | Quadratic formula + discriminant | ✅✅✅ |
| 2 | Polynomial identities | ✅✅ |
| 3 | AM ≥ GM ≥ HM | ✅✅ |
| 4 | AP/GP n-th term + sum | ✅✅✅ |
| 5 | Σk = n(n+1)/2, Σk², Σk³ | ✅✅ |
| 6 | Mensuration: cube, sphere, cylinder | ✅✅ |
| 7 | Pythagorean triples | ✅ |
| 8 | Heron's formula | ✅ |
| 9 | Distance / slope formulas | ✅ |
| 10 | Trig key values | ✅ |
| 11 | Log identities | ✅ |
| 12 | Vieta's: sum/product roots | ✅✅ |

### Tricks

- **For sum of AP/GP, plug in formula.**
- **For circles in problems:** keep π symbolic until end.
- **For Pythagorean:** check if matches known triple.
- **For trig values:** memorize 0°, 30°, 45°, 60°, 90°.
- **For mensuration of compound figures:** decompose into known shapes.

---

## 5. PYQs (with solutions)

### Q1. (GATE Aptitude 2017)
Sum of first 100 natural numbers:
**Solution.** 100·101/2 = 5050.

### Q2. (GATE Aptitude 2014)
GP: 2, 6, 18, 54. Common ratio?
**Solution.** 3.

### Q3. (GATE Aptitude 2018)
Discriminant of x² − 5x + 6:
**Solution.** 25 − 24 = 1.

### Q4. (GATE Aptitude 2008)
Volume of sphere radius 3:
**Solution.** (4/3)π·27 = 36π.

### Q5. (GATE Aptitude 2010)
AP with first term 5, common diff 3. 10th term:
**Solution.** 5 + 9·3 = 32.

### Q6. (GATE Aptitude 2015)
Heron's: triangle 5, 6, 7:
**Solution.** s = 9; A = √(9·4·3·2) = √216 = 6√6.

### Q7. (GATE Aptitude 2013)
Quadratic roots: sum = 5, product = 6:
**Solution.** Roots 2, 3.

### Q8. (GATE Aptitude 2007)
Surface area of cube side 4:
**Solution.** 6·16 = 96.

### Q9. (GATE Aptitude 2003)
log₂ 32:
**Solution.** 5.

### Q10. (GATE Aptitude 2009)
sin 30° + cos 60°:
**Solution.** 0.5 + 0.5 = 1.

### Q11. (GATE Aptitude 2019)
Σ from 1 to 50 of (2k):
**Solution.** 50·51 = 2550.

### Q12. (GATE Aptitude 2020)
Distance from (0,0) to (3,4):
**Solution.** 5.

### Q13. (GATE Aptitude 2021)
Pythagorean triple 7-24-?:
**Solution.** 25.

### Q14. (GATE Aptitude 2016)
Volume of cone radius 3, height 4:
**Solution.** (1/3)π·9·4 = 12π.

### Q15. (GATE Aptitude 2011)
GP sum to infinity: a=4, r=1/2:
**Solution.** 4/(1−1/2) = 8.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Discriminant of x² + 2x + 1.

**P2.** Sum of AP 1, 4, 7, ..., 100 terms.

**P3.** GP common ratio for 5, 10, 20.

**P4.** Volume of cube side 5.

**P5.** Area of circle radius 7.

**P6.** sin 45°.

**P7.** log_2(64).

**P8.** Sum 1+2+...+50.

**P9.** Pythagorean: 6-8-?

**P10.** Distance (0,0) to (5,12).

### Medium

**P11.** Solve x² − 7x + 12 = 0.

**P12.** Sum of GP 3 + 6 + 12 + ... 8 terms.

**P13.** Heron's: triangle 13, 14, 15.

**P14.** Volume of cylinder radius 5, height 10.

**P15.** Surface area of sphere radius 6.

**P16.** Average of 5 numbers in AP, first 2, last 18.

**P17.** Sum of squares 1² to 20².

**P18.** GP sum infinity 1 + 1/3 + 1/9 + ...

**P19.** Cone slant height for radius 6, height 8.

**P20.** Trig identity sin² + cos².

### Hard

**P21.** Quadratic with sum of roots = 7, product = 10.

**P22.** AP: a₃ = 7, a₇ = 19. Find d.

**P23.** Cone vs cylinder volume comparison (same r, h).

**P24.** Inscribed circle in equilateral triangle.

**P25.** Heron's for triangle 8, 15, 17.

**P26.** Compound figure: rectangle + semicircle.

**P27.** GP series question with negative ratio.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 0 | (x+1)² |
| P2 | 4·100/2·(2+99·3) = 14950 | direct |
| P3 | 2 | direct |
| P4 | 125 | direct |
| P5 | 49π | direct |
| P6 | √2/2 | direct |
| P7 | 6 | 2⁶ |
| P8 | 1275 | 50·51/2 |
| P9 | 10 | 6-8-10 |
| P10 | 13 | √(25+144) |
| P11 | x = 3, 4 | factor |
| P12 | 3·(2⁸−1) = 765 | direct |
| P13 | 84 | s=21; √(21·8·7·6) = 84 |
| P14 | 250π | direct |
| P15 | 144π | direct |
| P16 | (2+18)/2 = 10 | direct |
| P17 | 20·21·41/6 = 2870 | direct |
| P18 | 3/2 | direct |
| P19 | 10 | √(36+64) |
| P20 | 1 | identity |
| P21 | x² − 7x + 10 = 0 | Vieta |
| P22 | a + 2d = 7; a + 6d = 19 ⇒ d=3, a=1 | system |
| P23 | cone = cylinder/3 | direct |
| P24 | r = h/3 = (s/√3)/2 ... use formula | direct |
| P25 | 60 | s=20 |
| P26 | sum areas | direct |
| P27 | sum oscillates | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Quadratic formula sign | ± for both roots. |
| 2 | AP common difference negative | Allowed. |
| 3 | GP r ≠ 0; r = 1 special | Use sum formula for r ≠ 1. |
| 4 | Heron without semi-perimeter | s = (a+b+c)/2. |
| 5 | Sphere area = 2πr² | Wrong (4πr²). |
| 6 | Volume cone = πr²h | Wrong; (1/3) factor. |
| 7 | log without base | Default base 10. |
| 8 | sin 30° = √2/2 | Wrong (1/2). |
| 9 | Pythagorean wrong sides | Hypotenuse longest. |
| 10 | AM = GM only when equal | Equality holds iff a = b. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Sum of first n natural" | n(n+1)/2. |
| "Quadratic discriminant" | b² − 4ac. |
| "AP n-th term" | a + (n−1)d. |
| "GP sum" | a(rⁿ−1)/(r−1). |
| "Heron's" | √(s(s−a)(s−b)(s−c)). |
| "Volume sphere" | (4/3)πr³. |
| "Volume cylinder" | πr²h. |
| "Pythagorean" | Recognize triple. |
| "log identities" | Sum/product/power rules. |
| "Coord distance" | √((Δx)² + (Δy)²). |

---

## 9. Quick Revision

```
QUADRATIC
 x = (−b ± √(b²−4ac))/2a
 sum = −b/a; product = c/a

IDENTITIES
 (a±b)², (a±b)³, a²−b², a³±b³

AM ≥ GM ≥ HM

AP: a_n = a+(n−1)d; S = n/2(a+a_n)
GP: a_n = a r^(n−1); S = a(rⁿ−1)/(r−1)
   S_∞ = a/(1−r), |r|<1
HP: reciprocals AP

SUMS
 Σk = n(n+1)/2
 Σk² = n(n+1)(2n+1)/6
 Σk³ = (Σk)²
 Σ odd = n²; Σ even = n(n+1)

MENSURATION 2D
 square: s², 4s
 rectangle: lw, 2(l+w)
 triangle: bh/2 or Heron's
 equilateral: (√3/4)s²
 circle: πr², 2πr

3D
 cube: s³, 6s²
 cuboid: lbh, 2(lb+bh+hl)
 cylinder: πr²h, 2πr(r+h)
 cone: πr²h/3, πr(r+l)
 sphere: (4/3)πr³, 4πr²

PYTHAGOREAN: 3-4-5, 5-12-13, 8-15-17, 7-24-25

TRIG: 0°, 30°, 45°, 60°, 90°
sin² + cos² = 1

LOG: log(ab), log(a/b), log(a^n)
EXPONENT: a^m·a^n = a^(m+n)

DISTANCE: √((Δx)² + (Δy)²)
SLOPE: Δy/Δx
```
