# 🧩 Problem-Solving Frameworks — GATE CS

> When you stare at a question and don't know where to start, run a framework. Not improvisation.

---

## Framework 0 — The Universal 30-Second Triage

```
1. What subject? What topic? (5 sec)
2. What is being asked? (NAT/MCQ/MSQ?) (5 sec)
3. Any unit/range trap? (e.g., bytes vs bits, base-2 vs base-10)
4. Which formula/algorithm template applies?
5. If no template fires in 30 sec → MARK and skip.
```

If you can't classify in 30 sec, the question is more expensive than its marks justify on first pass.

---

## Framework — Discrete Math / Counting

1. Identify: *with* or *without* repetition? *Ordered* (permutation) or *unordered* (combination)?
2. Apply Inclusion–Exclusion *only* when sets overlap.
3. For graphs: degree sum = 2|E|. Always check this first on graph counting.
4. Pigeonhole when "must be at least one" appears.

## Framework — Linear Algebra

- Rank questions → row-reduce, count non-zero rows.
- Eigenvalue questions → trace(A) = Σλ, det(A) = Πλ — use these *before* expanding |A − λI|.
- System of equations → check rank(A) vs rank(A|b).

## Framework — Probability

- Define the sample space *explicitly*. 80% of mistakes happen here.
- "Given that…" → conditional → Bayes.
- Discrete: enumerate. Continuous: integrate.

## Framework — Digital Logic

- Combinational: build truth table → K-map → minimize.
- Sequential: state table → state diagram → flip-flop equations.
- For mux/decoder problems, label inputs explicitly. Don't trust intuition.

## Framework — COA

- Cache: hit ratio = hits / accesses. Always check word vs block size.
- Pipeline: Σ stalls / instr; speedup = (n×T) / (n + k − 1)×T_stage.
- Addressing modes: trace effective address step by step. Watch indexed-vs-indirect.

## Framework — DS & Algorithms

1. **Recognize the structure**: array? tree? graph?
2. **Recognize the goal**: search? optimize? count?
3. **Match the template**:
   - Optimize over choices → DP / Greedy
   - Shortest path → BFS / Dijkstra / Bellman-Ford / Floyd
   - MST → Kruskal / Prim
   - Cycle detect → DFS color / Union-Find
4. **Recurrence?** → Master theorem first; Akra-Bazzi only if it fails.
5. **Complexity claim?** → tight bound, not loose.

## Framework — TOC

- Language → smallest class that fits (Regular ⊂ CFL ⊂ CSL ⊂ RE).
- Closure question → check the *closure properties table* (memorize).
- Pumping lemma → use to *disprove* membership; never use to prove it.
- Decidability → reduce *from* a known undecidable problem (HALT, A_TM).

## Framework — Compilers

- Parser type: count look-ahead, recursion direction → LL(1) / SLR / LALR / LR(1) / CLR.
- First/Follow → systematic algorithm. Don't eyeball.
- SDT: synthesized vs inherited — match attributes to grammar position.

## Framework — OS

- Scheduling: Gantt chart, then waiting/turnaround. Always.
- Sync: spot the *invariant*; the bug breaks it.
- Memory: address split → page# + offset; page# → frame#; concat with offset.
- Disk scheduling: draw head movement track-by-track.

## Framework — DBMS

- FD problems: closure of attributes → candidate keys → BCNF/3NF check.
- SQL: write relational algebra first if the SQL feels off.
- Concurrency: build the precedence graph → cycle = not serializable.

## Framework — Computer Networks

- Subnetting: convert prefix → mask → block size; never count IPs by hand.
- Sliding window: throughput = W × MSS / RTT; check window vs sequence-space size.
- TCP CC: cwnd evolution by phase (SS / CA / FR/FR).
- Find the layer first, then the protocol — half the questions are layer-classification.

---

## Question-Reading Protocol

Read every question **twice** before solving.
- First read: classify (framework above).
- Second read: extract numbers + units onto rough sheet.
- Then solve.

This costs 15 sec and saves 90 sec from misreads.

---

## When You're Stuck (90-second rule)

1. 0–30 sec: try the obvious template.
2. 30–60 sec: change representation (truth table, diagram, table).
3. 60–90 sec: plug in small examples, look for pattern.
4. > 90 sec on a 1-mark / > 3 min on a 2-mark → **mark and move**.
