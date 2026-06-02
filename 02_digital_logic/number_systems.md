# Number Systems & Codes

> Subject: Digital Logic
> GATE weight: **1–2 marks** every year. Conversions, signed representations, IEEE 754, codes — quick scoring topic.

---

## 1. Concept Explanation

### 1.1 Positional Number Systems

A number in **base r** uses digits {0, 1, …, r−1}.

`(dₙ dₙ₋₁ … d₁ d₀ . d₋₁ d₋₂ …)ᵣ = Σ dᵢ · rⁱ`

Common bases:

| Base | Name | Digits |
|---|---|---|
| 2 | Binary | 0, 1 |
| 8 | Octal | 0–7 |
| 10 | Decimal | 0–9 |
| 16 | Hexadecimal | 0–9, A–F |

### 1.2 Conversions

**Decimal → base r:**
- Integer part: divide by r repeatedly, collect remainders bottom-up.
- Fractional part: multiply by r repeatedly, collect integer parts top-down.

**Base r → decimal:** sum dᵢ · rⁱ.

**Binary ↔ Octal:** group binary by 3 (around the point).
**Binary ↔ Hex:** group binary by 4.
**Octal ↔ Hex:** go through binary.

### 1.3 Binary Arithmetic

**Addition rules:**
| 0+0 | 0+1 | 1+0 | 1+1 |
|---|---|---|---|
| 0 | 1 | 1 | 10 |

**Subtraction:** borrow rules — `0−1 = 1, borrow 1`.

**Multiplication:** standard shift-and-add.

**Division:** standard long division.

### 1.4 Signed Representations (n bits)

| Format | Range | +0 / −0 |
|---|---|---|
| **Sign-magnitude** | −(2^(n−1) − 1) to +(2^(n−1) − 1) | both exist |
| **1's complement** | −(2^(n−1) − 1) to +(2^(n−1) − 1) | both exist |
| **2's complement** | −2^(n−1) to +(2^(n−1) − 1) | unique 0 |

**Conversion to 2's complement (negate):**
- Take 1's complement (flip all bits).
- Add 1.
- Or equivalently: from LSB, copy zeros up to the first 1, copy that 1, flip the rest.

**2's complement is the standard** for modern computers — single zero, addition/subtraction symmetric, easy hardware.

### 1.5 Range Comparison (n bits)

| Format | Min | Max | Total values |
|---|---|---|---|
| Unsigned | 0 | 2ⁿ − 1 | 2ⁿ |
| Sign-magnitude | −(2^(n−1) − 1) | +(2^(n−1) − 1) | 2ⁿ − 1 (∵ ±0) |
| 1's complement | −(2^(n−1) − 1) | +(2^(n−1) − 1) | 2ⁿ − 1 |
| 2's complement | −2^(n−1) | +(2^(n−1) − 1) | 2ⁿ |

For n = 8:
- Unsigned: 0 to 255.
- 2's complement: −128 to +127.

### 1.6 Overflow Detection

**Unsigned addition:** overflow iff carry out of MSB.

**Signed (2's complement) addition:** overflow iff signs of operands match but sign of result differs. Equivalent: carry into MSB ≠ carry out of MSB.

**Subtraction:** detect overflow as before, treating subtraction as A + (−B).

### 1.7 IEEE 754 Floating Point

**Single precision (32-bit):** `1 sign | 8 exponent | 23 mantissa`
**Double precision (64-bit):** `1 sign | 11 exponent | 52 mantissa`

**Bias:**
- Single: 127
- Double: 1023

**Stored exponent E_stored = E_actual + bias.**

**Value:** `(−1)^sign · 1.mantissa · 2^(E_stored − bias)` (normalized).

| E_stored | Mantissa | Meaning |
|---|---|---|
| 0 | 0 | ±0 |
| 0 | non-zero | denormalized (subnormal) |
| 255 (single) / 2047 (double) | 0 | ±∞ |
| 255 / 2047 | non-zero | NaN |
| else | any | normalized |

**Range (single):**
- Largest: ≈ 3.4 × 10³⁸
- Smallest normalized: ≈ 1.18 × 10⁻³⁸
- Smallest denormalized: ≈ 1.4 × 10⁻⁴⁵

### 1.8 Fixed-Point vs Floating-Point

- **Fixed-point:** scaled integer; faster but limited range.
- **Floating-point:** scientific notation; wide range, less precision per bit.

### 1.9 Binary-Coded Decimal (BCD)

Each decimal digit encoded with 4 bits (0000–1001). Combinations 1010–1111 are invalid.

- **Storage:** 4 bits per digit (less efficient than binary).
- **Addition:** if intermediate > 9, add 6 (0110) to correct.

### 1.10 Gray Code

Successive numbers differ by exactly **one bit**.

| Decimal | Binary | Gray |
|---|---|---|
| 0 | 000 | 000 |
| 1 | 001 | 001 |
| 2 | 010 | 011 |
| 3 | 011 | 010 |
| 4 | 100 | 110 |
| 5 | 101 | 111 |
| 6 | 110 | 101 |
| 7 | 111 | 100 |

**Conversion (binary → Gray):**
`gᵢ = bᵢ ⊕ bᵢ₊₁` (with b_{n} = 0).

**Conversion (Gray → binary):**
`bᵢ = gᵢ ⊕ gᵢ₊₁ ⊕ … ⊕ gₙ₋₁`.

### 1.11 Excess-3 Code

`Excess-3 = BCD + 3`. Self-complementing — useful for subtraction.

### 1.12 Parity & Hamming Codes

- **Parity bit:** detects single-bit error. Even parity: total # of 1's is even.
- **Hamming code:** detects + corrects single-bit error. (n, k) code.
  - Hamming(7, 4): 4 data + 3 parity bits.
  - **Hamming distance:** # bit positions that differ. Min distance d ⇒ detect d−1 errors, correct ⌊(d−1)/2⌋ errors.

### 1.13 ASCII & Unicode

- **ASCII:** 7-bit (128 chars) / 8-bit extended.
- **Unicode (UTF-8):** variable-length encoding (1–4 bytes).

> **Summary:** Master conversions, 2's complement, IEEE 754, Gray code, parity. These are formula-driven and quick if memorized.

---

## 2. Important Points

- 2's complement: **negate by flipping bits and adding 1**.
- 2's complement range is **asymmetric**: −2^(n−1) to +(2^(n−1) − 1).
- For 2's complement: extending to more bits = **sign-extend** (replicate MSB).
- Overflow in 2's complement: only when both operands have same sign and result has opposite sign.
- IEEE 754 has **biased exponent**, leading 1 implicit (in normalized form).
- IEEE 754 single: bias 127, range ≈ ±3.4×10³⁸.
- BCD wastes bits compared to pure binary (10 codes used out of 16).
- Gray code's **next** code differs by exactly one bit — used in counters to avoid glitches.
- Parity detects but doesn't correct.
- Hamming(7,4) corrects 1-bit errors.
- For n bits: 2^n distinct binary patterns.
- Hex digits A=10, B=11, C=12, D=13, E=14, F=15.
- Octal digit max = 7 (3 bits).
- Hex digit max = F=15 (4 bits).
- Conversion through binary is the fastest path for octal ↔ hex.

---

## 3. Short Notes

```
BASES
 base r, digits 0..r−1
 (d_n…d_0.d_-1…)_r = Σ dᵢ rⁱ

CONVERSIONS
 dec → r: divide-remainder (int), multiply-extract (frac)
 r → dec: sum dᵢ·rⁱ
 bin↔oct: group 3
 bin↔hex: group 4

SIGNED REPS (n bits)
 sign-mag: ±(2^(n−1)−1), ±0
 1's comp: ±(2^(n−1)−1), ±0
 2's comp: −2^(n−1) to +(2^(n−1)−1), unique 0
 negate (2's comp): flip + add 1

OVERFLOW
 unsigned: carry out
 signed: signs of operands same, result different

IEEE 754
 single: 1+8+23, bias 127
 double: 1+11+52, bias 1023
 normalized: (−1)^s · 1.m · 2^(E−bias)
 special:
  E=0,m=0: ±0
  E=0,m≠0: denormal
  E=all1,m=0: ±∞
  E=all1,m≠0: NaN

BCD
 4 bits/digit, 0000–1001 valid
 +6 correction on overflow

GRAY CODE
 successive differ by 1 bit
 g_i = b_i ⊕ b_{i+1}
 b_i = g_i ⊕ g_{i+1} ⊕ … ⊕ g_{n−1}

EXCESS-3 = BCD + 3 (self-complementing)

ERROR CODES
 parity: detect 1-bit error
 Hamming(7,4): correct 1 error
 d_min ⇒ detect d−1, correct ⌊(d−1)/2⌋
```

---

## 4. Formulas / Tricks

| # | Formula / Rule | Memorize Cold? |
|---|---|---|
| 1 | n-bit unsigned: 0 to 2ⁿ−1 | ✅✅ |
| 2 | n-bit 2's comp: −2^(n−1) to +(2^(n−1)−1) | ✅✅ |
| 3 | 2's complement of x = −x = (2ⁿ − x) (mod 2ⁿ) | ✅✅ |
| 4 | Negate via flip + add 1 | ✅✅ |
| 5 | Sign-extend in 2's comp: replicate MSB | ✅ |
| 6 | IEEE 754 single bias = 127, double = 1023 | ✅ |
| 7 | Normalized value: (−1)ˢ · 1.m · 2^(E−bias) | ✅✅ |
| 8 | Gray ↔ Binary conversion formulas | ✅ |
| 9 | BCD overflow correction: +6 | ✅ |
| 10 | Hex: A=10,…,F=15 | ✅✅ |
| 11 | Octal digit ≤ 7 | ✅ |
| 12 | Bin ↔ Oct: 3-bit groups; Bin ↔ Hex: 4-bit groups | ✅✅ |
| 13 | Hamming distance, error correction | ✅ |

### Tricks

- **Negate in 2's comp via subtraction:** `−x = 2ⁿ − x`. Hardware: invert bits + add 1.
- **Sign-extension shortcut:** to extend an 8-bit 2's comp to 16-bit, copy MSB to all extra bits.
- **Quick decimal range check:** for n = 16, 2's comp range is −32768 to 32767.
- **IEEE 754 mental conversion:** sign · 1.m · 2^(stored−127). Skip leading "1." (implicit).
- **Gray code shortcut:** Gᵢ = Bᵢ ⊕ Bᵢ₊₁. Quick to compute by XOR adjacent bits.
- **Octal → Hex via Binary:** convert each octal digit to 3 bits, regroup to 4 bits.
- **For BCD addition correction:** if sum > 9 in any digit, add 6 to that digit.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
The 8-bit 2's complement representation of −12 is:
**Solution.** 12 = 0000 1100. Flip: 1111 0011. Add 1: **1111 0100**.

### Q2. (GATE CSE 2014)
The hexadecimal equivalent of (0010 1101 1011)₂ is:
**Solution.** Group from right by 4: 0010 | 1101 | 1011 = **2DB**.

### Q3. (GATE CSE 2018)
The decimal value of IEEE 754 single-precision 0 10000010 11000000000000000000000:
**Solution.** Sign = 0; Exponent = 130 − 127 = 3; Mantissa = 1.11 = 1.75. Value = 1.75 × 2³ = **14.0**.

### Q4. (GATE CSE 2008)
The largest n-bit 2's complement positive number is:
**Solution.** 2^(n−1) − 1.

### Q5. (GATE CSE 2010)
The number of distinct 8-bit binary numbers is:
**Solution.** 2⁸ = 256.

### Q6. (GATE CSE 2015)
Add the 4-bit 2's complement numbers 0111 + 0011:
**Solution.** 0111 + 0011 = 1010 → MSB = 1 → result is negative in 2's comp = −6. **Overflow** (positive + positive = negative).

### Q7. (GATE CSE 2013)
The Gray code for 12₁₀ is:
**Solution.** 12 = 1100; Gray: g₃ = 1, g₂ = 1⊕1 = 0, g₁ = 1⊕0 = 1, g₀ = 0⊕0 = 0 ⇒ **1010**.

### Q8. (GATE CSE 2016)
Convert (175.25)₁₀ to binary:
**Solution.** 175 = 10101111; 0.25 = 0.01. Result: **10101111.01**.

### Q9. (GATE CSE 2007)
The smallest IEEE 754 single-precision positive normalized number:
**Solution.** Exponent stored = 1; bias 127; value = 1.0 · 2^(−126) ≈ 1.18 × 10⁻³⁸.

### Q10. (GATE CSE 2003)
The 1's complement of (10110100)₂ is:
**Solution.** Flip all bits: **01001011**.

### Q11. (GATE CSE 2009)
Number of bits in n-digit BCD representation of n-digit decimal number:
**Solution.** 4n.

### Q12. (GATE CSE 2019)
Hamming distance between 1011010 and 1110100:
**Solution.** Bit-wise XOR: 0101110. # of 1's = **4**.

### Q13. (GATE CSE 2020)
The 8-bit unsigned binary 11111111 in decimal:
**Solution.** 255.

### Q14. (GATE CSE 2021)
What is (2A)₁₆ in decimal?
**Solution.** 2·16 + 10 = 42.

### Q15. (GATE CSE 2011)
The base of a number system in which (101)ᵣ + (52)ᵣ = (153)ᵣ:
**Solution.** Convert: r² + 0r + 1 + 5r + 2 = r² + 5r + 3. Already balanced ⇒ **any base ≥ 6** is fine. GATE answer: **r = 6**.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Convert (45)₁₀ to binary.

**P2.** Convert (B7)₁₆ to decimal.

**P3.** 1's complement of 10101010.

**P4.** 2's complement of 00110010.

**P5.** Convert (101101)₂ to decimal.

**P6.** Convert (273)₈ to decimal.

**P7.** Range of 5-bit 2's complement.

**P8.** What is (FF)₁₆ in decimal?

**P9.** Convert (10110010)₂ to hexadecimal.

**P10.** Convert (75)₁₀ to BCD.

### Medium

**P11.** Add (1011)₂ + (1110)₂.

**P12.** Multiply (1101)₂ × (101)₂.

**P13.** Convert (170.625)₁₀ to binary.

**P14.** Subtract (0110)₂ − (1010)₂ in 4-bit 2's complement; detect overflow.

**P15.** IEEE 754 single representation of 12.5.

**P16.** Find the Gray code of 5₁₀ (3 bits).

**P17.** Hamming distance between 11010110 and 10011100.

**P18.** Convert (3FA)₁₆ to octal.

**P19.** Add (0110 1001)_BCD + (0011 0101)_BCD.

**P20.** Show (101.11)₂ in decimal.

### Hard

**P21.** Decode IEEE 754 single 1 10000001 01000000000000000000000.

**P22.** Find the smallest positive normalized double-precision value.

**P23.** Show that 2's complement subtraction = addition of 2's complement.

**P24.** Convert (0.7)₁₀ to binary (state if terminating).

**P25.** Hamming(7,4) — encode 1011 with even parity.

**P26.** Gray code → binary: convert (1011)_Gray to binary.

**P27.** Add (15)₁₀ + (10)₁₀ in 5-bit 2's complement; detect overflow.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 101101 | divide by 2 |
| P2 | 183 | 11·16 + 7 |
| P3 | 01010101 | flip |
| P4 | 11001110 | flip + 1 |
| P5 | 45 | 32+8+4+1 |
| P6 | 187 | 2·64 + 7·8 + 3 |
| P7 | −16 to 15 | 2's comp |
| P8 | 255 | 16² − 1 |
| P9 | B2 | groups of 4 |
| P10 | 0111 0101 | per digit |
| P11 | 11001 (5 bits) | direct |
| P12 | 1000001 (65) | shift-add |
| P13 | 10101010.101 | 0.625 = 0.101 |
| P14 | 1100 (= −4 in 2's comp); overflow? both signs known; no overflow | direct |
| P15 | 0 10000010 10010000000000000000000 | 12.5 = 1.5625 × 2³ |
| P16 | 111 | g = b ⊕ shifted |
| P17 | 4 | XOR count |
| P18 | 1772 | 3FA = 1111111010 → 1772 |
| P19 | 1010 0100 (after +6 correction in low digit if needed; here 9+5=14 → 14+6 = 20 i.e. 0010 0000 → carry) — careful BCD step | direct + correction |
| P20 | 5.75 | 4+1+0.5+0.25 |
| P21 | sign 1; E = 129 − 127 = 2; mantissa = 1.01 = 1.25; value = −1.25·4 = −5.0 | IEEE 754 |
| P22 | 1.0 · 2^(−1022) ≈ 2.225 × 10⁻³⁰⁸ | bias 1023 |
| P23 | A − B = A + (−B); −B = 2's comp(B) | identity |
| P24 | 0.10110011… (non-terminating) | repeating |
| P25 | (positions of parity: 1,2,4) compute parities | Hamming encoding |
| P26 | Gray 1011 → b₃=1, b₂=1⊕0=1, b₁=1⊕1⊕1=1, b₀=1⊕0⊕1⊕1=1 ⇒ 1101 | reverse XOR |
| P27 | 15+10=25 > 15 max for 5-bit 2's comp; **overflow** | range check |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting to extend sign in 2's comp | Replicate MSB. |
| 2 | Confusing 1's and 2's complement | 2's = 1's + 1. |
| 3 | Treating positive overflow as negative wraparound | Check signs explicitly. |
| 4 | IEEE 754 forgetting bias | Subtract 127 (single) / 1023 (double). |
| 5 | Forgetting implicit 1 in normalized IEEE 754 | Mantissa = 1.fraction_bits. |
| 6 | Ignoring denormalized numbers | E_stored = 0, m ≠ 0. |
| 7 | BCD without +6 correction | Required when sum > 9. |
| 8 | Gray code: standard binary order | Each step changes 1 bit only. |
| 9 | Hex grouping wrong direction | Group **from right** for integer part. |
| 10 | Sign-magnitude vs 2's comp range confusion | 2's comp asymmetric. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Convert decimal to binary" | Repeated division. |
| "Convert binary to decimal" | Sum of dᵢ · 2ⁱ. |
| "Add/subtract in 2's comp" | Standard, watch for overflow. |
| "Range of n-bit signed" | 2's comp: −2^(n−1) to +(2^(n−1) − 1). |
| "IEEE 754 decode" | Sign, exponent − bias, 1.mantissa, multiply. |
| "Gray code conversion" | XOR adjacent bits. |
| "Hamming distance" | XOR + count 1's. |
| "BCD addition" | Add per digit, +6 if > 9. |
| "Overflow in addition" | Same-sign operands + opposite-sign result. |
| "Find base r given equation" | Convert all digits, solve. |

---

## 9. Quick Revision

```
BASE r: digits 0..r−1; value = Σ dᵢ rⁱ
bin↔oct: 3 bits;  bin↔hex: 4 bits

n-bit unsigned: 0 to 2ⁿ−1
n-bit 2's comp: −2^(n−1) to +(2^(n−1)−1)
NEGATE (2's): flip + add 1
SIGN-EXTEND: replicate MSB

OVERFLOW (signed)
 same signs in, different sign out

IEEE 754
 single: 1+8+23, bias 127
 double: 1+11+52, bias 1023
 (−1)^s · 1.m · 2^(E−bias)
 E=0,m=0: ±0
 E=0,m≠0: denormal
 E=max,m=0: ±∞
 E=max,m≠0: NaN

BCD: 4 bits/digit; +6 if sum > 9
GRAY: g_i = b_i ⊕ b_{i+1}
       b_i = g_i ⊕ g_{i+1} ⊕ … ⊕ g_{n−1}

PARITY: 1-error detect
HAMMING(7,4): 1-error correct
d_min ⇒ detect d−1, correct ⌊(d−1)/2⌋

HEX: A=10, B=11, C=12, D=13, E=14, F=15
```
