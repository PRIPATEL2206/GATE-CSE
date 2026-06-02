# Topic Test 14 — Algorithms (Graph Algorithms · NP-Completeness)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] BFS time complexity:
(A) O(V)  (B) O(E)  (C) O(V+E)  (D) O(V·E)

**Q2.** [MCQ] Dijkstra (binary heap) time:
(A) O(V²)  (B) O((V+E) log V)  (C) O(V·E)  (D) O(V³)

**Q3.** [MCQ] Bellman-Ford time:
(A) O(V+E)  (B) O((V+E) log V)  (C) O(V·E)  (D) O(V³)

**Q4.** [MCQ] Floyd-Warshall time:
(A) O(V²)  (B) O(V·E)  (C) O(V³)  (D) O(V² log V)

**Q5.** [MCQ] Dijkstra fails on:
(A) Cyclic graphs  (B) Negative weights  (C) Disconnected graphs  (D) DAG

**Q6.** [MCQ] Kruskal time:
(A) O(V²)  (B) O(E log V)  (C) O(E + V)  (D) O(V³)

**Q7.** [NAT] # of edges in MST of K₆ = `____`

**Q8.** [MCQ] Edmonds-Karp time:
(A) O(VE)  (B) O(VE²)  (C) O(V²E)  (D) O(E³)

**Q9.** [MCQ] Topological sort applies to:
(A) Any graph  (B) DAG  (C) Cyclic  (D) Bipartite

**Q10.** [MCQ] SCC algorithm time:
(A) O(V+E)  (B) O(V²)  (C) O(V·E)  (D) O(V³)

**Q11.** [MCQ] SAT was proved NP-complete by:
(A) Turing  (B) Cook-Levin  (C) Edmonds  (D) Knuth

**Q12.** [MCQ] 2-SAT is in:
(A) P  (B) NP-complete  (C) NP-hard but not NP  (D) Undecidable

**Q13.** [MCQ] Halting problem is:
(A) In P  (B) NP-complete  (C) Undecidable  (D) co-NP

**Q14.** [MCQ] Approximation ratio for greedy vertex cover:
(A) 1  (B) 2  (C) log n  (D) n

**Q15.** [MCQ] If A ≤_p B and B ∈ P:
(A) A is NP-hard  (B) A ∈ P  (C) Cannot decide  (D) A ∈ NP-complete

---

## Section B — 2 marks each

**Q16.** [MCQ] Shortest path in DAG with possibly negative weights:
(A) Dijkstra  (B) Bellman-Ford  (C) Topological sort + DP  (D) Floyd-Warshall

**Q17.** [MCQ] Negative cycle detection in dense graph:
(A) Dijkstra  (B) BFS  (C) Floyd-Warshall  (D) Kruskal

**Q18.** [NAT] # MSTs in K₄ with all distinct weights = `____`

**Q19.** [MCQ] Reduce 3-SAT to:
(A) 2-SAT  (B) CLIQUE  (C) Bipartite matching  (D) MST

**Q20.** [MCQ] Pseudo-polynomial example:
(A) Sorting  (B) Subset sum DP  (C) BFS  (D) MST

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (C) O(V+E) | direct |
| 2 | (B) | direct |
| 3 | (C) O(V·E) | direct |
| 4 | (C) O(V³) | direct |
| 5 | (B) | direct |
| 6 | (B) O(E log V) | E log E = E log V |
| 7 | 5 | n − 1 |
| 8 | (B) O(VE²) | direct |
| 9 | (B) DAG | direct |
| 10 | (A) O(V+E) | direct |
| 11 | (B) Cook-Levin | direct |
| 12 | (A) P | direct |
| 13 | (C) Undecidable | direct |
| 14 | (B) 2 | direct |
| 15 | (B) | reduction property |
| 16 | (C) Topo + DP | DAG specific, faster |
| 17 | (C) Floyd-Warshall | dense; checks diagonal |
| 18 | 1 | unique with distinct weights |
| 19 | (B) CLIQUE | classical reduction |
| 20 | (B) Subset sum | poly in S |

---

## Score Sheet

| | Score |
|---|---|
| Section A (15 × 1) | _ /15 |
| Section B (5 × 2)  | _ /10 |
| **Total**          | _ /25 |
| Time used          | _ min |

**Targets:**
- ≥ 22/25 in 25 min → mastery
- 18–21 → revise short notes + pattern recognition
- < 18 → re-do PYQs of both topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
