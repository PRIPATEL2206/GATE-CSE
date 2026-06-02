# Combinational Circuits (Mux, Decoder, Adders)

> Subject: Digital Logic
> GATE weight: **2–4 marks** every year. Mux/decoder implementations, adders, comparators, encoders.

---

## 1. Concept Explanation

### 1.1 Combinational vs Sequential

- **Combinational:** output depends **only** on current inputs. No memory.
- **Sequential:** output depends on inputs **and** internal state (memory).

### 1.2 Half Adder

Adds two 1-bit inputs A, B; produces Sum (S) and Carry (C).

| A | B | S | C |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

`S = A ⊕ B`
`C = AB`

### 1.3 Full Adder

Adds A, B, and carry-in Cᵢₙ; produces Sum and Cₒᵤₜ.

| A | B | Cin | S | Cout |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

`S = A ⊕ B ⊕ Cin`
`Cout = AB + (A ⊕ B)Cin = AB + ACin + BCin`

A Full Adder = 2 Half Adders + OR gate.

### 1.4 Ripple-Carry Adder (n-bit)

Cascade n full adders; each carry feeds the next.
- Delay: O(n) — slow for large n.
- Gates: 5n approx (2 XOR + 2 AND + 1 OR per FA).

### 1.5 Carry Look-ahead Adder (CLA)

Compute carries in parallel.
- **Generate** Gᵢ = AᵢBᵢ.
- **Propagate** Pᵢ = Aᵢ ⊕ Bᵢ.
- Cᵢ₊₁ = Gᵢ + Pᵢ Cᵢ.
- Expand: C₁ = G₀ + P₀C₀; C₂ = G₁ + P₁G₀ + P₁P₀C₀; …
- **Delay:** O(log n) using tree of carries.
- More gates but faster.

### 1.6 Subtractor

A − B = A + (2's complement of B) = A + B' + 1.
Use FA with B inverted and Cin = 1.

**Half subtractor:** D = A ⊕ B; Borrow = A'B.
**Full subtractor:** D = A ⊕ B ⊕ Bin; Bout = A'B + (A ⊕ B)'Bin.

### 1.7 Multiplexer (MUX)

Selects 1 of 2ⁿ inputs based on n select lines.

**2:1 MUX:** `Y = S'·I₀ + S·I₁`.

**4:1 MUX:**
```
Y = S₁'S₀'·I₀ + S₁'S₀·I₁ + S₁S₀'·I₂ + S₁S₀·I₃
```

**Cascading:** 2:1 MUXes can build 4:1 (3 of them), 8:1 (7), …; 2ⁿ:1 needs 2ⁿ−1 of 2:1 MUXes.

**Function realization:** any n-variable Boolean function can be implemented using:
- 2ⁿ:1 MUX (each input is 0 or 1 — a minterm).
- 2^(n−1):1 MUX with n−1 select lines, n-th variable feeds inputs as constants/literals.

### 1.8 Demultiplexer (DEMUX)

Routes 1 input to 1 of 2ⁿ outputs based on n select lines.
Inverse of MUX. Often used as a decoder when input is held at 1.

### 1.9 Decoder

n-to-2ⁿ decoder: n inputs, 2ⁿ outputs. Exactly one output is high.

| Inputs | Output enabled |
|---|---|
| 00 | Y₀ |
| 01 | Y₁ |
| 10 | Y₂ |
| 11 | Y₃ |

Each output = a minterm.

**Function realization:** an n-to-2ⁿ decoder followed by an OR gate of selected minterms implements any function.

### 1.10 Encoder

Inverse of decoder. 2ⁿ-to-n: only one input is high; output = its index.

**Priority encoder:** if multiple inputs are high, output = index of highest priority (typically highest-numbered).

### 1.11 Comparator (Magnitude)

For 1-bit: A > B = AB'; A = B = A'B' + AB; A < B = A'B.

For multi-bit: compare from MSB downward; first different bit decides.

### 1.12 Code Converters

Common converters:
- BCD → 7-segment.
- Binary → Gray.
- Gray → Binary.

### 1.13 Tri-state Buffer

Output = input when enable = 1; high impedance (Z) when enable = 0. Used for **bus** sharing.

### 1.14 PLD (Programmable Logic Devices)

| Type | AND array | OR array |
|---|---|---|
| ROM | fixed (decoder) | programmable |
| PAL | programmable | fixed |
| PLA | programmable | programmable |

### 1.15 Hazards (preview — full file: minimization_hazards)

- **Static-1 hazard:** output briefly drops to 0 even though it should stay 1.
- **Static-0 hazard:** opposite.
- **Dynamic hazard:** multiple transitions where one was expected.
- Caused by unequal gate delays. Eliminated by **redundant prime implicants**.

### 1.16 Common Implementations Summary

| Component | # Inputs | Function |
|---|---|---|
| Half Adder | 2 | S, C |
| Full Adder | 3 | S, Cout |
| 4-bit Adder | 8 (4+4) | 4 sum bits + Cout |
| 2:1 MUX | 3 (2 data + 1 sel) | Y |
| 4:1 MUX | 6 (4 data + 2 sel) | Y |
| 8:1 MUX | 11 (8 data + 3 sel) | Y |
| 2-to-4 Decoder | 2 (+1 enable) | 4 outputs |
| 3-to-8 Decoder | 3 (+1 enable) | 8 outputs |
| 4-bit Comparator | 8 | A>B, A=B, A<B |

> **Summary:** Full adder is the building block. MUX/Decoder/Encoder are standard. Master function realization using MUX (especially 2^(n−1):1) and via decoder + OR. CLA gives O(log n) addition.

---

## 2. Important Points

- A **2ⁿ:1 MUX** can realize any n-input Boolean function with truth-table values fed to data inputs.
- A **2^(n−1):1 MUX** can realize any n-input Boolean function: pair rows by the n-th variable; feed `0`, `1`, `Xₙ`, or `Xₙ'` to each MUX input.
- An **n-to-2ⁿ decoder + OR gate** realizes any function (one minterm per output line).
- **Full adder using 2 XORs + 2 ANDs + 1 OR**, OR using 2 half adders + OR.
- **Subtraction** = addition with 2's complement of subtrahend.
- **Ripple-carry delay = O(n)**; CLA delay = O(log n).
- Half adder produces no Cin handling — must use FA for chained addition.
- **In a 2:1 MUX:** select line picks between two data lines.
- **Demux** with n select bits has 2ⁿ outputs.
- A decoder enabled with input fixed at 1 acts as a demux.
- A **priority encoder** resolves ambiguity when multiple inputs are 1.
- Tri-state buffers allow multiple devices to share a bus (only one drives at a time).
- ROM with k address bits can realize any k-input function (table lookup).
- For PLA, count gates carefully — programmable on both AND and OR arrays.

---

## 3. Short Notes

```
HALF ADDER
 S = A ⊕ B
 C = AB

FULL ADDER
 S = A ⊕ B ⊕ Cin
 Cout = AB + (A⊕B)·Cin
      = AB + ACin + BCin
 = 2 HA + 1 OR

n-bit RIPPLE: O(n) delay
CLA
 G_i = A_iB_i (generate)
 P_i = A_i ⊕ B_i (propagate)
 C_{i+1} = G_i + P_iC_i
 delay O(log n)

SUBTRACTOR
 A − B = A + B' + 1

MUX
 2ⁿ:1 selects from 2ⁿ
 select lines = n
 Y = Σ S' decoded · I

 2^(n−1):1 realizes n-var fn:
   pair rows by last var; feed {0, 1, X, X'}

DEMUX = inverse MUX

DECODER
 n-to-2ⁿ; each output = minterm
 + OR gate ⇒ any fn

ENCODER
 2ⁿ-to-n
 priority: resolves ties

COMPARATOR
 A>B, A=B, A<B (MSB to LSB)

PLD
 ROM: AND fixed, OR prog
 PAL: AND prog, OR fixed
 PLA: both prog

TRI-STATE: 0/1/Z
 used for bus sharing

HAZARDS (preview)
 fixed by redundant PIs
```

---

## 4. Formulas / Tricks

| # | Fact | Memorize Cold? |
|---|---|---|
| 1 | HA: S = A⊕B, C = AB | ✅✅ |
| 2 | FA: S = A⊕B⊕Cin, Cout = AB + (A⊕B)Cin | ✅✅ |
| 3 | n-bit ripple delay = O(n) | ✅ |
| 4 | CLA delay = O(log n) | ✅ |
| 5 | Subtraction via 2's complement | ✅✅ |
| 6 | 2ⁿ:1 MUX = any n-var function | ✅✅ |
| 7 | 2^(n−1):1 MUX = any n-var function (with one var as data) | ✅✅ |
| 8 | n-to-2ⁿ decoder + OR = any n-var function | ✅ |
| 9 | # 2:1 MUXes for 2ⁿ:1 = 2ⁿ − 1 | ✅ |
| 10 | Encoder produces output = index of high input | ✅ |
| 11 | Priority encoder breaks ties | ✅ |
| 12 | ROM/PAL/PLA AND-OR programmability table | ✅ |
| 13 | Carry-out of FA: AB + ACin + BCin (majority function) | ✅ |

### Tricks

- **MUX function realization:** for n inputs, use n−1 select lines. The remaining variable feeds data inputs as one of `{0, 1, X, X'}` based on truth-table grouping.
- **For ripple-carry adder, worst-case delay** = (n−1) FA delays + final FA delay.
- **Decoder for memory addressing:** n bits address 2ⁿ memory locations.
- **Two adders for both adder and subtractor:** XOR each B-bit with mode bit M (M=0 add, M=1 subtract).
- **Comparator MSB-first:** earliest difference decides (equal-bits pass through).
- **Tri-state with active-low enable:** common in bus implementation.
- For function realization with MUX, **pair groups of 2** in K-map; each pair gives one MUX data input.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A 4-bit ripple-carry adder uses 4 full adders. Each FA has propagation delay 1 ns. Total worst-case delay?
**Solution.** 4·1 = 4 ns.

### Q2. (GATE CSE 2014)
Number of select lines for an 8:1 MUX is:
**Solution.** log₂8 = 3.

### Q3. (GATE CSE 2018)
A function F(A, B, C) = Σm(0, 2, 5, 6) is realized using a 4:1 MUX with A, B as select. What's I₀, I₁, I₂, I₃?
**Solution.**
- AB=00 (rows 0,1): F=1,0 ⇒ depends on C; row 0 is m0=1, row 1 is m1=0 → I₀ = C'
- AB=01 (rows 2,3): F=1,0 → I₁ = C'
- AB=10 (rows 4,5): F=0,1 → I₂ = C
- AB=11 (rows 6,7): F=1,0 → I₃ = C'

### Q4. (GATE CSE 2008)
Implement F(A,B,C) = AB + AC using 2:1 MUXes:
**Solution.** F = A(B + C); use one 2:1 MUX with A as select: I₀=0, I₁=B+C; or other arrangement.

### Q5. (GATE CSE 2015)
Number of NAND gates required to implement a Full Adder:
**Solution.** 9 NAND gates.

### Q6. (GATE CSE 2010)
A 32-bit ripple-carry adder takes 32 ns when each FA has 1 ns delay. A CLA implementation reduces this to:
**Solution.** O(log 32) = 5 ns approximately.

### Q7. (GATE CSE 2013)
A 2-to-4 decoder is used to implement F(A,B) = Σm(0, 2). Outputs Y₀=A'B', Y₂=AB'. F = Y₀ + Y₂.

### Q8. (GATE CSE 2007)
A 4:1 MUX has inputs `I₀=1, I₁=0, I₂=A, I₃=A'`, select lines `S₁S₀ = BC`. Output?
**Solution.**
- BC=00: output = 1
- BC=01: output = 0
- BC=10: output = A
- BC=11: output = A'

This is `B'C' + BC'·A + BC·A' = ...` — simplify: output = `B'C' + B·(C XOR A)`. Verify via truth table.

### Q9. (GATE CSE 2003)
The number of 2:1 MUXes required to realize an 8:1 MUX:
**Solution.** 2ⁿ − 1 = 7.

### Q10. (GATE CSE 2009)
A Boolean function F(W, X, Y, Z) is realized using a 4:1 MUX with W, X as select. Determine inputs.
*(Pattern: for each WX pair, find dependence on Y, Z.)*

### Q11. (GATE CSE 2016)
Carry generation: G_i = A_i AND B_i. Propagation: P_i = A_i XOR B_i. C_2 in CLA?
**Solution.** C₂ = G₁ + P₁G₀ + P₁P₀C₀.

### Q12. (GATE CSE 2019)
A 4-bit comparator outputs A=B when:
**Solution.** All bits match: ∏(Aᵢ ⊙ Bᵢ).

### Q13. (GATE CSE 2020)
A 4-bit binary number is converted to gray code. Number of XOR gates required?
**Solution.** 3 (one for each adjacent pair: g₀=b₀⊕b₁, g₁=b₁⊕b₂, g₂=b₂⊕b₃, g₃=b₃).

### Q14. (GATE CSE 2021)
A 1-bit full adder has Cout = AB + ACin + BCin. This is also known as the:
**Solution.** Majority function (3 inputs).

### Q15. (GATE CSE 2011)
Implement F(A,B,C,D) using only one 8:1 MUX. Is it possible?
**Solution.** Yes — use A, B, C as select; for each of 8 select combinations, feed data input as `0`, `1`, `D`, or `D'` based on truth table rows.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Truth table of a half adder.

**P2.** Number of select lines in 16:1 MUX.

**P3.** Number of outputs in a 3-to-8 decoder.

**P4.** Sum equation for full adder.

**P5.** Cout equation for full adder.

**P6.** Cardinality of 2:1 MUX inputs (data + select).

**P7.** Number of 2:1 MUXes to make 4:1 MUX.

**P8.** Implement OR using 2:1 MUX.

**P9.** Realize 4:1 MUX using 2-to-4 decoder.

**P10.** Implement subtraction using addition.

### Medium

**P11.** Implement F = A ⊕ B ⊕ C using 4:1 MUX with A, B as select.

**P12.** Implement F(A,B,C) = AB + BC + CA using 2-to-4 decoder + OR.

**P13.** A 4-bit ripple-carry adder + 4-bit subtractor combined: design.

**P14.** Compute carry C₃ in CLA for 4-bit adder.

**P15.** Implement 4:1 MUX from two 2:1 MUXes; verify.

**P16.** Implement 2-to-4 decoder using 1-to-2 demuxes (and vice versa).

**P17.** A priority encoder has inputs I₃ I₂ I₁ I₀ = 0011. Output?

**P18.** Implement a 4-bit comparator (>, =, <).

**P19.** A 2:1 MUX has S=1, I₀=1, I₁=0. Output?

**P20.** A 4:1 MUX with I₀=A, I₁=A', I₂=0, I₃=1, select BC. Output for B=1, C=0, A=1?

### Hard

**P21.** Implement F(A,B,C,D) = Σm(0,2,5,7,8,10,13,15) using 8:1 MUX.

**P22.** A binary multiplier 4×4: design using AND gates and adders.

**P23.** Compare ripple-carry vs CLA delay for 16-bit adder (gate delay = 1 ns).

**P24.** Implement F = (A ⊕ B) · (C + D') using NAND gates only.

**P25.** Implement F(A,B,C,D) = Σm(0,1,3,5,7,9,11,15) using a 4-to-16 decoder + OR.

**P26.** Show how to use a 3-to-8 decoder + OR gates to implement a full adder (S, Cout).

**P27.** A 32K × 8 ROM is used. How many address lines and data lines?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | as in 1.2 | direct |
| P2 | 4 | log₂16 |
| P3 | 8 | 2³ |
| P4 | A ⊕ B ⊕ Cin | direct |
| P5 | AB + (A⊕B)Cin | direct |
| P6 | 3 (2 data + 1 select) | direct |
| P7 | 3 | tree |
| P8 | I₀=B, I₁=1; select=A | OR identity |
| P9 | enable each output line; OR all | direct |
| P10 | 2's comp + add | identity |
| P11 | for AB=00,01,10,11: F = C, C', C', C respectively | via XOR table |
| P12 | majority via decoder; output = m3+m5+m6+m7 | OR |
| P13 | XOR each B-bit with mode bit M; Cin = M | adder/subtractor |
| P14 | C₃ = G₂+P₂G₁+P₂P₁G₀+P₂P₁P₀C₀ | CLA |
| P15 | tree of two 2:1 MUXes | direct |
| P16 | similar mapping | direct |
| P17 | output = 1 (binary 01) | priority |
| P18 | use XNOR for equality + chain inequality | direct |
| P19 | I₁ = 0 | direct |
| P20 | BC=10, output = I₂ = 0 | direct |
| P21 | use 3 var as select; data = 0 or 1 or D or D' | implement F |
| P22 | partial products + adders | direct |
| P23 | ripple = 16 ns; CLA = ~5 ns | log delay |
| P24 | apply DM and convert | NAND-only |
| P25 | OR of selected outputs | decoder |
| P26 | S = m1+m2+m4+m7; Cout = m3+m5+m6+m7 | direct |
| P27 | 15 address (32K = 2¹⁵), 8 data | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Using HA for chained addition | HA has no Cin handling — use FA. |
| 2 | Forgetting Cin in subtraction | Subtraction needs Cin = 1. |
| 3 | Wrong # select lines for MUX | n select lines for 2ⁿ:1 MUX. |
| 4 | Wrong # data inputs | 2ⁿ for 2ⁿ:1. |
| 5 | Confusing decoder and demux | They're functionally equivalent (decoder = demux with constant input). |
| 6 | Mixing up encoder priority | Default: highest index wins. |
| 7 | Forgetting CLA reduces to log delay only at gate level | Practical CLA may use grouping. |
| 8 | PLA vs PAL ROMs confusion | ROM = decoder + OR; PAL = prog AND fixed OR; PLA = both prog. |
| 9 | Implementing function with MUX without checking truth table groupings | List minterms, group by select bits. |
| 10 | Forgetting A=B comparator chain | Comparator must check all bits. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Implement n-input function with MUX" | 2^(n−1):1 MUX with one var as data. |
| "Implement using decoder + OR" | n-to-2ⁿ decoder; OR selected minterms. |
| "Number of FAs for n-bit adder" | n. |
| "n-bit subtraction via adder" | XOR gates + Cin trick. |
| "Carry-look-ahead delay" | O(log n) gate delays. |
| "MUX cascading" | 2ⁿ − 1 of (2:1) for 2ⁿ:1. |
| "Priority encoder output" | Highest-index 1-input. |
| "Comparator equality" | Bitwise XNOR + AND. |
| "ROM/PAL/PLA differences" | Programmability table. |
| "Implementing XOR with NAND" | Bubble-pushing / 4-NAND XOR. |

---

## 9. Quick Revision

```
HA: S = A⊕B, C = AB
FA: S = A⊕B⊕Cin, Cout = AB + (A⊕B)Cin
n-bit ripple: O(n)
CLA: O(log n)
sub: A + B' + 1

MUX
 2ⁿ:1 needs n select lines
 2^(n−1):1 + var-as-data ⇒ n-input fn
 # 2:1 MUXes for 2ⁿ:1 = 2ⁿ − 1

DECODER
 n-to-2ⁿ; outputs = minterms
 + OR ⇒ any fn

ENCODER
 2ⁿ-to-n; priority resolves ties

COMPARATOR
 MSB first; equality via XNOR chain

PLD
 ROM: AND fixed, OR prog
 PAL: AND prog, OR fixed
 PLA: both prog

TRI-STATE: 0, 1, Z

HAZARDS — fix with redundant PIs
```
