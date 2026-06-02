# Sequential Circuits (Flip-Flops, Counters, Registers)

> Subject: Digital Logic
> GATE weight: **2–4 marks** every year. Latches/FFs, state diagrams, counters, FSM design.

---

## 1. Concept Explanation

### 1.1 Sequential vs Combinational

A **sequential circuit** has memory: output depends on **inputs + present state**.

```
                 ┌────────────┐
   inputs ──────►│    Comb.   │──── outputs
                 │   Logic    │
                 └─────┬──────┘
                       │ next state
                ┌──────▼──────┐
                │   Memory    │
                │  (FF/latch) │
                └──────┬──────┘
                       │ present state
                       ▼  (feedback)
```

### 1.2 Latch vs Flip-Flop

| Type | Triggering |
|---|---|
| **Latch** | Level-triggered (transparent when enable = 1) |
| **Flip-Flop** | Edge-triggered (samples on clock edge only) |

Most modern designs use edge-triggered FFs to avoid glitches.

### 1.3 SR Latch (NOR / NAND)

**NOR-based SR latch:**

| S | R | Q (next) |
|---|---|---|
| 0 | 0 | Q (hold) |
| 0 | 1 | 0 (reset) |
| 1 | 0 | 1 (set) |
| 1 | 1 | invalid |

**NAND-based SR latch** uses inverted inputs (S' R').

### 1.4 D Latch / D Flip-Flop

`D = data` input; on enable/clock, Q = D.

**D Flip-Flop characteristic equation:**
`Q(t+1) = D`

| D | Q(t+1) |
|---|---|
| 0 | 0 |
| 1 | 1 |

### 1.5 JK Flip-Flop

Most flexible: handles all four input combinations.

| J | K | Q(t+1) |
|---|---|---|
| 0 | 0 | Q (hold) |
| 0 | 1 | 0 (reset) |
| 1 | 0 | 1 (set) |
| 1 | 1 | Q' (toggle) |

**Characteristic equation:** `Q(t+1) = JQ' + K'Q`.

### 1.6 T Flip-Flop

`T = toggle` input. JK with J = K = T.

| T | Q(t+1) |
|---|---|
| 0 | Q |
| 1 | Q' |

**Characteristic equation:** `Q(t+1) = T ⊕ Q`.

### 1.7 Excitation Tables

Used to design FFs from desired state transitions.

**SR FF:**
| Q(t) | Q(t+1) | S | R |
|---|---|---|---|
| 0 | 0 | 0 | X |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | X | 0 |

**JK FF:**
| Q(t) | Q(t+1) | J | K |
|---|---|---|---|
| 0 | 0 | 0 | X |
| 0 | 1 | 1 | X |
| 1 | 0 | X | 1 |
| 1 | 1 | X | 0 |

**D FF:** simple — D = Q(t+1).

**T FF:** T = Q(t) ⊕ Q(t+1).

### 1.8 Master-Slave Configuration

Two latches in series, alternately enabled. Eliminates race-around in JK FF for J=K=1.

### 1.9 Setup & Hold Time

- **Setup time (t_setup):** input must be stable **before** clock edge.
- **Hold time (t_hold):** input must remain stable **after** clock edge.
- Violating either ⇒ metastability.
- **Propagation delay (t_pd):** delay from clock edge to output stable.

**Maximum clock frequency** for a register-to-register path:
`T_clk ≥ t_pd + t_comb + t_setup`
where t_comb is combinational delay.

### 1.10 Counters

Sequential circuits cycling through a sequence of states.

**Asynchronous (Ripple) Counter:**
- FFs cascaded; each output triggers next.
- Slow due to ripple delay.
- For mod-N: needs additional logic.
- n FFs ⇒ counts 0 to 2ⁿ − 1.

**Synchronous Counter:**
- All FFs share the same clock.
- Faster, more stable.
- Requires more logic per FF.

**Mod-N counter:** counts 0 to N−1; needs ⌈log₂N⌉ FFs.

### 1.11 Common Counters

| Counter | Count Sequence |
|---|---|
| Mod-2 (1 FF) | 0, 1 |
| Mod-4 (2 FFs) | 0, 1, 2, 3 |
| Mod-8 (3 FFs) | 0–7 |
| Mod-10 (4 FFs, BCD) | 0–9 |
| Up/Down | both directions |
| Ring counter | circular shift of single 1 |
| Johnson counter | "twisted ring": shifts inverted MSB |

**Johnson counter (n FFs):** 2n unique states.
**Ring counter (n FFs):** n unique states.

### 1.12 Shift Registers

n FFs in series; data shifts on clock edge.

| Type | Description |
|---|---|
| SISO | serial-in serial-out |
| SIPO | serial-in parallel-out |
| PISO | parallel-in serial-out |
| PIPO | parallel-in parallel-out |
| Bidirectional | shifts left or right |

**Universal shift register:** modes for all directions and parallel load.

### 1.13 Finite State Machine (FSM)

| Type | Output depends on |
|---|---|
| **Mealy** | Inputs **and** state |
| **Moore** | State only |

**FSM design steps:**
1. Identify states.
2. Build state diagram.
3. State assignment (binary encoding).
4. Build state transition table.
5. Use FF excitation tables to derive next-state and output logic.

### 1.14 Race Condition & Metastability

- **Race-around:** in JK level-triggered with J=K=1, output toggles continuously while clock high.
- **Solution:** master-slave or edge-triggered FFs.
- **Metastability:** FF stuck in undefined state; resolves probabilistically.

### 1.15 Number of FFs Required

For a counter with N states: `⌈log₂ N⌉` FFs.

For mod-12 counter: 4 FFs (since 2³ < 12 < 2⁴).

> **Summary:** Master FF characteristic + excitation tables (D, T, SR, JK). Asynchronous = ripple, synchronous = parallel. Ring (n states) and Johnson (2n states). FSM: Mealy vs Moore. Setup/hold/clock period.

---

## 2. Important Points

- **Latch is level-triggered**, **FF is edge-triggered**.
- D FF: `Q(t+1) = D`. Simplest.
- JK characteristic: `Q(t+1) = JQ' + K'Q`.
- T FF: `Q(t+1) = T ⊕ Q`.
- **JK with J = K = 1 toggles** — basis for counters.
- Race-around in JK avoided via master-slave (level) or edge-triggering.
- **n-bit ripple counter:** worst-case delay ≈ n × t_pd.
- **Mod-N counter** needs `⌈log₂ N⌉` FFs.
- Ring counter (n FFs) → n states; Johnson counter (n FFs) → 2n states.
- **Setup time before edge; hold time after.**
- Max clock freq = 1 / (t_pd + t_comb + t_setup).
- Mealy ≤ Moore in number of states (Mealy may have fewer).
- All FFs have a characteristic equation derived from truth table — memorize these.

---

## 3. Short Notes

```
LATCH vs FF
 latch: level-triggered (transparent when enable)
 FF: edge-triggered (samples on edge)

CHARACTERISTIC EQUATIONS
 D:  Q+ = D
 T:  Q+ = T ⊕ Q
 JK: Q+ = JQ' + K'Q
 SR: Q+ = S + R'Q (with SR=0)

EXCITATION
 SR: 00→0X, 01→10, 10→01, 11→X0
 JK: 00→0X, 01→1X, 10→X1, 11→X0
 D = Q+
 T = Q ⊕ Q+

TIMING
 t_setup: stable before edge
 t_hold: stable after edge
 t_pd: clock-to-Q delay
 T_clk ≥ t_pd + t_comb + t_setup

COUNTERS
 mod-N needs ⌈log₂ N⌉ FFs
 ripple: cascaded, slow
 sync: shared clock, fast
 ring (n FFs): n states
 Johnson (n FFs): 2n states

SHIFT REGISTERS
 SISO, SIPO, PISO, PIPO

FSM
 Mealy: out = f(state, input)
 Moore: out = f(state)
 design: states → diagram → table → FF logic

RACE-AROUND
 JK level-triggered with J=K=1
 fix: master-slave / edge-triggered

METASTABILITY
 setup/hold violation
```

---

## 4. Formulas / Tricks

| # | Formula / Rule | Memorize Cold? |
|---|---|---|
| 1 | D FF: Q+ = D | ✅✅ |
| 2 | T FF: Q+ = T ⊕ Q | ✅✅ |
| 3 | JK FF: Q+ = JQ' + K'Q | ✅✅ |
| 4 | SR FF (with SR ≠ 11): Q+ = S + R'Q | ✅ |
| 5 | Excitation tables for D, T, SR, JK | ✅✅ |
| 6 | T_clk ≥ t_pd + t_comb + t_setup | ✅✅ |
| 7 | Max f_clk = 1 / T_clk | ✅ |
| 8 | n-bit ripple delay = n · t_pd | ✅ |
| 9 | Mod-N counter: ⌈log₂ N⌉ FFs | ✅✅ |
| 10 | Ring (n FFs) = n states; Johnson = 2n | ✅✅ |
| 11 | JK with J=K=1 toggles | ✅✅ |
| 12 | Mealy vs Moore | ✅ |

### Tricks

- **Designing a counter:** state table → excitation table per FF → K-map for FF inputs.
- **JK to D conversion:** D = JQ' + K'Q.
- **D to JK conversion:** J = D, K = D' (with same Q).
- **T to JK:** J = K = T.
- **Frequency division:** a T FF with T=1 toggles every clock — divides by 2.
- **n-bit binary counter as freq divider:** divides by 2ⁿ.
- **For asynchronous counter to skip states (mod-N where N ≠ 2ᵏ):** use AND gate + reset.
- **Setup/hold violation hardware risk:** cascade synchronizing FFs.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A 4-bit synchronous counter with T FFs counts from 0 to 15. State 7 transitions to:
**Solution.** 8 (binary 0111 → 1000): all bits toggle when their lower bits are all 1. T₀=1 always, T₁=Q₀, T₂=Q₀Q₁, T₃=Q₀Q₁Q₂.

### Q2. (GATE CSE 2014)
Number of FFs to design a mod-12 counter:
**Solution.** ⌈log₂ 12⌉ = 4.

### Q3. (GATE CSE 2018)
A 4-bit ring counter has how many states?
**Solution.** 4.

### Q4. (GATE CSE 2008)
Johnson counter with 4 FFs has how many states?
**Solution.** 8.

### Q5. (GATE CSE 2010)
Excitation input for JK FF: Q(t) = 0, Q(t+1) = 1?
**Solution.** J = 1, K = X.

### Q6. (GATE CSE 2015)
For a D FF in feedback loop with t_pd = 5 ns, t_setup = 2 ns, t_comb = 8 ns. Max clock frequency?
**Solution.** T_clk ≥ 5 + 8 + 2 = 15 ns; f_max = 1/15 ns ≈ 66.7 MHz.

### Q7. (GATE CSE 2013)
A JK flip-flop with J = K = 1 acts as:
**Solution.** Toggle (T) flip-flop.

### Q8. (GATE CSE 2007)
The characteristic equation of D FF is:
**Solution.** Q(t+1) = D.

### Q9. (GATE CSE 2003)
A binary counter has 8 FFs. How many distinct count values?
**Solution.** 256.

### Q10. (GATE CSE 2009)
A FSM has 5 states. Minimum # of FFs for state encoding:
**Solution.** ⌈log₂ 5⌉ = 3.

### Q11. (GATE CSE 2019)
A 4-bit asynchronous counter with 1 ns FF delay. Worst-case ripple delay?
**Solution.** 4 ns.

### Q12. (GATE CSE 2020)
A T FF with T = 1 has clock 100 MHz. Output frequency?
**Solution.** 50 MHz (divide-by-2).

### Q13. (GATE CSE 2021)
A Mealy machine vs Moore machine: which has more states (typically)?
**Solution.** Moore — output depends on state only, so more states needed for same I/O behavior.

### Q14. (GATE CSE 2016)
JK FF with J=1, K=0: next state?
**Solution.** Q+ = 1 (set).

### Q15. (GATE CSE 2011)
Maximum frequency of operation of a 32-bit ripple counter, given each FF has 5 ns delay:
**Solution.** 1 / (32 · 5 ns) = 1/160 ns ≈ 6.25 MHz (worst case for last bit visibility).

---

## 6. Practice Questions (20+)

### Easy

**P1.** D FF: Q(t) = 0, D = 1. Q(t+1) = ?

**P2.** JK FF: J = 0, K = 0. Q(t+1) = ?

**P3.** T FF: T = 1, Q(t) = 1. Q(t+1) = ?

**P4.** Number of FFs for mod-32 counter.

**P5.** Number of unique states in 5-bit ring counter.

**P6.** Number of states in 5-bit Johnson counter.

**P7.** SR FF: S = 1, R = 0. Q(t+1) = ?

**P8.** Difference between latch and flip-flop.

**P9.** Number of FFs in 4-bit shift register.

**P10.** Output of a T FF with T = 1 and 100 MHz clock.

### Medium

**P11.** Design a 3-bit synchronous counter using T FFs.

**P12.** Convert JK FF to D FF.

**P13.** Convert D FF to T FF.

**P14.** Show why JK with J = K = 1 has race-around in level-triggered version.

**P15.** Compute max clock freq: t_pd = 4, t_comb = 6, t_setup = 1 (all ns).

**P16.** Design a mod-6 counter.

**P17.** State diagram for a 1-bit sequence detector (detect "101").

**P18.** Mealy vs Moore for sequence "11" detection.

**P19.** Implement T FF using D FF.

**P20.** Implement D FF using JK FF.

### Hard

**P21.** Show the master-slave JK FF eliminates race-around.

**P22.** Design a 4-bit up/down counter with mode bit M.

**P23.** Design a synchronous mod-10 counter (BCD).

**P24.** Determine the number of FFs in a circuit that detects "1101".

**P25.** A finite state machine has output Y = 1 iff input string ends in "00". Minimum states (Mealy and Moore)?

**P26.** State table for a Johnson counter (4-bit).

**P27.** Design a 4-bit shift register that loads parallel data on `Load = 1`, shifts on `Load = 0`.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 1 | direct |
| P2 | Q (hold) | direct |
| P3 | 0 | toggle |
| P4 | 5 | log₂ 32 |
| P5 | 5 | ring |
| P6 | 10 | 2n |
| P7 | 1 (set) | direct |
| P8 | latch level, FF edge | direct |
| P9 | 4 | shift register |
| P10 | 50 MHz | divide-by-2 |
| P11 | T₀=1, T₁=Q₀, T₂=Q₀Q₁ | sync count |
| P12 | D = JQ' + K'Q | use char eq |
| P13 | T = D ⊕ Q | derived |
| P14 | clock high → JK toggles repeatedly | race |
| P15 | T = 4+6+1 = 11 ns; f = 91 MHz | direct |
| P16 | 3 FFs; reset on count = 6 | async / sync |
| P17 | 4 states (S0, S1, S10, S101) | FSM |
| P18 | Mealy 2 states; Moore 3 states | typical |
| P19 | D = T ⊕ Q | conversion |
| P20 | J = D, K = D' | conversion |
| P21 | master samples on rising edge; slave on falling — never both transparent | master-slave |
| P22 | XOR each next-state with M | up/down |
| P23 | reset on 1010; standard BCD design | direct |
| P24 | 4 FFs (states for prefixes of 1101) | FSM |
| P25 | Mealy 2, Moore 3 | typical |
| P26 | 8 states cycling | direct |
| P27 | mode bit selects shift vs load | universal SR |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing latch with edge-triggered FF | Latch is level-triggered. |
| 2 | Forgetting race-around in level-triggered JK | Use master-slave or edge-triggered. |
| 3 | Wrong characteristic equation | Memorize D, T, JK, SR. |
| 4 | Underestimating # FFs for mod-N | Use ⌈log₂ N⌉. |
| 5 | Confusing ring (n) and Johnson (2n) | Ring shifts; Johnson inverts MSB. |
| 6 | Setup/hold time confusion | Setup before edge, hold after. |
| 7 | Mealy fewer outputs than Moore — accidentally swap | Mealy depends on inputs too. |
| 8 | Forgetting clock period includes both FF delay and combinational | Sum all. |
| 9 | Treating async counter as fast | Async = ripple = slow. |
| 10 | Wrong state encoding | Keep distinct states distinct. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "FF with toggle behavior" | T or JK with J=K=1. |
| "Most flexible FF" | JK. |
| "Counter modulo N" | ⌈log₂ N⌉ FFs. |
| "Ring vs Johnson" | n vs 2n states. |
| "Sequence detector" | FSM design (Mealy/Moore). |
| "Max clock freq" | 1/(t_pd + t_comb + t_setup). |
| "Convert FF X to FF Y" | Use characteristic + excitation tables. |
| "Race-around" | JK level-triggered with J=K=1. |
| "Frequency division by k" | Use chain of T FFs (k = 2ⁿ) or mod-k counter. |
| "Output depends on state and input" | Mealy. |

---

## 9. Quick Revision

```
LATCH (level) vs FF (edge)

CHARACTERISTIC
 D: Q+ = D
 T: Q+ = T ⊕ Q
 JK: Q+ = JQ' + K'Q
 SR: Q+ = S + R'Q (SR=0 valid)

EXCITATION (Q→Q+)
 D: Q+
 T: Q ⊕ Q+
 JK: 00→0X, 01→1X, 10→X1, 11→X0
 SR: 00→0X, 01→10, 10→01, 11→X0

TIMING
 setup (before edge)
 hold (after edge)
 t_pd (clock to Q)
 T_clk ≥ t_pd + t_comb + t_setup

COUNTERS
 ⌈log₂ N⌉ FFs for mod-N
 ripple (slow), sync (fast)
 ring n FFs → n states
 Johnson n FFs → 2n states

SHIFT REGISTERS
 SISO/SIPO/PISO/PIPO
 universal: load + direction

FSM
 Mealy: out = f(state, input)
 Moore: out = f(state)

RACE-AROUND
 JK level + J=K=1
 fix: master-slave / edge-triggered
```
