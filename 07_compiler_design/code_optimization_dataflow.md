# Code Optimization & Data-Flow Analysis

> Subject: Compiler Design
> GATE weight: **2–3 marks** every year. Local/global optimization, dataflow equations, common transformations.

---

## 1. Concept Explanation

### 1.1 Code Optimization Goals

Improve generated code by:
- Reducing **execution time**.
- Reducing **memory** usage.
- Reducing **code size**.
- Reducing **power consumption**.

Without changing **semantics** (program meaning).

### 1.2 Optimization Levels

| Level | Description |
|---|---|
| **Local** | Within a basic block |
| **Global** | Across basic blocks (within function) |
| **Interprocedural** | Across functions |
| **Whole-program / link-time** | At link stage |

### 1.3 Common Optimizations

| Optimization | Description |
|---|---|
| **Constant folding** | Evaluate constant expressions at compile time |
| **Constant propagation** | Replace variable with known constant value |
| **Common subexpression elimination (CSE)** | Reuse computed expression |
| **Dead code elimination** | Remove unreachable / unused code |
| **Copy propagation** | Replace `b = a; … = b` with `… = a` |
| **Loop-invariant code motion** | Move invariant out of loop |
| **Strength reduction** | Replace expensive op (e.g., `i*4 → i << 2`) |
| **Induction variable elimination** | Simplify loop counter computations |
| **Code hoisting** | Move common code earlier |
| **Function inlining** | Replace call with body |
| **Tail call optimization** | Reuse call frame for tail calls |
| **Loop unrolling** | Replicate loop body |
| **Loop fusion / fission** | Combine / split loops |
| **Jump threading** | Skip redundant jumps |

### 1.4 Local Optimization

Within a basic block. Uses:
- DAG representation.
- Algebraic identities.
- Constant folding/propagation.

### 1.5 Global Optimization

Across basic blocks. Requires **dataflow analysis**.

### 1.6 Dataflow Analysis

Compute information about how data flows through the CFG.

**Generic framework:** for each block B, compute IN[B] and OUT[B] satisfying:
- **Transfer function:** OUT[B] = f_B(IN[B]).
- **Meet operator:** IN[B] = ⊓ OUT[P] for predecessors P (forward) or ⊓ IN[S] for successors S (backward).

### 1.7 Common Dataflow Problems

| Analysis | Direction | Meet | Use |
|---|---|---|---|
| **Reaching Definitions** | Forward | Union | Constant propagation |
| **Live Variables** | Backward | Union | Register allocation |
| **Available Expressions** | Forward | Intersection | CSE |
| **Very Busy Expressions** | Backward | Intersection | Code hoisting |
| **Constant Propagation** | Forward | Special meet | Constant folding |

### 1.8 Reaching Definitions

A definition `d: x = …` reaches point p if there's a path from d to p with no other definition of x between.

**Equations:**
```
OUT[B] = gen[B] ∪ (IN[B] − kill[B])
IN[B] = ∪ OUT[P] for predecessors P
```

**gen[B]** = definitions in B that reach end of B.
**kill[B]** = definitions killed by B.

### 1.9 Live Variables Analysis

Variable v is **live** at point p if v's value at p may be used along some future path.

**Equations:**
```
IN[B] = use[B] ∪ (OUT[B] − def[B])
OUT[B] = ∪ IN[S] for successors S
```

**Direction:** backward.

### 1.10 Available Expressions

Expression e is **available** at point p if every path from start to p evaluates e and no operand modified after.

**Equations:**
```
OUT[B] = gen[B] ∪ (IN[B] − kill[B])
IN[B] = ∩ OUT[P] for predecessors P  (intersect)
```

Initial OUT[entry] = ∅; OUT[B] = U (universe) for others.

### 1.11 Very Busy Expressions

Expression e is **very busy** at p if e will be evaluated on every path from p before any operand is modified.

**Equations:**
```
IN[B] = use[B] ∪ (OUT[B] − kill[B])
OUT[B] = ∩ IN[S] for successors S
```

### 1.12 Iterative Algorithm

Initialize all IN and OUT.
Repeat:
  for each block B:
    update IN[B], OUT[B] using equations.
Until no change.

**Convergence:** for monotonic transfer functions on finite lattices.

### 1.13 Lattice Properties

Dataflow values form a **lattice**:
- Partial order ⊑.
- Meet ⊓.
- Top ⊤ and bottom ⊥.

Common lattice: powerset under union or intersection.

### 1.14 Loop Optimizations

| Optimization | Description |
|---|---|
| **Loop-invariant code motion** | Move computation outside loop |
| **Strength reduction** | Replace multiplications with additions |
| **Induction variable elimination** | Identify and simplify counters |
| **Loop unrolling** | Reduce branch overhead |
| **Loop fusion** | Merge loops over same range |
| **Loop fission** | Split loop for parallelism |
| **Loop tiling** | Improve cache locality |

### 1.15 Constant Folding & Propagation

**Folding:** `5 + 3` → `8`.
**Propagation:** if `x = 5`, replace later use of `x` with `5`.

### 1.16 Common Subexpression Elimination (CSE)

If same expression computed twice without operand changes, compute once.

**Local CSE** uses DAG of basic block.
**Global CSE** uses Available Expressions analysis.

### 1.17 Dead Code Elimination

Remove code:
- **Unreachable** (no path leads to it).
- **Useless** (results unused).

Uses **live variables** analysis.

### 1.18 Function Inlining

Replace call with function body. Trade-offs:
- + Eliminates call overhead.
- + Enables further optimizations.
- − Increases code size.

### 1.19 Tail Call Optimization

If last action is a function call, reuse the current activation record.

Important for **recursion** in functional languages.

### 1.20 Comparison Table

| Analysis | Direction | Meet | Initialize OUT |
|---|---|---|---|
| Reaching Defs | Forward | ∪ | ∅ everywhere |
| Live Variables | Backward | ∪ | ∅ everywhere |
| Available Expr | Forward | ∩ | universe (except entry: ∅) |
| Very Busy Expr | Backward | ∩ | universe (except exit: ∅) |

### 1.21 Static Single Assignment (SSA)

Form where each variable assigned exactly once.

**φ-functions** at merge points:
```
x3 = φ(x1, x2)
```

SSA simplifies many optimizations (constant propagation, dead code, register alloc).

### 1.22 Common Misconceptions

- **Optimization can change running time** but **not correctness**.
- **Compiler may reorder** operations if semantics preserved.
- Some optimizations interact (one enables another).

> **Summary:** Optimizations split into local (basic block) and global (dataflow). 4 canonical dataflow analyses (reaching defs, live vars, available expr, very busy expr). Loop optimizations + SSA + classic transformations like CSE, CP, DCE.

---

## 2. Important Points

- **Optimization preserves semantics**, improves performance.
- **Local optimization** within a basic block; **global** uses dataflow.
- **4 classic dataflow problems:** reaching defs, live vars, available expr, very busy expr.
- **Forward analyses** flow from start; **backward** from end.
- **Union meet** = "may"; **intersection meet** = "must".
- **Reaching defs:** forward + union.
- **Live vars:** backward + union.
- **Available expr:** forward + intersection.
- **Very busy:** backward + intersection.
- **Iterative algorithm** converges if monotonic + finite lattice.
- **CSE** uses available expressions.
- **DCE** uses live variables.
- **Constant propagation** uses reaching defs.
- **Loop unrolling** reduces branch overhead but enlarges code.
- **SSA** simplifies optimization.
- **Inlining** trades code size for speed.

---

## 3. Short Notes

```
OPTIMIZATION GOALS
 reduce time / memory / code size
 preserve semantics

LEVELS: local / global / interprocedural / whole-program

CLASSIC OPTIMIZATIONS
 constant folding, constant propagation
 CSE, copy propagation
 dead code elimination
 loop-invariant code motion
 strength reduction
 induction variable elimination
 function inlining
 tail call optimization
 loop unrolling, fusion, fission, tiling

LOCAL: within basic block (DAG)
GLOBAL: dataflow analysis

DATAFLOW
 IN[B] = ⊓ OUT[P]/IN[S]
 OUT[B] = f_B(IN[B])

CLASSIC DATAFLOW ANALYSES
 reaching defs: forward, ∪
 live variables: backward, ∪
 available expr: forward, ∩
 very busy expr: backward, ∩

REACHING DEFS
 OUT[B] = gen[B] ∪ (IN[B] − kill[B])
 IN[B] = ∪ OUT[P]

LIVE VARS
 IN[B] = use[B] ∪ (OUT[B] − def[B])
 OUT[B] = ∪ IN[S]

AVAILABLE EXPR
 OUT[B] = gen[B] ∪ (IN[B] − kill[B])
 IN[B] = ∩ OUT[P]

VERY BUSY
 IN[B] = use[B] ∪ (OUT[B] − kill[B])
 OUT[B] = ∩ IN[S]

ITERATIVE ALGORITHM
 init, repeat update, until stable

LATTICE: partial order, meet, top/bottom

LOOP OPTIMIZATIONS
 invariant motion, strength reduction,
 induction var elim, unrolling,
 fusion / fission / tiling

SSA: each var assigned once; φ at merges
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Optimization preserves semantics | ✅ |
| 2 | Local = within block; global = dataflow | ✅✅ |
| 3 | 4 dataflow direction/meet table | ✅✅✅ |
| 4 | Reaching defs equations | ✅ |
| 5 | Live variables equations | ✅ |
| 6 | Available expressions equations | ✅ |
| 7 | CSE uses available expressions | ✅ |
| 8 | DCE uses live variables | ✅ |
| 9 | Loop-invariant motion | ✅ |
| 10 | Strength reduction (e.g., ×4 → <<2) | ✅ |
| 11 | Inlining trade-off | ✅ |
| 12 | SSA: single assignment + φ | ✅ |

### Tricks

- **Pick analysis by goal:** CSE → available expr; DCE → live vars; const prop → reaching defs.
- **Forward + Union = "may":** at least one path supports.
- **Forward + Intersection = "must":** all paths support.
- **Convergence:** iterations bounded by lattice height.
- **Loop optimizations:** identify invariants outside loop body.
- **For SSA conversion:** φ-functions at merge points.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Reaching definitions analysis direction:
**Solution.** Forward.

### Q2. (GATE CSE 2014)
Live variables analysis direction:
**Solution.** Backward.

### Q3. (GATE CSE 2018)
Available expressions analysis meet:
**Solution.** Intersection.

### Q4. (GATE CSE 2008)
CSE uses which analysis?
**Solution.** Available expressions.

### Q5. (GATE CSE 2010)
DCE uses which analysis?
**Solution.** Live variables.

### Q6. (GATE CSE 2015)
Strength reduction example:
**Solution.** Replace `i*4` with `i << 2`.

### Q7. (GATE CSE 2013)
Loop-invariant code motion:
**Solution.** Move invariant computation out of loop.

### Q8. (GATE CSE 2007)
Function inlining trade-off:
**Solution.** Code size vs call overhead.

### Q9. (GATE CSE 2003)
Constant folding:
**Solution.** Compute constants at compile time.

### Q10. (GATE CSE 2009)
SSA φ-function purpose:
**Solution.** Merge values at control-flow joins.

### Q11. (GATE CSE 2019)
Dead code elimination removes:
**Solution.** Unreachable + useless code.

### Q12. (GATE CSE 2020)
Loop unrolling effect:
**Solution.** Reduces branch overhead, enlarges code.

### Q13. (GATE CSE 2021)
Forward-intersection analysis:
**Solution.** Available expressions.

### Q14. (GATE CSE 2016)
Very busy expressions direction:
**Solution.** Backward.

### Q15. (GATE CSE 2011)
Iterative dataflow convergence:
**Solution.** Monotonic transfer + finite lattice.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define optimization.

**P2.** Local vs global optimization?

**P3.** Reaching defs direction?

**P4.** Live vars direction?

**P5.** Available expr meet?

**P6.** DCE uses what?

**P7.** Strength reduction example.

**P8.** Loop-invariant code motion.

**P9.** Constant folding.

**P10.** Inlining trade-off.

### Medium

**P11.** Compute reaching defs for small CFG.

**P12.** Compute live variables for small CFG.

**P13.** Apply CSE to expression block.

**P14.** Identify dead code.

**P15.** Apply strength reduction in loop.

**P16.** Convert simple code to SSA.

**P17.** Identify loop invariants in nested loop.

**P18.** Apply constant propagation across blocks.

**P19.** Detect tail call.

**P20.** Compute very busy expressions.

### Hard

**P21.** Implement iterative reaching defs algorithm.

**P22.** Show convergence of dataflow analysis.

**P23.** Compare available expr and very busy expr.

**P24.** Apply loop unrolling with factor 4.

**P25.** Construct SSA with φ-functions.

**P26.** Detect induction variables.

**P27.** Trade-offs of inlining heuristics.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | improve performance preserving semantics | direct |
| P2 | within block vs across blocks | direct |
| P3 | forward | direct |
| P4 | backward | direct |
| P5 | ∩ intersection | direct |
| P6 | live variables | direct |
| P7 | x*2 → x << 1 | direct |
| P8 | move out of loop | direct |
| P9 | evaluate constants | direct |
| P10 | code size vs speed | direct |
| P11 | trace iteration | direct |
| P12 | trace iteration | direct |
| P13 | DAG-based reuse | direct |
| P14 | use live vars | direct |
| P15 | replace expensive ops | direct |
| P16 | rename + φ at merges | direct |
| P17 | values fixed across iterations | direct |
| P18 | propagate known values | direct |
| P19 | last action is call | direct |
| P20 | trace backward intersection | direct |
| P21 | iterative algorithm | direct |
| P22 | monotonic + finite lattice | direct |
| P23 | direction differ | direct |
| P24 | replicate body | direct |
| P25 | rename + φ | direct |
| P26 | linear in counter | direct |
| P27 | size vs speed | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Optimization changes semantics | It must preserve them. |
| 2 | Confuse forward/backward analyses | Pick by direction of "future". |
| 3 | Use union for available expr | Should be intersection. |
| 4 | Treat loop-invariant motion as always safe | Side effects matter. |
| 5 | Forget φ-function placement in SSA | At merge points. |
| 6 | DCE removes side-effecting ops | Avoid removing those. |
| 7 | Strength reduction always applies | Some not equivalent (overflow). |
| 8 | Inlining always faster | May enlarge code excessively. |
| 9 | CSE without checking operand changes | Operands must be unchanged. |
| 10 | Confuse reaching defs and available expr | One tracks defs, other expressions. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Reaching definitions" | Forward + ∪. |
| "Live variables" | Backward + ∪. |
| "Available expressions" | Forward + ∩. |
| "Very busy expressions" | Backward + ∩. |
| "CSE optimization" | Available expressions. |
| "Dead code elimination" | Live variables. |
| "Constant propagation" | Reaching defs. |
| "Loop optimization" | Hoist invariants, strength reduction. |
| "SSA form" | Single assignment + φ. |
| "Inlining" | Code size vs speed. |

---

## 9. Quick Revision

```
OPTIMIZATION = improve performance, preserve semantics

LEVELS: local / global / interprocedural / whole-program

CLASSIC
 const fold/prop, CSE, copy prop, DCE
 loop-invariant motion, strength reduction
 induction var elim, inlining, tail-call
 unrolling, fusion, fission, tiling

DATAFLOW (4 classic)
            direction  meet
 reaching def  fwd     ∪
 live vars     bwd     ∪
 avail expr    fwd     ∩
 very busy     bwd     ∩

EQUATIONS
 reaching def: OUT = gen ∪ (IN − kill); IN = ∪ OUT[pred]
 live vars: IN = use ∪ (OUT − def); OUT = ∪ IN[succ]
 avail: OUT = gen ∪ (IN − kill); IN = ∩ OUT[pred]
 very busy: IN = use ∪ (OUT − kill); OUT = ∩ IN[succ]

ITERATIVE ALGO: init + repeat until stable
LATTICE: monotonic + finite ⇒ converges

USES
 CSE → avail expr
 DCE → live vars
 const prop → reaching defs

LOOP OPTIMIZATIONS
 invariant motion, strength red, induction elim,
 unrolling, fusion, fission, tiling

SSA: single assignment + φ at merges

INLINING: size vs speed trade-off
```
