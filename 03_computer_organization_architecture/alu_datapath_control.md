# ALU, Datapath & Control Unit

> Subject: Computer Organization & Architecture (COA)
> GATE weight: **2–4 marks** every year. Datapath cycle counting, control signals, hardwired vs microprogrammed, integer/float arithmetic.

---

## 1. Concept Explanation

### 1.1 CPU = Datapath + Control

- **Datapath:** the actual hardware (ALU, registers, MUXes, buses) that performs operations.
- **Control unit:** generates control signals to direct datapath actions per instruction.

### 1.2 Basic Instruction Cycle

A typical instruction goes through:

```
1. Fetch (IF):  IR ← M[PC]; PC ← PC + 4
2. Decode (ID): determine operation, read registers
3. Execute (EX): ALU operation
4. Memory (MEM): load/store (if needed)
5. Write-back (WB): result → register
```

### 1.3 ALU (Arithmetic Logic Unit)

Operates on input(s) to produce output and status flags.

**Typical operations:**
- ADD, SUB
- AND, OR, XOR, NOT
- Shifts, rotates
- Compare (sets flags only)

**Status flags:** Zero (Z), Negative (N), Carry (C), Overflow (V), Parity (P).

### 1.4 ALU Building Blocks

- **Adder/Subtractor** with mode bit M:
  - Each B-bit XORed with M.
  - Cin = M.
  - M = 0: A + B; M = 1: A − B.
- **Logic unit:** parallel AND/OR/XOR/NOT with output MUX.
- **Shifter:** logical / arithmetic / rotate.

### 1.5 Register File

- Bank of registers (e.g., 32 in MIPS).
- Two read ports + one write port (typical).
- Read combinational, write on clock edge.

### 1.6 Single-Cycle Datapath

All instructions execute in **one** clock cycle.
- Clock period = longest instruction's path delay.
- Simple control but slow.

### 1.7 Multi-Cycle Datapath

Each instruction takes multiple shorter cycles. Common stages: IF, ID, EX, MEM, WB.
- Different instruction types use different # of cycles.
- Better hardware utilization than single-cycle.

### 1.8 Pipelined Datapath (preview — see pipelining_hazards.md)

5-stage pipeline (MIPS): IF, ID, EX, MEM, WB.
- Throughput = 1 instr/cycle (ideal).
- Hazards reduce performance.

### 1.9 Control Unit Types

| Type | Description |
|---|---|
| **Hardwired** | Fixed combinational logic generates control signals. Fast but inflexible. |
| **Microprogrammed** | Each instruction = sequence of microinstructions stored in ROM. Slower but flexible. |

### 1.10 Hardwired Control

- Decode opcode → activate control signals via gates / state machine.
- Used in RISC processors (simple, fast).

### 1.11 Microprogrammed Control

- **Microinstruction:** specifies control signals for one cycle.
- **Microprogram:** sequence of microinstructions per instruction.
- **Control memory (ROM):** stores microprograms.
- **Control word width:** equals # of control signals.

**Horizontal vs Vertical Microcode:**
- **Horizontal:** wider, fewer microinstructions per program (1 bit per signal).
- **Vertical:** narrower (encoded), more microinstructions, decoder needed.

### 1.12 Control Memory Sizing

- # microinstructions × control word width = total bits.
- E.g., 256 microinstructions × 32 bits = 8 Kb (1 KB).

### 1.13 Performance Equations

| Quantity | Formula |
|---|---|
| CPU time | (# instructions) × (CPI) × (clock period) |
| Clock period T | 1 / clock frequency |
| MIPS rate | (clock rate) / (CPI × 10⁶) |
| Speedup | T_old / T_new |
| Average CPI | Σ (instr_freq × CPI_i) |

### 1.14 Amdahl's Law

`Speedup = 1 / ((1 − f) + f/s)`, where f = fraction sped up, s = local speedup.

### 1.15 Integer Multiplication (Booth's Algorithm)

Booth's algorithm: signed multiplication using add/subtract-shift based on adjacent bit pairs.

**Booth recoding rules:**

| Q_i | Q_{i−1} | Action |
|---|---|---|
| 0 | 0 | Shift right |
| 0 | 1 | Add multiplicand, shift right |
| 1 | 0 | Subtract multiplicand, shift right |
| 1 | 1 | Shift right |

For n-bit numbers: n iterations.

### 1.16 Integer Division (Restoring / Non-restoring)

**Restoring division** (Q ← A/M):
1. Shift left A,Q.
2. A ← A − M.
3. If A < 0: A ← A + M; Q's lowest bit = 0.
4. Else: Q's lowest bit = 1.
5. Repeat n times.

**Non-restoring** avoids the conditional restore — fewer steps on average.

### 1.17 Floating-Point Arithmetic (IEEE 754 — preview)

**Addition (X + Y):**
1. Align exponents (shift smaller mantissa).
2. Add mantissas.
3. Normalize and round.

**Multiplication:**
1. Multiply mantissas.
2. Add exponents (subtract bias once).
3. Normalize and round.

### 1.18 Bus Architecture

- **Single bus:** simple, slow (only one transfer at a time).
- **Multi-bus:** parallel transfers, more hardware.

For single-bus CPU: each register transfer needs its own cycle.

### 1.19 Control Signals (typical)

For a register file + ALU:
- **RegRead, RegWrite**
- **MemRead, MemWrite**
- **ALUOp** (encoded)
- **ALUSrc** (which operand source)
- **MemtoReg** (write-back source: ALU vs memory)
- **PCSrc** (next-PC source)

### 1.20 Status Flags & Branching

Conditional branches read status flags from previous ALU op (CMP).

> **Summary:** Master single-cycle vs multi-cycle CPU design, hardwired vs microprogrammed control, performance equations (CPU time = N × CPI × T, MIPS, Amdahl), and ALU arithmetic algorithms (Booth, restoring division, FP add/mul).

---

## 2. Important Points

- **CPU time = N × CPI × T** is the master equation.
- **Average CPI** = weighted sum across instruction types.
- **MIPS rate** can mislead — different ISAs have different work per instruction.
- **Hardwired** control is fast but hard to modify; microprogrammed is flexible but slower.
- **Single-cycle clock period** = longest instruction's delay (worst case).
- Multi-cycle reduces clock period but adds CPI overhead.
- **Booth's algorithm** handles signed multiplication elegantly via 2-bit recoding.
- Restoring vs non-restoring division: same answer, different efficiency.
- **Floating-point alignment** loses precision in the smaller operand.
- Control signals = flat list of binary lines; control memory = sequence.
- **Horizontal microcode** is wider but faster; vertical is more compact.
- Status flags from the most recent ALU operation are used for branches.
- The **ALU + register file + memory** triad forms the datapath core.
- **Multi-bus architectures** parallelize register transfers.

---

## 3. Short Notes

```
INSTRUCTION CYCLE
 IF → ID → EX → MEM → WB

DATAPATH
 ALU + register file + MUXes + buses

CONTROL
 hardwired: fast, inflexible
 microprogrammed: flexible, slower
  horizontal: 1-bit-per-signal
  vertical: encoded + decoder

PERFORMANCE
 CPU time = N × CPI × T
 MIPS = clock_freq / (CPI × 10⁶)
 average CPI = Σ (freq × CPI_i)
 speedup = T_old / T_new

AMDAHL: speedup = 1 / ((1−f) + f/s)

ALU
 ADD/SUB/AND/OR/XOR/NOT/SHIFT
 status flags: Z, N, C, V

ADDER/SUBTRACTOR
 XOR each B with M
 Cin = M
 M=0: add; M=1: sub

REGISTER FILE
 2 read ports + 1 write port

BOOTH'S ALGORITHM
 Q_i Q_{i-1}: 00 SR; 01 +M, SR; 10 −M, SR; 11 SR

DIVISION
 restoring: shift, sub, restore if neg
 non-restoring: add or sub based on prev

FLOAT ARITHMETIC (IEEE 754)
 add: align exp, add mantissas, normalize
 mul: mul mantissas, add exp, sub bias, normalize

BUS
 single (slow), multi (fast)

CONTROL SIGNALS
 RegRead/RegWrite, MemRead/MemWrite
 ALUOp, ALUSrc, MemtoReg, PCSrc
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | CPU time = N × CPI × T | ✅✅✅ |
| 2 | T = 1/f | ✅✅ |
| 3 | MIPS = f / (CPI × 10⁶) | ✅✅ |
| 4 | Average CPI = Σ freq_i × CPI_i | ✅✅ |
| 5 | Speedup = T_old / T_new | ✅ |
| 6 | Amdahl: 1 / ((1−f) + f/s) | ✅ |
| 7 | Single-cycle period = longest instr delay | ✅ |
| 8 | Multi-cycle: cycle = max stage delay | ✅ |
| 9 | Booth's recoding rules | ✅ |
| 10 | Restoring vs non-restoring division | ✅ |
| 11 | FP add: align then add | ✅ |
| 12 | Hardwired vs microprogrammed control | ✅ |
| 13 | Horizontal vs vertical microcode | ✅ |

### Tricks

- **Average CPI shortcut:** weight each CPI by its frequency; sum.
- **Compare two designs:** compute CPU time for each; ratio = speedup.
- **Amdahl extreme limits:** if f → 1, speedup → s; if f → 0, speedup → 1.
- **Booth's algorithm cycle count:** n cycles for n-bit operation.
- **FP rounding:** can affect last bit; for GATE, often ignored.
- **For multi-cycle:** count cycles per instruction class, then total.
- **Microcode size:** count distinct microinstructions × control word width.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A CPU has clock 2 GHz. Average CPI = 1.5. Program has 10⁹ instructions. Execution time?
**Solution.** T = 10⁹ × 1.5 × (1/(2 × 10⁹)) = 1.5/2 = 0.75 s.

### Q2. (GATE CSE 2014)
A computer has CPI for instruction types: ALU 1, Load 2, Store 2, Branch 2. Frequencies: 50%, 20%, 10%, 20%. Average CPI?
**Solution.** 0.5·1 + 0.2·2 + 0.1·2 + 0.2·2 = 0.5 + 0.4 + 0.2 + 0.4 = 1.5.

### Q3. (GATE CSE 2018)
Booth's algorithm multiplies signed numbers. For multiplicand = 1011 (−5) and multiplier = 0110 (6), result?
**Solution.** −5 × 6 = −30. Booth produces same in binary 2's complement.

### Q4. (GATE CSE 2008)
Microinstruction width when 32 control signals are needed and horizontal coding is used:
**Solution.** 32 bits.

### Q5. (GATE CSE 2010)
Amdahl's law: 80% parallel, 20% serial; max speedup with infinite processors?
**Solution.** Speedup = 1 / 0.20 = 5.

### Q6. (GATE CSE 2015)
A floating-point adder works in 4 stages, each 5 ns. Pipelining throughput?
**Solution.** 1 / 5 = 0.2 G FLOPS per stage = 200 MFLOPS.

### Q7. (GATE CSE 2013)
For 5-stage pipeline ideal throughput vs single-cycle 5×: speedup?
**Solution.** Approaches 5 (for very large N).

### Q8. (GATE CSE 2007)
A single-cycle CPU has clock period 10 ns. Multi-cycle splits into 5 stages, longest 3 ns. Multi-cycle clock period?
**Solution.** 3 ns.

### Q9. (GATE CSE 2003)
Restoring division of 9 by 3. Quotient & remainder?
**Solution.** Q = 3, R = 0.

### Q10. (GATE CSE 2009)
A microprogrammed control unit has 256 micro-instructions, each 32 bits. Control memory size?
**Solution.** 256 × 32 = 8192 bits = 1 KB.

### Q11. (GATE CSE 2019)
Hardwired control compared to microprogrammed:
**Solution.** Faster but harder to modify.

### Q12. (GATE CSE 2020)
A program runs in 100 s. After optimization, 60 s of computation accelerated 2x. New time?
**Solution.** 40 + 60/2 = 70 s.

### Q13. (GATE CSE 2021)
A CPU executes instructions: 30% ALU (1 cycle), 30% Load (2 cycles), 20% Store (2 cycles), 20% Branch (3 cycles). Average CPI?
**Solution.** 0.3·1 + 0.3·2 + 0.2·2 + 0.2·3 = 0.3 + 0.6 + 0.4 + 0.6 = 1.9.

### Q14. (GATE CSE 2016)
For 5-stage MIPS pipeline, ideal CPI = ?
**Solution.** 1 (after fill).

### Q15. (GATE CSE 2011)
A CPU has 2 GHz clock, 5 GHz memory. Memory access takes 5 cycles of CPU (= 5/2 = 2.5 ns) — find effective latency.
*(Pattern: cycle conversion.)*

---

## 6. Practice Questions (20+)

### Easy

**P1.** State CPU time formula.

**P2.** Compute CPI for: 50% ALU(1), 50% Load(2).

**P3.** A CPU at 1 GHz with CPI=2 executes 10⁸ instructions. Time?

**P4.** State Amdahl's law.

**P5.** Define hardwired control.

**P6.** Define microprogrammed control.

**P7.** Number of microinstructions for 256-instruction ROM.

**P8.** Booth's algorithm: handle which type of multiplication?

**P9.** Single-cycle vs multi-cycle CPU advantage?

**P10.** State performance ranking: hardwired vs microprogrammed.

### Medium

**P11.** Average CPI: ALU 60% (1), Load 20% (2), Branch 20% (3).

**P12.** A 1 GHz CPU runs program with 10⁹ instr at avg CPI = 2. Time?

**P13.** Speedup if 50% sped up by 4x (Amdahl)?

**P14.** Multiply (10101 × 01100) using Booth's algorithm.

**P15.** Restoring division: divide 13 by 4.

**P16.** Calculate FP addition: 1.25 × 2³ + 1.5 × 2¹.

**P17.** Microprogram with 100 micro-instructions × 24 bits. Size in bytes?

**P18.** Compute pipeline speedup for 5-stage with 100 instructions.

**P19.** Determine clock period of multi-cycle if stages take 2, 3, 4, 3, 2 ns.

**P20.** Compute MIPS rate for 1 GHz, CPI = 2.

### Hard

**P21.** A pipelined CPU has 5 stages (1 ns each). 1000 instructions. Cycles? Time?

**P22.** Show Booth's algorithm produces correct signed product.

**P23.** Design control word for 30 signals, vertical encoding.

**P24.** A CPU achieves 4 GHz, CPI = 1.2. Memory access takes 4 cycles. % of time spent in memory?

**P25.** Apply Amdahl: 60% parallelizable, 4 cores. Max speedup?

**P26.** FP multiplication of (1.5 × 2²) × (1.25 × 2³).

**P27.** Microprogrammed control: each instruction takes 4 micro-cycles. CPU clock 1 GHz. Effective instruction frequency?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | N × CPI × T | direct |
| P2 | 1.5 | weighted |
| P3 | 0.2 s | 10⁸ × 2 / 10⁹ |
| P4 | as in 1.14 | direct |
| P5 | combinational logic produces control | direct |
| P6 | ROM-stored microinstructions | direct |
| P7 | 256 × control_word_width | direct |
| P8 | signed | direct |
| P9 | simple control vs better hardware utilization | direct |
| P10 | hardwired faster | direct |
| P11 | 0.6·1 + 0.2·2 + 0.2·3 = 1.6 | weighted |
| P12 | 2 s | direct |
| P13 | 1/(0.5 + 0.5/4) = 1/0.625 = 1.6 | Amdahl |
| P14 | trace Booth | algorithm |
| P15 | Q=3, R=1 | direct |
| P16 | align: 1.5×2¹ = 0.375×2³; sum = 1.625×2³ | FP add |
| P17 | 300 bytes | direct |
| P18 | 100 + 4 = 104 cycles vs 500; speedup ≈ 4.81 | pipelining |
| P19 | 4 ns | longest |
| P20 | 500 MIPS | direct |
| P21 | 1004 cycles, 1004 ns | pipeline |
| P22 | trace example | direct |
| P23 | encode 30 signals into ⌈log₂30⌉ = 5 bits + decoder | vertical |
| P24 | 4 cycles × CPI/total ratio | direct |
| P25 | 1/(0.4 + 0.6/4) = 1/0.55 ≈ 1.82 | Amdahl |
| P26 | 1.875 × 2⁵ | FP mult |
| P27 | 250 MHz | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing MIPS rate with absolute performance | MIPS doesn't account for instruction work. |
| 2 | Single-cycle CPU "wastes" clock | Period set by slowest instruction. |
| 3 | Average CPI not weighted by frequency | Always compute weighted. |
| 4 | Amdahl: ignoring speedup limit | When s → ∞, speedup limited by serial fraction. |
| 5 | Booth misapplication for unsigned | Booth handles signed properly. |
| 6 | FP normalization step skipped | Always normalize after add/mul. |
| 7 | Microprogrammed = always slower? | Modern CPUs blur the line. |
| 8 | Treating hardwired as easy to modify | It's not — needs physical redesign. |
| 9 | Control memory size: forgetting bits | bits = # instr × width. |
| 10 | Counting registers for 2-port read file | 2 read ports + 1 write port. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Compute CPU time" | N × CPI × T. |
| "Compute speedup" | Amdahl or T_old/T_new. |
| "Average CPI" | Σ freq × CPI. |
| "Pipeline cycles" | N + (k − 1) for k stages. |
| "Booth multiplication" | 2-bit recoding rules. |
| "Microinstruction count" | # cycles per instr. |
| "Control memory size" | # micro × width. |
| "FP add / mul" | Align/multiply mantissa, add/sub exp. |
| "Hardwired vs microprogrammed" | Speed vs flexibility. |
| "Multi-cycle vs single-cycle" | Clock period reduction at CPI cost. |

---

## 9. Quick Revision

```
CPU TIME = N × CPI × T
T = 1/f
MIPS = f / (CPI · 10⁶)
average CPI = Σ freq · CPI_i

AMDAHL: 1 / ((1−f) + f/s)

INSTRUCTION CYCLE
 IF → ID → EX → MEM → WB

CONTROL
 hardwired: fast, fixed
 microprogrammed: flexible, slower
  horizontal: wide, fast
  vertical: narrow, decoded

ALU
 ADD/SUB/AND/OR/XOR/NOT/SHIFT
 flags: Z, N, C, V
 add/sub: XOR + Cin = M

BOOTH (signed mult, 2-bit recode)
 00, 11: SR
 01: +M, SR
 10: −M, SR

DIVISION
 restoring: subtract; restore if neg
 non-restoring: add or sub on previous sign

FLOAT (IEEE 754)
 add: align exp, add, normalize
 mul: mul mant, add exp, sub bias, normalize

BUS: single (slow), multi (fast)
CONTROL SIGNALS: RegRead/Write, MemRead/Write, ALUOp, ALUSrc, MemtoReg, PCSrc
```
