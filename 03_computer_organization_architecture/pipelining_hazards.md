# Pipelining & Hazards

> Subject: Computer Organization & Architecture (COA)
> GATE weight: **3–6 marks** every year. Pipeline cycle counting, hazards (data/control/structural), forwarding, branch handling.

---

## 1. Concept Explanation

### 1.1 Pipelining Idea

Overlap execution of instructions. Each instruction proceeds through stages; multiple instructions occupy different stages simultaneously.

**Classic 5-stage MIPS pipeline:**

| Stage | Action |
|---|---|
| **IF** | Instruction Fetch |
| **ID** | Instruction Decode + Register Read |
| **EX** | Execute (ALU op or address calc) |
| **MEM** | Memory access (if load/store) |
| **WB** | Write back result to register |

### 1.2 Pipeline Performance

**Sequential (non-pipelined):** total time = N · k · T_stage (where k stages per instruction, all run in series).

**Pipelined (no hazards):** total time = (N + k − 1) · T_stage.

**Speedup:**

`S = (N · k · T_stage) / ((N + k − 1) · T_stage) = (N · k)/(N + k − 1)`

**Limit (large N):** S → k.

**Throughput (steady state):** 1 instruction / cycle.

### 1.3 Pipeline Cycle Time

`T_pipe = max(T_stage_i) + T_register`

The slowest stage limits throughput. T_register is FF setup overhead.

### 1.4 Pipeline Stalls and Hazards

| Hazard | Cause |
|---|---|
| **Structural** | Hardware resource conflict (e.g., single memory port, single ALU). |
| **Data** | One instruction depends on result of an earlier (not-yet-complete) instruction. |
| **Control (branch)** | Branch outcome unknown until later stages. |

### 1.5 Structural Hazards

Multiple instructions need the same resource simultaneously.

**Examples:**
- IF and MEM both access memory (same port).
- Single FP unit used by two instructions.

**Fix:**
- Duplicate hardware (separate I-cache and D-cache — Harvard architecture).
- Stall.

### 1.6 Data Hazards

Three types:

| Type | Description | Example |
|---|---|---|
| **RAW** (true) | Read After Write | I2 reads value I1 writes |
| **WAR** (anti) | Write After Read | I2 writes register I1 reads |
| **WAW** (output) | Write After Write | I2 writes register I1 also writes |

In simple in-order pipeline, only **RAW** is a problem (WAR/WAW arise in out-of-order execution).

### 1.7 RAW Hazard Example

```
ADD R1, R2, R3     ; R1 = R2 + R3 (WB at cycle 5)
SUB R4, R1, R5     ; R4 = R1 − R5 (needs R1 at cycle 3 ID/EX)
```

I2 needs R1 before I1 writes it back. Without intervention → wrong result.

### 1.8 Forwarding (Bypassing)

Pass result from EX/MEM register directly to ALU input of next instruction — no need to wait for WB.

**Forwarding paths:**
- **EX → EX** (ALU output in EX/MEM register forwarded back to ALU input).
- **MEM → EX** (loaded value in MEM/WB forwarded back).

Forwarding **eliminates** most RAW stalls — except the **load-use** hazard.

### 1.9 Load-Use Hazard

```
LW R1, 0(R2)     ; loads R1 in MEM stage (cycle 4)
ADD R3, R1, R4   ; needs R1 in EX (cycle 3)
```

Even with forwarding, you can't bypass from MEM (cycle 4) to EX (cycle 3) — one cycle stall is unavoidable.

**Compiler reordering** can hide this stall.

### 1.10 Control Hazards

Branches: outcome (taken/not taken) and target known late (typically end of EX or MEM).
- Default: stall or flush instructions in pipeline.

### 1.11 Branch Handling Techniques

| Technique | Description |
|---|---|
| **Stall (freeze)** | Hold pipeline until branch resolved. Penalty = pipeline stages until branch resolution. |
| **Predict not-taken** | Always assume branch falls through; squash on miss. |
| **Predict taken** | Always assume branch taken; squash on miss. |
| **Delayed branch** | Reschedule one instruction after branch (delay slot) — runs regardless. |
| **Branch prediction (dynamic)** | Use history (1-bit, 2-bit predictors, BTB) to guess outcome. |
| **Branch Target Buffer (BTB)** | Cache of recent branch targets. |

**Cost of branch misprediction = # bubbles inserted = # stages until resolution.**

### 1.12 Branch Resolution Stage

In classic MIPS:
- Branch decision in **EX** (or **ID** with extra hardware).
- Earlier resolution = fewer bubbles.

If decision in stage *e* and branch starts at stage 1:
- Bubbles per misprediction = (e − 1).

### 1.13 Multi-Cycle / Variable-Latency Stages

If a stage takes multiple cycles (e.g., FP multiply taking 4 cycles), pipeline stalls or uses pipelined functional units.

### 1.14 Performance Calculations

**Effective CPI:**
`CPI_pipe = 1 + stall_cycles_per_instruction`

**Stall cycles = (frequency of hazard) × (penalty)**.

### 1.15 Superscalar & Out-of-Order

- **Superscalar:** issue >1 instruction per cycle.
- **Out-of-order:** execute independent instructions early.
- **Register renaming** eliminates WAR/WAW hazards.

### 1.16 Pipeline Diagram (Time-Stage Chart)

```
Cycle:    1   2   3   4   5   6   7   8
I1:      IF  ID  EX MEM  WB
I2:           IF  ID  EX MEM WB
I3:                IF  ID  EX MEM WB
I4:                    IF  ID  EX MEM WB
```

For a stall, insert "—" (bubble) and shift later instructions.

### 1.17 Pipeline Speedup with Frequency

If pipelining doubles clock rate (each stage faster) and incurs CPI_eff:
`Speedup = (T_old) / (T_new)`
where T_new uses faster clock and possibly higher CPI.

> **Summary:** Master 5-stage MIPS, hazard types (RAW/WAR/WAW + structural + control), forwarding, load-use stall, branch handling. Pipeline cycle count = N + k − 1 (no hazards); add stalls for hazards.

---

## 2. Important Points

- **Speedup limit** = k (number of stages) for very large N.
- **Throughput** of ideal pipeline = 1 instruction per cycle.
- **CPI_pipe = 1** ideally; > 1 with hazards.
- **In-order pipelines** suffer only **RAW** data hazards.
- **Forwarding** eliminates most RAW stalls — except load-use.
- **Load-use stall is 1 cycle** in classic MIPS (cannot be forwarded).
- **Branch penalty = # cycles until resolution − 1** (stages skipped after branch).
- **Delay slot** is architecturally visible — programmer/compiler must fill it.
- **Branch prediction** dynamic predictors achieve > 95% accuracy.
- **Structural hazards** prevented by **separate I-cache and D-cache**.
- **WAW and WAR** appear only in out-of-order execution.
- **Register renaming** removes false dependencies (WAR, WAW).
- **Pipeline cycles for N instructions, k stages, no stalls** = N + k − 1.
- **Pipeline cycle time** ≥ longest stage delay + register overhead.
- Misalignment between pipeline depth and clock speed → diminishing returns.

---

## 3. Short Notes

```
PIPELINE
 5-stage MIPS: IF, ID, EX, MEM, WB
 throughput: 1 / cycle (ideal)
 no-hazard cycles for N instr: N + k − 1
 speedup → k for large N
 cycle time = max(stage_delay) + register

HAZARDS
 structural: HW resource conflict
 data:
   RAW: read after write (true)
   WAR: write after read (anti)
   WAW: write after write (output)
 control: branch outcome unknown

DATA HAZARD FIXES
 forwarding: EX→EX, MEM→EX
 load-use: 1 stall (unavoidable with simple FW)
 compiler reorder

CONTROL HAZARD FIXES
 stall (freeze)
 predict not-taken / taken
 delayed branch (delay slot)
 dynamic prediction (1-bit, 2-bit, BTB)

PENALTY
 misprediction = # bubbles = stages-until-resolution

OUT-OF-ORDER
 register renaming → removes WAR, WAW
 superscalar: > 1 instr/cycle

CPI_pipe = 1 + stall_cycles_per_instr
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | Pipeline cycles (no hazards) = N + k − 1 | ✅✅✅ |
| 2 | Speedup = (N · k)/(N + k − 1) → k | ✅✅ |
| 3 | Throughput = 1/T_cycle (ideal) | ✅ |
| 4 | T_cycle = max(stage delay) + reg overhead | ✅ |
| 5 | CPI_pipe = 1 + stall_cycles_per_instr | ✅✅ |
| 6 | Stall cycles per instruction = freq × penalty | ✅ |
| 7 | Load-use stall = 1 cycle | ✅✅ |
| 8 | Branch penalty = stages-until-resolution − 1 (≈ k − 1 worst) | ✅ |
| 9 | Speedup with branch penalty: (1)/(1 + b · p) where b = branch freq, p = penalty | ✅ |
| 10 | Forwarding eliminates most RAW stalls | ✅ |

### Tricks

- **For non-pipelined comparison:** total cycles = N · k.
- **Pipeline filling time:** k − 1 cycles before steady-state.
- **Load-use stall fix:** insert independent instruction between load and use.
- **Branch resolution earlier (e.g., ID stage):** reduces penalty to 0–1 cycle.
- **For mixed instructions with different stalls:** compute weighted avg.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A 5-stage pipeline with each stage 1 ns. 1000 instructions, no hazards. Total time?
**Solution.** (1000 + 4) · 1 = 1004 ns.

### Q2. (GATE CSE 2014)
A non-pipelined CPU runs at 100 MHz, CPI=4. Pipelining 5 stages each runs at 100 MHz. Speedup for 1000 instructions?
**Solution.**
- Non-pipelined: 1000 · 4 = 4000 cycles.
- Pipelined (no hazard): 1000 + 4 = 1004 cycles.
- Speedup = 4000 / 1004 ≈ 3.98.

### Q3. (GATE CSE 2018)
A 4-stage pipeline has stage delays 5, 6, 11, 8 ns. Cycle time?
**Solution.** Max = 11 ns (+ reg overhead, often ignored).

### Q4. (GATE CSE 2008)
RAW hazard between two instructions in 5-stage pipeline. Stalls if no forwarding?
**Solution.** Up to 3 cycles (depends on producer/consumer stages).

### Q5. (GATE CSE 2010)
Load-use hazard with forwarding: stalls?
**Solution.** 1 cycle.

### Q6. (GATE CSE 2015)
Branch resolved in EX (3rd stage). Misprediction penalty?
**Solution.** 2 cycles.

### Q7. (GATE CSE 2013)
Pipelining 5 stages, 20% branches, branch misprediction rate 30%, penalty 2 cycles. Effective CPI?
**Solution.** CPI = 1 + 0.2 · 0.3 · 2 = 1 + 0.12 = 1.12.

### Q8. (GATE CSE 2007)
Non-pipelined CPU: clock 1 GHz, CPI 4. Pipelined: 5-stage clock 1 GHz, CPI 1.2. Speedup?
**Solution.** 4/1.2 ≈ 3.33.

### Q9. (GATE CSE 2003)
A 4-stage pipeline: stage 1, 3, 5, 7 ns. Bottleneck stage?
**Solution.** Stage 4 (7 ns).

### Q10. (GATE CSE 2009)
WAW hazard occurs in:
**Solution.** Out-of-order or multi-issue pipelines.

### Q11. (GATE CSE 2019)
A pipeline takes 100 ns to fill, then runs at 1 instruction per 5 ns. After 1 second, # instructions completed?
**Solution.** Time at steady state ≈ 1 s − 100 ns ≈ 1 s; instructions ≈ 200 million.

### Q12. (GATE CSE 2020)
Delayed branch with one delay slot: how many cycles wasted on branch?
**Solution.** 0 (if delay slot filled with useful instruction); 1 (if NOP).

### Q13. (GATE CSE 2021)
Forwarding eliminates which RAW stall:
**Solution.** All except load-use.

### Q14. (GATE CSE 2016)
A 5-stage pipeline with frequencies: 60% ALU, 20% Load, 10% Store, 10% Branch. Load-use stall = 1, branch misprediction (30%) = 2. CPI?
**Solution.** Assume 50% load-use = 0.2·0.5·1 = 0.1; branch = 0.1·0.3·2 = 0.06. CPI = 1 + 0.1 + 0.06 = 1.16.

### Q15. (GATE CSE 2011)
Speedup with infinite pipeline depth?
**Solution.** Limited by branch + stall overheads; not infinite.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define pipeline.

**P2.** State the 5-stage MIPS pipeline.

**P3.** Pipeline cycles for 100 instructions in a 5-stage pipeline (no hazards)?

**P4.** Throughput of ideal pipeline?

**P5.** Define RAW hazard.

**P6.** What is forwarding?

**P7.** Load-use stall is how many cycles in classic MIPS?

**P8.** Define structural hazard.

**P9.** Branch in 5-stage MIPS resolved in which stage?

**P10.** State formula for pipeline cycles.

### Medium

**P11.** Pipeline stages 4, 5, 7, 6 ns. Cycle time?

**P12.** Speedup of 5-stage pipeline for 1000 instructions vs sequential?

**P13.** Pipeline with 30% load-use, 1-cycle stall. CPI?

**P14.** Delayed branch reduces penalty by how much?

**P15.** Compute non-pipelined cycles for 100 instr in 5-stage where each stage = 1 ns.

**P16.** Branch frequency 25%, misprediction rate 20%, penalty 3. Stall CPI?

**P17.** A 4-stage pipeline has max delay 6 ns; reg overhead 1 ns. Cycle time?

**P18.** Show pipeline diagram for 4 instructions in 5-stage MIPS.

**P19.** Which hazards need register renaming?

**P20.** Pipeline filling time for 5-stage pipeline?

### Hard

**P21.** A pipeline with 2 ns stages, 30% branches with 25% misprediction (penalty 2), 25% loads with 30% load-use stall. Effective CPI?

**P22.** Compare in-order vs out-of-order CPI for a workload with mostly RAW hazards.

**P23.** Pipeline reorganization: which stage to move branch decision to for minimum penalty?

**P24.** Compute speedup of pipelined CPU @ 2 GHz vs non-pipelined @ 500 MHz, both with same CPI.

**P25.** A pipeline with 7 stages reduces clock to 200 ps from 1 ns. Speedup?

**P26.** Show that load-use stall is unavoidable with simple forwarding.

**P27.** Compute total cycles for 100 instructions with 10% load-use (1 stall) and 5% branch misprediction (2 stalls) in a 5-stage MIPS pipeline.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | overlapping execution | direct |
| P2 | IF, ID, EX, MEM, WB | direct |
| P3 | 100 + 4 = 104 | direct |
| P4 | 1 / cycle | ideal |
| P5 | read after write | direct |
| P6 | bypass result earlier | direct |
| P7 | 1 | direct |
| P8 | resource conflict | direct |
| P9 | EX | classic MIPS |
| P10 | N + k − 1 | direct |
| P11 | 7 ns | max |
| P12 | (1000·5)/(1004) ≈ 4.98 | direct |
| P13 | 1 + 0.3·1 = 1.3 | weighted |
| P14 | 1 cycle if slot filled | direct |
| P15 | 500 cycles | direct |
| P16 | 0.25·0.2·3 = 0.15 | weighted |
| P17 | 7 ns | direct |
| P18 | trace | direct |
| P19 | WAR, WAW | direct |
| P20 | k − 1 = 4 | direct |
| P21 | CPI = 1 + 0.3·0.25·2 + 0.25·0.3·1 = 1 + 0.15 + 0.075 = 1.225 | weighted |
| P22 | OoO better with renaming + many independent instructions | direct |
| P23 | earlier (e.g., ID) | direct |
| P24 | depends on CPI | direct |
| P25 | scale by clock | direct |
| P26 | load completes in MEM (stage 4) but consumer needs in EX (stage 3) → 1 stall | direct |
| P27 | 100 + 4 + 0.10·100·1 + 0.05·100·2 = 124 | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting filling time (k − 1 cycles) | Include in formula. |
| 2 | Treating CPI = 1 with hazards | Add stall cycles. |
| 3 | Confusing WAR/WAW with RAW | Only RAW in in-order pipelines. |
| 4 | Forwarding fixes load-use | It doesn't — 1-cycle stall remains. |
| 5 | Branch resolution stage assumed always EX | Could be ID with extra hardware. |
| 6 | Treating branch frequency = misprediction frequency | Multiply both. |
| 7 | Assuming infinite pipeline = infinite speedup | Diminishing returns due to hazards. |
| 8 | Cycle time = sum of stage delays (wrong) | Cycle = max stage delay. |
| 9 | Ignoring register file overhead | Adds to T_cycle. |
| 10 | Flushing entire pipeline on every branch | Only on misprediction. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Pipeline cycles for N instructions, k stages, no hazards" | N + k − 1. |
| "Speedup of pipelining" | (N·k)/(N+k−1). |
| "Cycle time of pipeline" | max stage delay (+ register overhead). |
| "Effective CPI" | 1 + stall_cycles_per_instruction. |
| "Load-use hazard" | 1 cycle stall in classic 5-stage. |
| "Branch misprediction penalty" | branches × misprediction × penalty added to CPI. |
| "Forwarding" | Eliminates most RAW stalls (not load-use). |
| "WAR/WAW" | Out-of-order execution; renaming. |
| "Structural hazard" | Hardware duplication (Harvard arch). |
| "Delay slot filled" | No effective branch penalty. |

---

## 9. Quick Revision

```
5-STAGE MIPS: IF, ID, EX, MEM, WB

Pipeline cycles (no hazard):
 N + k − 1

Speedup → k for large N
Throughput = 1 / cycle (ideal)
T_cycle = max(stage_delay) + reg_overhead

HAZARDS
 structural: HW conflict (separate caches)
 data:
  RAW: read after write (in-order pb)
  WAR / WAW: only OoO
 control: branch unresolved

FIXES
 forwarding: EX→EX, MEM→EX
 load-use: 1 stall (irreducible)
 branch:
  stall, predict (taken/not), delayed slot, dynamic predictor

CPI_pipe = 1 + stall/instr
stall = frequency × penalty

OUT-OF-ORDER
 register renaming → kills WAR, WAW
 superscalar: > 1 instr/cycle
```
