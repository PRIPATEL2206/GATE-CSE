# Runtime Environment & Code Generation

> Subject: Compiler Design
> GATE weight: **1–3 marks** every year. Stack frames, parameter passing, register allocation, peephole optimization.

---

## 1. Concept Explanation

### 1.1 Runtime Environment

Manages execution-time data: **memory layout, activation records, parameter passing, dynamic allocation**.

### 1.2 Memory Layout (typical)

```
HIGH ADDRESS
+------------------+
|     Stack        |  ← grows down
|------------------|
|     Heap         |  ← grows up (malloc/new)
|------------------|
|  Static / BSS    |  ← initialized/uninitialized globals
|------------------|
|     Code (Text)  |  ← read-only program code
+------------------+
LOW ADDRESS
```

### 1.3 Storage Allocation Strategies

| Strategy | When |
|---|---|
| **Static** | At compile time; size known (globals, static locals) |
| **Stack** | LIFO; for activation records (function calls) |
| **Heap** | Dynamic; via malloc/new; manual or GC management |

### 1.4 Activation Record (Stack Frame)

Per-function-call structure on the stack:

```
+-----------------+
| Return value    |
+-----------------+
| Actual params   |
+-----------------+
| Control link    |  → caller's frame (saved FP)
+-----------------+
| Access link     |  → enclosing scope frame (for nested)
+-----------------+
| Saved registers |
+-----------------+
| Local variables |
+-----------------+
| Temporaries     |
+-----------------+
```

### 1.5 Parameter Passing Mechanisms

| Mechanism | Description |
|---|---|
| **Call-by-value** | Copy of value passed; modifications local |
| **Call-by-reference** | Address passed; modifications affect caller |
| **Call-by-value-result (copy-restore)** | Copy in, copy back on return |
| **Call-by-name** | Substitute textual argument (lazy; Algol 60) |
| **Call-by-need** | Lazy + memoized (Haskell) |

### 1.6 Side Effects

Different mechanisms produce different results when arguments alias or modify shared state.

**Example:** `swap(a, a)`:
- Value: no effect.
- Reference: swaps a with itself = no effect.
- Value-result: depends on order.
- Name: textual substitution → no effect.

### 1.7 Heap Management

**Dynamic memory:** allocated/deallocated at runtime.

| Issue | Description |
|---|---|
| **Fragmentation** | Internal (wasted within blocks) and external (between blocks) |
| **Allocators** | First-fit, best-fit, worst-fit |
| **Garbage Collection** | Reference counting, mark-sweep, copying, generational |

### 1.8 Symbol Table at Runtime

In static-scope languages (C), symbol info compiled in. In dynamic-scope, may need runtime lookup.

### 1.9 Code Generation

Translate IR → target machine code.

**Issues:**
- Instruction selection.
- Register allocation.
- Instruction ordering.
- Addressing modes.

### 1.10 Code Generator Input

- Intermediate representation (3AC, AST).
- Symbol table.
- Target machine description.

### 1.11 Issues in Code Generation

| Issue | Description |
|---|---|
| **Instruction selection** | Which target instruction implements which IR? |
| **Register allocation** | Which values held in registers, which in memory? |
| **Spilling** | Move register values to memory when out of registers |
| **Ordering** | Evaluation sequence affects register pressure |

### 1.12 Basic Block

Maximal sequence of consecutive instructions with **single entry, single exit**.

**Properties:**
- No jumps in middle.
- Last instruction may be jump or return.

### 1.13 Control Flow Graph (CFG)

Nodes = basic blocks; edges = transfers of control.

**Used for:** dataflow analysis, optimization, register allocation.

### 1.14 Register Allocation

**Goal:** assign virtual registers to physical registers, minimizing memory traffic.

**Approaches:**
- **Linear scan:** for JIT (fast, simple).
- **Graph coloring:** model interference; k-color the graph.

**Interference graph:** vertex per virtual register; edge if two virtuals are simultaneously live.

**Register allocation = graph coloring with k colors** (k = # physical registers).

### 1.15 Spill

When > k registers needed simultaneously, **spill** some values to memory; reload later.

### 1.16 Peephole Optimization

Local optimizations on small "windows" of generated code.

**Examples:**
- Remove redundant loads/stores.
- Strength reduction (replace `x*2` with `x << 1`).
- Constant folding.
- Dead code elimination.
- Use of machine idioms.

### 1.17 DAG for Basic Block

Build DAG representing computations in a basic block.

**Properties:**
- Common subexpressions share nodes.
- Useful for **local optimization** within block.
- Each leaf = identifier or constant.

### 1.18 Address Calculation

For arrays, structures, pointers: address arithmetic must be efficient.

**Array A[i][j]:** address = base + (i · cols + j) · elem_size.

### 1.19 Function Call Sequence (typical)

**Caller:**
1. Push parameters.
2. Save caller-save registers.
3. Call (push return address).

**Callee:**
1. Save callee-save registers.
2. Set up frame pointer.
3. Allocate locals.

**Return:**
1. Restore registers.
2. Pop frame.
3. Return value in register.

### 1.20 Stack vs Register Machine

**Stack machine** (JVM bytecode): operands implicit; simple but slow.
**Register machine** (x86, ARM): explicit operands; faster.

Real CPUs are register machines; bytecode often stack-based for portability.

> **Summary:** Runtime = memory layout + activation records + param passing. Code generation = IR → machine code, with register allocation (graph coloring), spilling, peephole opt, basic block analysis.

---

## 2. Important Points

- **Stack frame** = activation record; per function call.
- **Static / stack / heap** memory.
- **Call-by-value** is common in C; **call-by-reference** via pointers.
- **Call-by-need** = lazy + memoized.
- **Heap fragmentation** (internal + external) addressed by GC / allocators.
- **Garbage collection** approaches: mark-sweep, copying, generational, reference counting.
- **Basic block:** single entry/exit.
- **CFG** built from basic blocks.
- **Register allocation** = graph coloring (NP-hard); heuristics used.
- **Spilling** when too many live values.
- **Peephole optimization** local; small window.
- **DAG of basic block** identifies common subexpressions.

---

## 3. Short Notes

```
MEMORY LAYOUT
 stack ↓ | heap ↑ | BSS / data | text

STORAGE
 static: compile-time
 stack: LIFO (activation records)
 heap: dynamic

ACTIVATION RECORD
 return val | params | control link |
 access link | saved regs | locals | temps

PARAM PASSING
 value, reference, value-result,
 name (textual), need (lazy + memo)

HEAP MGMT
 fragmentation: internal / external
 allocators: first-fit, best-fit, worst-fit
 GC: reference counting / mark-sweep / copying / generational

CODE GENERATION
 input: IR + symbol table + machine
 issues: instruction selection, register alloc, ordering

BASIC BLOCK
 single entry/exit
 no jumps in middle
 last instr may be jump

CFG = blocks + control edges

REGISTER ALLOCATION
 linear scan / graph coloring
 interference graph
 spilling when out of registers

PEEPHOLE OPTIMIZATION
 local on small windows
 strength reduction, constant fold,
 dead code elim, redundant load/store

DAG for basic block
 common subexpressions shared

FUNCTION CALL
 caller: push params, save regs, call
 callee: save regs, set FP, allocate locals
 return: restore regs, pop frame

STACK MACHINE vs REGISTER MACHINE
 stack: JVM bytecode
 register: x86, ARM
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Memory layout: stack/heap/BSS/text | ✅✅ |
| 2 | Activation record contents | ✅✅ |
| 3 | Storage: static / stack / heap | ✅✅ |
| 4 | 5 parameter passing mechanisms | ✅✅ |
| 5 | Basic block: single entry/exit | ✅✅ |
| 6 | Register alloc = graph coloring (NP-hard) | ✅✅ |
| 7 | Heap fragmentation: internal/external | ✅ |
| 8 | GC approaches | ✅ |
| 9 | Peephole = local optimization | ✅ |
| 10 | DAG for common subexpression | ✅ |

### Tricks

- **Quick parameter-passing test:** trace `swap(a, a)` to see effect.
- **For garbage collection:** reference counting fails on cycles; mark-sweep handles them.
- **Register allocation graph coloring:** k physical registers → k-color the interference graph.
- **Identify basic blocks:** start at leader (target of jump or first instr); end at branch.
- **Peephole patterns:** `x = x + 0` → eliminate; `x * 2` → `x << 1`.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Activation record stores:
**Solution.** Return value, params, control link, locals, temps.

### Q2. (GATE CSE 2014)
Call-by-reference:
**Solution.** Address passed; caller's variable modifiable.

### Q3. (GATE CSE 2018)
Heap allocation:
**Solution.** Dynamic; via malloc/new.

### Q4. (GATE CSE 2008)
Basic block definition:
**Solution.** Single entry/exit; no jumps in middle.

### Q5. (GATE CSE 2010)
Register allocation modeled as:
**Solution.** Graph coloring.

### Q6. (GATE CSE 2015)
Peephole optimization:
**Solution.** Local; small window of code.

### Q7. (GATE CSE 2013)
GC approach handling cycles:
**Solution.** Mark-sweep (or copying); reference counting fails.

### Q8. (GATE CSE 2007)
Static vs stack vs heap allocation:
**Solution.** Compile-time / activation records / dynamic.

### Q9. (GATE CSE 2003)
Call-by-name:
**Solution.** Textual substitution; lazy.

### Q10. (GATE CSE 2009)
DAG of basic block exposes:
**Solution.** Common subexpressions.

### Q11. (GATE CSE 2019)
Linear scan register allocation:
**Solution.** Single pass; for JIT use.

### Q12. (GATE CSE 2020)
Internal vs external fragmentation:
**Solution.** Internal: wasted within block; external: between blocks.

### Q13. (GATE CSE 2021)
Spilling occurs when:
**Solution.** Out of physical registers; move value to memory.

### Q14. (GATE CSE 2016)
JVM bytecode is:
**Solution.** Stack-based.

### Q15. (GATE CSE 2011)
Strength reduction:
**Solution.** Replace expensive op with cheaper (e.g., x*2 → x << 1).

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define activation record.

**P2.** Memory layout components?

**P3.** Static vs stack vs heap.

**P4.** Define basic block.

**P5.** Garbage collection methods?

**P6.** Call-by-value vs call-by-reference.

**P7.** Peephole optimization?

**P8.** Register allocation problem class?

**P9.** Internal fragmentation?

**P10.** External fragmentation?

### Medium

**P11.** Show stack frame layout.

**P12.** Compare call-by-value and call-by-need.

**P13.** Find basic blocks in code.

**P14.** Build CFG from basic blocks.

**P15.** Identify common subexpressions via DAG.

**P16.** Apply peephole: `x = x + 0`.

**P17.** Strength reduction: replace `x * 8` with shift.

**P18.** Heap allocator: first-fit example.

**P19.** Mark-sweep GC steps.

**P20.** Compute register pressure for given live ranges.

### Hard

**P21.** Implement graph coloring register allocation.

**P22.** Compare 4 parameter passing on `swap(a, a)`.

**P23.** Analyze fragmentation after sequence of allocations.

**P24.** Build interference graph from live ranges.

**P25.** Peephole optimization rules in detail.

**P26.** Compare reference counting vs mark-sweep.

**P27.** Stack vs register machine code comparison.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | per-call structure with locals/params/return | direct |
| P2 | stack/heap/BSS/text | direct |
| P3 | as in 1.3 | direct |
| P4 | single entry/exit | direct |
| P5 | mark-sweep, copying, reference counting, generational | direct |
| P6 | as in 1.5 | direct |
| P7 | local optimization | direct |
| P8 | NP-hard (graph coloring) | direct |
| P9 | wasted within block | direct |
| P10 | gaps between blocks | direct |
| P11 | trace layout | direct |
| P12 | eager vs lazy + memoized | direct |
| P13 | leaders mark blocks | direct |
| P14 | nodes blocks, edges control | direct |
| P15 | DAG nodes shared | direct |
| P16 | eliminate | direct |
| P17 | x << 3 | direct |
| P18 | trace allocation | direct |
| P19 | mark + sweep | direct |
| P20 | count concurrent live | direct |
| P21 | iterative coloring | direct |
| P22 | trace 4 mechanisms | direct |
| P23 | trace heap state | direct |
| P24 | edges between live-overlapping | direct |
| P25 | enumerate patterns | direct |
| P26 | cycle handling difference | direct |
| P27 | implicit vs explicit operands | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confuse internal and external fragmentation | Within vs between blocks. |
| 2 | Reference counting handles cycles | It doesn't. |
| 3 | Treat all params as call-by-value | C: yes; many languages: no. |
| 4 | Basic block can have internal jumps | No: single entry/exit. |
| 5 | Register allocation polynomial | NP-hard in general. |
| 6 | Stack frame == heap allocation | Stack uses LIFO discipline. |
| 7 | Garbage collection is free | Has overhead. |
| 8 | Peephole = global optimization | It's local. |
| 9 | DAG is unique | Multiple DAGs possible per block (depending on order). |
| 10 | Call-by-name efficient | Generally slow due to repeated evaluation. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Stack frame contents" | Activation record fields. |
| "Parameter passing" | List 5 mechanisms; effects. |
| "Heap allocation" | Dynamic; allocator + GC. |
| "Register allocation" | Graph coloring. |
| "Basic block" | Single entry/exit. |
| "DAG of block" | Common subexpression. |
| "Peephole optimization" | Local code patterns. |
| "Garbage collection" | Approach trade-offs. |
| "Fragmentation" | Internal vs external. |
| "Call-by-name" | Textual; lazy. |

---

## 9. Quick Revision

```
MEMORY: stack ↓ | heap ↑ | BSS | text

STORAGE: static / stack / heap

ACTIVATION RECORD
 return val | params | control link |
 access link | saved regs | locals | temps

PARAM PASSING
 value, reference, value-result, name, need

HEAP MGMT
 fragmentation: internal / external
 allocators: first/best/worst-fit
 GC: ref count / mark-sweep / copying / generational

CODE GEN ISSUES
 instruction selection
 register allocation (graph coloring, spill)
 ordering

BASIC BLOCK: single entry/exit
CFG: blocks + control edges

REGISTER ALLOC
 interference graph
 k-color = k registers
 spill when not k-colorable

PEEPHOLE OPTIMIZATION
 strength reduction, constant fold,
 dead code, redundant load/store

DAG: common subexpression in basic block

FUNCTION CALL
 caller: push, save, call
 callee: save, FP, locals
 return: restore, pop, return val
```
