# Numerical Computation, Ratios & Percentages

> Subject: General Aptitude — Quantitative
> GATE weight: **2–4 marks** every year. Speed/distance, ratios, percentages, profit/loss, simple/compound interest.

---

## 1. Concept Explanation

### 1.1 Numerical Computation

Quick mental arithmetic, fraction/decimal conversions, BODMAS, divisibility rules.

**BODMAS:** Brackets, Orders (powers/roots), Division, Multiplication, Addition, Subtraction.

### 1.2 Divisibility Rules

| Divisor | Rule |
|---|---|
| 2 | Last digit even |
| 3 | Sum of digits divisible by 3 |
| 4 | Last 2 digits divisible by 4 |
| 5 | Ends in 0 or 5 |
| 6 | Divisible by 2 and 3 |
| 8 | Last 3 digits divisible by 8 |
| 9 | Sum of digits divisible by 9 |
| 10 | Ends in 0 |
| 11 | Alternating sum divisible by 11 |

### 1.3 LCM & GCD (HCF)

- `gcd(a, b) · lcm(a, b) = a · b`.
- LCM by prime factorization: highest power of each prime.
- GCD by Euclidean algorithm: `gcd(a, b) = gcd(b, a mod b)`.

### 1.4 Fractions ↔ Decimals

| Fraction | Decimal |
|---|---|
| 1/2 | 0.5 |
| 1/3 | 0.333… |
| 1/4 | 0.25 |
| 1/5 | 0.2 |
| 1/6 | 0.1666… |
| 1/7 | 0.142857… (repeating) |
| 1/8 | 0.125 |
| 1/9 | 0.111… |
| 1/11 | 0.0909… |

### 1.5 Squares & Cubes (memorize 1–25 squares, 1–10 cubes)

| n | n² | n³ |
|---|---|---|
| 11 | 121 | 1331 |
| 12 | 144 | 1728 |
| 13 | 169 | 2197 |
| 14 | 196 | 2744 |
| 15 | 225 | 3375 |
| 16 | 256 | 4096 |
| 17 | 289 | — |
| 18 | 324 | — |
| 19 | 361 | — |
| 20 | 400 | 8000 |
| 21 | 441 | — |
| 22 | 484 | — |
| 23 | 529 | — |
| 24 | 576 | — |
| 25 | 625 | 15625 |

### 1.6 Ratio & Proportion

**Ratio a:b** = a/b.

**Properties:**
- a:b :: c:d ⇒ ad = bc.
- a:b = ka:kb (multiply both).
- Compounded: a:b and c:d → ac:bd.

**Mean proportional** of a, b: √(ab).

### 1.7 Percentage

`x% = x/100`.

- **A is x% of B:** A = (x/100)·B.
- **% increase:** (new − old)/old × 100.
- **% decrease:** (old − new)/old × 100.

### 1.8 Successive Percentage Change

If a quantity changes by x% then y%:
**Net change** = `x + y + xy/100`.

For decrease, use −y. For two increases:
- 10% then 20% increase: 10 + 20 + 200/100 = 32%.

### 1.9 Profit & Loss

- **CP:** cost price; **SP:** selling price.
- **Profit %** = (SP − CP)/CP × 100.
- **Loss %** = (CP − SP)/CP × 100.
- **SP** = CP × (1 ± p%/100).
- **Discount %** = (MP − SP)/MP × 100.

### 1.10 Simple Interest (SI)

`SI = P × R × T / 100`

| P | Principal |
|---|---|
| R | Rate per annum |
| T | Time (years) |

Total = P + SI.

### 1.11 Compound Interest (CI)

`A = P · (1 + R/100)^T`

`CI = A − P`.

For half-yearly: rate/2, time × 2. For quarterly: rate/4, time × 4.

**Difference (CI − SI):**
- 2 years: P·(R/100)².
- 3 years: P·(R/100)²·(3 + R/100).

### 1.12 Speed, Time, Distance

`Distance = Speed × Time`.

**Conversions:**
- 1 km/h = 5/18 m/s.
- 1 m/s = 18/5 km/h.

**Average speed for two segments:**
- Same distance, speeds s₁, s₂: `2s₁s₂/(s₁+s₂)` (harmonic mean).
- Different distances: total distance / total time.

### 1.13 Trains

- **Length L1, L2; speeds in same direction:** time to overtake = (L1+L2)/(s1−s2).
- **Opposite direction:** time = (L1+L2)/(s1+s2).
- **Train passing pole:** time = L/s.
- **Train passing platform of length P:** time = (L+P)/s.

### 1.14 Boats / Streams

- Downstream speed = boat + stream.
- Upstream speed = boat − stream.
- Average for round trip = 2·D·U/(D+U).

### 1.15 Time and Work

- If A does work in n days, A's rate = 1/n per day.
- Combined: rates add.
- A and B: 1/n_A + 1/n_B = combined rate.

**Pipes & Cisterns:** filling pipes are positive rates, draining negative.

### 1.16 Mixtures & Alligation

**Alligation rule** for two ingredients with concentrations c₁, c₂ to make mean c_m:
`(c₁ − c_m) : (c_m − c₂)` = ratio of c₂ : c₁ amounts.

### 1.17 Ratio Problems Quick Tricks

- **Increase ratio** a:b by x: (a+x):(b+x); always check if it produces target ratio.
- **Combined ratio** when comparing 3 quantities: convert pairs to common middle.

### 1.18 Percentage to Fraction Quick Memory

| % | Fraction |
|---|---|
| 12.5% | 1/8 |
| 25% | 1/4 |
| 33.33% | 1/3 |
| 50% | 1/2 |
| 66.66% | 2/3 |
| 75% | 3/4 |
| 87.5% | 7/8 |

### 1.19 Approximation Tips

For percentages: 10% = move decimal one place; 5% = half of 10%.
- 17% of 250 = 25 + 12.5 = 37.5 + ... ≈ 42.5.

### 1.20 Common GATE Problem Types

- Speed conversions.
- Train problems (overtake, passing).
- Boats and streams.
- Profit and loss with multiple stages.
- Compound interest.
- Mixtures (alligation).
- Ratio combinations.

> **Summary:** Master arithmetic shortcuts, percentage tricks, ratio manipulation, profit/loss formulas, SI/CI, and STD problems. Aptitude rewards speed; memorize the formulas.

---

## 2. Important Points

- **gcd × lcm = product** of two numbers.
- **% increase ≠ % decrease** in general (different bases).
- **Successive percentage** uses `x + y + xy/100` formula.
- **Average speed (same distance, two speeds):** harmonic mean.
- **Train overtake time:** sum of lengths over relative speed.
- **CI grows faster than SI** for same P, R, T.
- **CI − SI for 2 years** = P·(R/100)².
- **Profit% on CP**, not SP.
- **Discount % on MP**, not SP.
- **Alligation:** 2 components, find mean concentration.

---

## 3. Short Notes

```
BODMAS

DIVISIBILITY: 2 (last digit), 3 (sum), 4 (last 2), 5 (ends 0/5),
              8 (last 3), 9 (sum), 11 (alt sum)

LCM·GCD = a·b

PERCENTAGE
 x% = x/100
 % increase: (new−old)/old × 100
 successive: x + y + xy/100

PROFIT/LOSS
 SP = CP·(1 ± p%/100)
 profit% = (SP−CP)/CP × 100
 discount% = (MP−SP)/MP × 100

SI = P·R·T/100
CI: A = P·(1+R/100)^T; CI = A − P
CI − SI (2 yr) = P(R/100)²

SPEED/DISTANCE/TIME
 D = S × T
 km/h ↔ m/s: × 5/18 / × 18/5

TRAINS
 same direction overtake: (L₁+L₂)/(s₁−s₂)
 opposite: (L₁+L₂)/(s₁+s₂)
 pole: L/s
 platform: (L+P)/s

BOATS/STREAMS
 downstream = boat + stream
 upstream = boat − stream

WORK
 rate = 1/days; combine rates

MIXTURES/ALLIGATION
 (c₁−cₘ) : (cₘ−c₂) = c₂ : c₁ amount

% TO FRACTION
 12.5%=1/8, 25%=1/4, 33.3%=1/3, 50%=1/2, 75%=3/4

SQUARES 11–25 / CUBES 1–10
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | gcd × lcm = a·b | ✅✅ |
| 2 | Successive %: x + y + xy/100 | ✅✅✅ |
| 3 | km/h ↔ m/s: × 5/18 / × 18/5 | ✅✅✅ |
| 4 | Average speed (same distance): 2s₁s₂/(s₁+s₂) | ✅✅ |
| 5 | SI = PRT/100 | ✅✅ |
| 6 | CI = P(1+R/100)^T − P | ✅✅ |
| 7 | CI − SI (2 yr) = P(R/100)² | ✅ |
| 8 | Profit% = (SP−CP)/CP × 100 | ✅✅ |
| 9 | Discount% on MP | ✅ |
| 10 | Train overtake (same dir): (L₁+L₂)/(s₁−s₂) | ✅✅ |
| 11 | Boats: down/up = boat ± stream | ✅ |
| 12 | Alligation: (c₁−cₘ)/(cₘ−c₂) | ✅ |
| 13 | Mean proportional = √(ab) | ✅ |

### Tricks

- **% increase + decrease in alternation:** never returns to original; net = −(x²/100) for same x.
- **For successive % of same x twice:** multiplier = (1 + x/100)².
- **For boats finding stream speed:** stream = (D − U)/2; boat = (D + U)/2.
- **For mixtures ratio change:** alligation table.
- **For speed conversion:** memorize key speeds (60 km/h = 16.67 m/s).

---

## 5. PYQs (with solutions)

### Q1. (GATE Aptitude 2017)
A's speed is 30 km/h, B's speed is 40 km/h. They travel from same point opposite directions for 3 hours. Distance apart?
**Solution.** Combined speed = 70 km/h × 3 = 210 km.

### Q2. (GATE Aptitude 2014)
Net change after 20% increase then 10% decrease:
**Solution.** 20 + (−10) + 20·(−10)/100 = 8%.

### Q3. (GATE Aptitude 2018)
SI on Rs 5000 at 8% for 2 years:
**Solution.** 5000·8·2/100 = 800.

### Q4. (GATE Aptitude 2008)
CI on Rs 1000 at 10% for 2 years:
**Solution.** 1000·(1.1)² − 1000 = 1210 − 1000 = 210.

### Q5. (GATE Aptitude 2010)
Trains 100 m and 150 m, speeds 50 km/h and 30 km/h opposite. Time to cross:
**Solution.** Rel speed = 80 km/h = 200/9 m/s. Time = 250 / (200/9) = 11.25 s.

### Q6. (GATE Aptitude 2015)
Boat speed in still water 10 km/h, stream 2 km/h. Time to go 24 km downstream + return:
**Solution.** D = 12, U = 8. 24/12 + 24/8 = 2 + 3 = 5 hrs.

### Q7. (GATE Aptitude 2013)
A : B = 3:5; B : C = 4:7. A : B : C?
**Solution.** Match B: 3·4 : 5·4 = 12:20; B:C = 4·5:7·5 = 20:35. So A:B:C = 12:20:35.

### Q8. (GATE Aptitude 2007)
A = 25% of B. C = 50% of A. B in terms of C?
**Solution.** A = 0.25B; C = 0.5A = 0.125B; B = 8C.

### Q9. (GATE Aptitude 2003)
Alligation: 30% milk + 70% milk to make 50% mix. Ratio?
**Solution.** (50−30):(70−50) = 20:20 = 1:1.

### Q10. (GATE Aptitude 2009)
Profit 20% on CP. CP = 100. SP?
**Solution.** SP = 120.

### Q11. (GATE Aptitude 2019)
A does work in 10 days; B in 15. Together?
**Solution.** Rate = 1/10 + 1/15 = 5/30 = 1/6. **6 days.**

### Q12. (GATE Aptitude 2020)
Mean proportional of 4 and 9:
**Solution.** √(4·9) = 6.

### Q13. (GATE Aptitude 2021)
Average speed for 60 km at 30 km/h and 60 km at 60 km/h:
**Solution.** 2·30·60/(30+60) = 3600/90 = 40 km/h.

### Q14. (GATE Aptitude 2016)
% to fraction: 37.5%:
**Solution.** 3/8.

### Q15. (GATE Aptitude 2011)
Discount of 25% on Rs 800 marked. SP?
**Solution.** 800·0.75 = 600.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Convert 72 km/h to m/s.

**P2.** 30% of 250.

**P3.** Successive 10% then 20% increase.

**P4.** SI Rs 1000, 5%, 4 yrs.

**P5.** CI Rs 2000, 10%, 2 yrs.

**P6.** Profit% if CP=80, SP=100.

**P7.** Discount% if MP=200, SP=160.

**P8.** A's speed 60 km/h. Distance in 3 hrs.

**P9.** Two trains opposite, speeds 40 and 50 km/h, 100m+200m. Time to cross.

**P10.** A:B = 2:3. If A=10, B=?

### Medium

**P11.** Average speed of 100 km at 50 and 100 km at 100 km/h.

**P12.** Alligation: 20% and 50% to make 35%.

**P13.** Mean proportional of 5 and 20.

**P14.** A:B:C = 2:3:4. A+B+C = 27. Find A.

**P15.** CI − SI for Rs 5000, 10%, 2 yrs.

**P16.** Boat speed in still water? Down 18, up 12.

**P17.** A = 1/3 of B. C = 1/2 of A. C in terms of B.

**P18.** Time to cover 90 km at 60 km/h.

**P19.** Discount calculation: List 1000, 20% then 10%.

**P20.** Pipe A fills tank in 4 hrs, B in 6 hrs. Together?

### Hard

**P21.** A invests Rs 5000 at SI 6% for 5 years. CI for same → diff.

**P22.** Mixture: 5L milk-water with 80% milk. How much water to add for 50%?

**P23.** Train 200m crosses platform 400m in 30s. Speed?

**P24.** Profit-loss chain: A → B with 20% profit; B → C with 10% loss. Net?

**P25.** Boats: speed in still 8, against current half of with. Find current.

**P26.** Three pipes A, B, C: A fills 1/3, B fills 1/4, C drains 1/6 per hr. Together?

**P27.** Two cars meet at midpoint. Speeds 40 and 60. Total distance 100. When meet?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 20 m/s | × 5/18 |
| P2 | 75 | direct |
| P3 | 32% | x+y+xy/100 |
| P4 | 200 | direct |
| P5 | 420 | 2000·1.21−2000 |
| P6 | 25% | 20/80 |
| P7 | 20% | 40/200 |
| P8 | 180 km | direct |
| P9 | 12 s | rel 90·5/18 = 25 m/s; 300/25 |
| P10 | 15 | direct |
| P11 | 200/3 ≈ 66.67 km/h | total dist / total time |
| P12 | (35−20):(50−35) = 1:1 | direct |
| P13 | 10 | √100 |
| P14 | 6 | 2·27/9 |
| P15 | 50 | 5000·(0.1)² |
| P16 | 15 | (D+U)/2 |
| P17 | C = B/6 | direct |
| P18 | 1.5 hr | direct |
| P19 | (1000·0.8·0.9) = 720 | successive |
| P20 | 12/5 = 2.4 hrs | combined rate |
| P21 | SI = 1500; CI = 5000(1.06⁵ − 1) ≈ 1691; diff ≈ 191 | direct |
| P22 | 3L water (5L mix has 4L milk; need 50% → 8L total ⇒ 3L water) | direct |
| P23 | 600/30 = 20 m/s = 72 km/h | direct |
| P24 | A→B at 1.2x; B→C at 0.9·1.2x = 1.08x; net 8% profit | direct |
| P25 | Down speed = 8 + c; up = 8 − c; ratio 2:1 ⇒ c = 8/3 | direct |
| P26 | 1/3 + 1/4 − 1/6 = (4+3−2)/12 = 5/12 ⇒ 12/5 hrs | direct |
| P27 | meet when sum of distances = 100; time = 100/100 = 1 hr | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forget % is on CP not SP | Profit% always on CP. |
| 2 | Successive % wrongly added | Use x+y+xy/100. |
| 3 | Average speed = arithmetic mean | Use harmonic mean for same distance. |
| 4 | km/h to m/s without conversion | × 5/18. |
| 5 | Train passing pole as platform | Pole has 0 length. |
| 6 | Stream = boat speed | Different concepts. |
| 7 | Discount on SP | Discount on MP. |
| 8 | CI = SI for 1 year | Equal in first year only. |
| 9 | Profit when SP > CP only | Yes. |
| 10 | Mixture ratio reversed | Alligation order matters. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Successive % change" | x + y + xy/100. |
| "Average speed same distance" | Harmonic mean. |
| "Trains crossing" | Sum of lengths / relative speed. |
| "Stream / current" | down/up = boat ± stream. |
| "Profit/Loss" | % on CP. |
| "Mixture concentration" | Alligation. |
| "Compound interest" | A = P(1+R/100)^T. |
| "CI − SI 2 years" | P(R/100)². |
| "Work problems" | Add rates. |
| "Mean proportional" | √(ab). |

---

## 9. Quick Revision

```
DIVISIBILITY: 2/3/4/5/6/8/9/10/11

gcd · lcm = a · b

PERCENTAGE
 x% = x/100
 successive: x + y + xy/100

km/h ↔ m/s: × 5/18 / × 18/5

PROFIT/LOSS
 SP = CP(1 ± p%/100)
 % on CP

SI = PRT/100
CI = P(1+R/100)^T − P
CI − SI (2 yr) = P(R/100)²

SPEED
 D = S·T
 avg same dist: 2s₁s₂/(s₁+s₂)

TRAINS
 same dir: (L₁+L₂)/(s₁−s₂)
 opp: (L₁+L₂)/(s₁+s₂)

BOATS
 down = boat + stream
 up = boat − stream

WORK: rates add

MIXTURES alligation: (c₁−cₘ):(cₘ−c₂)

% FRAC
 12.5=1/8, 25=1/4, 33.3=1/3, 50=1/2, 75=3/4

SQUARES 11-25 cold
```
