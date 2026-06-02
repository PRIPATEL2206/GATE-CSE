# Graph Algorithms (BFS, DFS, MST, Shortest Paths)

> Subject: Algorithms
> GATE weight: **3–6 marks** every year. Shortest paths, MST algorithms with complexities, network flow basics.

---

## 1. Concept Explanation

### 1.1 BFS / DFS Recap (cross-link)

See [graphs.md](../../04_programming_data_structures/graphs.md) for representation, BFS (queue), DFS (stack/recursion), edge classification, SCC.

This file focuses on **shortest paths, MST algorithms, and applications**.

### 1.2 Shortest Path Problems

| Problem | Description |
|---|---|
| **Single-Source (SSSP)** | Shortest path from one source to all vertices |
| **Single-Destination** | All vertices to one destination (reverse of SSSP) |
| **Single-Pair** | Specific u → v |
| **All-Pairs (APSP)** | Every pair |

### 1.3 BFS Shortest Path (Unweighted)

For unweighted graph, BFS from source gives shortest path (in # edges).

**Time:** O(V + E).

### 1.4 Dijkstra's Algorithm

**SSSP** for graphs with **non-negative** edge weights.

```
dist[s] = 0; dist[other] = ∞
Min-priority queue Q with (dist, vertex)
while Q not empty:
  u = extract-min(Q)
  for each edge (u, v, w):
    if dist[u] + w < dist[v]:
      dist[v] = dist[u] + w
      decrease-key in Q
```

| Implementation | Time |
|---|---|
| Adjacency matrix + array | O(V²) |
| Adjacency list + binary heap | O((V + E) log V) |
| + Fibonacci heap | O(V log V + E) |

**Greedy property:** once a vertex is extracted, its dist is final.

**Fails on negative weights.**

### 1.5 Bellman-Ford Algorithm

**SSSP** allowing **negative weights** (no negative cycle).

```
dist[s] = 0; dist[other] = ∞
for i in 1..V-1:
  for each edge (u, v, w):
    if dist[u] + w < dist[v]:
      dist[v] = dist[u] + w
```

After V−1 iterations, all distances finalized.
**Negative cycle detection:** an extra relaxation succeeds.

**Time:** O(V · E).

### 1.6 SPFA (Shortest Path Faster Algorithm)

Optimization of Bellman-Ford using queue. Worst-case still O(VE) but often faster in practice.

### 1.7 Floyd-Warshall (APSP)

Dynamic programming on intermediate vertices.

```
for k in 1..V:
  for i in 1..V:
    for j in 1..V:
      if dp[i][k] + dp[k][j] < dp[i][j]:
        dp[i][j] = dp[i][k] + dp[k][j]
```

**Time:** O(V³). **Space:** O(V²).

Handles negative weights (no negative cycles); detects negative cycles via diagonal.

### 1.8 Johnson's Algorithm (APSP)

For sparse graphs:
1. Add new vertex 0 with 0-weight edges to all.
2. Run Bellman-Ford from 0 → potentials h[v].
3. Reweight edges: w'(u, v) = w(u, v) + h[u] − h[v] (non-negative).
4. Run Dijkstra from each vertex.

**Time:** O(V² log V + V·E).

### 1.9 Minimum Spanning Tree (MST)

Tree spanning all vertices with minimum total edge weight.

| Algorithm | Idea | Time |
|---|---|---|
| **Kruskal** | Sort edges; add if no cycle | O(E log E) |
| **Prim** | Grow tree from start vertex | O(E log V) heap |
| **Borůvka** | Each component picks lightest edge | O(E log V) |

### 1.10 Kruskal (recap)

```
Sort edges by weight.
Union-Find on vertices.
For each edge (u, v):
  If u and v different components:
    Add to MST; union(u, v).
Stop after V−1 edges.
```

### 1.11 Prim (recap)

```
Start at any vertex; mark visited.
Min-heap of edges from visited.
While not all visited:
  Extract min edge (u, v) where v not visited.
  Add (u, v) to MST; mark v.
  Add v's edges to heap.
```

### 1.12 Maximum Flow (overview)

Flow network: directed graph with source s, sink t, capacity c(u,v) per edge.

**Max-Flow Min-Cut Theorem:** max flow value = min cut capacity.

**Algorithms:**
- **Ford-Fulkerson** (generic): O(E · max_flow).
- **Edmonds-Karp** (BFS-based augmenting paths): O(V · E²).
- **Dinic's algorithm:** O(V² · E).

### 1.13 Topological Sort (recap)

DAG → linear ordering. Two algorithms:

**DFS-based:** finish times in reverse.
**Kahn's:** repeatedly remove zero-indegree nodes. O(V + E).

### 1.14 Strongly Connected Components (recap)

| Algorithm | Approach | Time |
|---|---|---|
| **Kosaraju** | 2 DFS passes | O(V + E) |
| **Tarjan** | 1 DFS with low-link | O(V + E) |

### 1.15 Articulation Points & Bridges

DFS-based with **discovery time** and **low value**:
- u is articulation if some child v has low[v] ≥ disc[u].
- (u, v) is bridge if low[v] > disc[u].

**Time:** O(V + E).

### 1.16 Eulerian Path / Circuit (algorithm)

**Hierholzer's Algorithm:** O(E).
- Start at a vertex with odd degree (or any if Eulerian circuit).
- Follow edges, marking used.
- When stuck, splice in subtour.

### 1.17 Hamiltonian Path / Cycle

NP-hard. Brute force O(n!); DP bitmask O(2ⁿ n²).

### 1.18 A* Algorithm (overview)

Heuristic-based shortest path:
`f(n) = g(n) + h(n)` where g = cost so far, h = heuristic estimate to goal.

Optimal if h is admissible (never overestimates).

### 1.19 Comparison Table

| Algorithm | Use | Time |
|---|---|---|
| BFS | Unweighted SSSP | O(V + E) |
| Dijkstra | Non-negative SSSP | O((V+E) log V) |
| Bellman-Ford | Negative weights SSSP | O(VE) |
| Floyd-Warshall | APSP | O(V³) |
| Johnson | APSP sparse | O(V² log V + VE) |
| Kruskal | MST | O(E log E) |
| Prim | MST | O(E log V) |
| Edmonds-Karp | Max flow | O(VE²) |
| Tarjan/Kosaraju | SCC | O(V + E) |
| Hierholzer | Eulerian | O(E) |
| Topological sort | DAG order | O(V + E) |

### 1.20 Algorithm Selection Guidelines

| Problem | Algorithm |
|---|---|
| Unweighted shortest path | BFS |
| Single-source non-negative | Dijkstra |
| Single-source any weights | Bellman-Ford |
| All-pairs dense | Floyd-Warshall |
| All-pairs sparse + non-negative | Johnson |
| MST sparse | Kruskal |
| MST dense | Prim with matrix |
| DAG | Topological sort + DP |
| Cycle detection directed | DFS back edge |
| Negative cycle | Bellman-Ford or Floyd-Warshall |

> **Summary:** Memorize complexity table cold. Master Dijkstra (greedy with PQ), Bellman-Ford (V−1 relaxations), Floyd-Warshall (3 nested loops). MST: Kruskal (sort + DSU) vs Prim (heap).

---

## 2. Important Points

- **BFS** = unweighted shortest path; O(V + E).
- **Dijkstra fails on negative weights** — use Bellman-Ford.
- **Bellman-Ford** handles negative; detects negative cycles.
- **Floyd-Warshall** = O(V³); negative cycles detected via diagonal.
- **Johnson** = O(V² log V + VE) for sparse APSP.
- **MST** unique iff edge weights distinct.
- **Cut property:** lightest edge across cut is in some MST.
- **Cycle property:** heaviest edge in any cycle is not in any MST.
- **Max flow = min cut** (LP duality).
- **Topological sort** only works on DAG.
- **SCC algorithms** all run in O(V + E).
- **DAG longest path** can be done in O(V + E) via topological sort + DP (NP-hard for general graph).
- **A\*** is optimal with admissible heuristic.
- For grids/maps, **Dijkstra/A*** more efficient than Bellman-Ford.
- **Edmonds-Karp** is BFS-based Ford-Fulkerson.

---

## 3. Short Notes

```
SHORTEST PATHS
 BFS: unweighted SSSP, O(V+E)
 Dijkstra: non-negative SSSP
   matrix: O(V²)
   heap: O((V+E) log V)
 Bellman-Ford: any weights, O(VE)
   detect neg cycle (V-th relaxation)
 Floyd-Warshall: APSP, O(V³)
 Johnson: APSP sparse, O(V² log V + VE)

MST
 Kruskal: O(E log E), DSU
 Prim: O(E log V), heap
 Borůvka: O(E log V)
 cut property: lightest edge across cut
 cycle property: heaviest in cycle excluded

MAX FLOW
 max-flow = min-cut
 Ford-Fulkerson: O(E · max_flow)
 Edmonds-Karp: O(V·E²)
 Dinic's: O(V²·E)

OTHER
 topological sort: O(V+E)
 SCC: Kosaraju / Tarjan: O(V+E)
 articulation / bridge: DFS low-link
 Eulerian (Hierholzer): O(E)
 Hamiltonian: NP-hard

ALGORITHM SELECTION
 unweighted SSSP → BFS
 non-neg SSSP → Dijkstra
 any weights SSSP → Bellman-Ford
 dense APSP → Floyd-Warshall
 sparse APSP → Johnson
 MST sparse → Kruskal
 MST dense → Prim with matrix
 cycle directed → DFS back edge
 DAG order → topological sort
```

---

## 4. Formulas / Tricks

| # | Algorithm | Time | Memorize Cold? |
|---|---|---|---|
| 1 | BFS | O(V + E) | ✅✅✅ |
| 2 | Dijkstra (heap) | O((V+E) log V) | ✅✅✅ |
| 3 | Bellman-Ford | O(VE) | ✅✅✅ |
| 4 | Floyd-Warshall | O(V³) | ✅✅✅ |
| 5 | Johnson's | O(V² log V + VE) | ✅ |
| 6 | Kruskal | O(E log E) | ✅✅ |
| 7 | Prim | O(E log V) | ✅✅ |
| 8 | Edmonds-Karp | O(VE²) | ✅ |
| 9 | Topological sort | O(V + E) | ✅✅ |
| 10 | SCC | O(V + E) | ✅✅ |
| 11 | Hierholzer | O(E) | ✅ |
| 12 | A* | O((V+E) log V) | ✅ |

### Tricks

- **Dijkstra** on negative graph: rewrite using Bellman-Ford or Johnson.
- **Floyd-Warshall** for negative cycle: dp[i][i] < 0.
- **Bellman-Ford for negative cycle:** if V-th iteration relaxes, negative cycle exists.
- **MST count:** when ties exist, may have multiple MSTs.
- **Topological sort applicability:** check for cycles first.
- **For grid/maze problems:** BFS for unweighted, Dijkstra otherwise.
- **For shortest path in DAG:** topological sort + DP, O(V+E) — faster than Dijkstra.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Dijkstra's time with binary heap:
**Solution.** O((V+E) log V).

### Q2. (GATE CSE 2014)
Bellman-Ford time:
**Solution.** O(VE).

### Q3. (GATE CSE 2018)
Floyd-Warshall time:
**Solution.** O(V³).

### Q4. (GATE CSE 2008)
MST: number of edges?
**Solution.** V − 1.

### Q5. (GATE CSE 2010)
Kruskal data structure:
**Solution.** Union-Find.

### Q6. (GATE CSE 2015)
Negative cycle detection:
**Solution.** Bellman-Ford (V-th relaxation succeeds) or Floyd-Warshall (diagonal < 0).

### Q7. (GATE CSE 2013)
Topological sort applies only to:
**Solution.** DAG.

### Q8. (GATE CSE 2007)
SCC algorithms:
**Solution.** Kosaraju, Tarjan, both O(V+E).

### Q9. (GATE CSE 2003)
Max flow Edmonds-Karp:
**Solution.** O(VE²).

### Q10. (GATE CSE 2009)
Prim's complexity with binary heap:
**Solution.** O(E log V).

### Q11. (GATE CSE 2019)
Dijkstra fails on:
**Solution.** Negative edge weights.

### Q12. (GATE CSE 2020)
Eulerian circuit exists if:
**Solution.** Connected + every vertex even degree.

### Q13. (GATE CSE 2021)
Articulation point detection:
**Solution.** DFS with low-link, O(V+E).

### Q14. (GATE CSE 2016)
Number of edges in MST of K₅:
**Solution.** 4.

### Q15. (GATE CSE 2011)
Shortest path on DAG:
**Solution.** Topological sort + DP, O(V+E).

---

## 6. Practice Questions (20+)

### Easy

**P1.** BFS time complexity?

**P2.** Dijkstra fails on what?

**P3.** Floyd-Warshall time?

**P4.** Bellman-Ford time?

**P5.** Edmonds-Karp time?

**P6.** Number of edges in MST of n-vertex graph?

**P7.** Cut property of MST?

**P8.** Cycle property of MST?

**P9.** SCC time?

**P10.** Topological sort time?

### Medium

**P11.** Run Dijkstra on graph: 1→2 (weight 1), 1→3 (4), 2→3 (2), 2→4 (5), 3→4 (1). From source 1.

**P12.** Run Bellman-Ford on graph with negative edge.

**P13.** Run Floyd-Warshall on 4-vertex graph.

**P14.** Find MST using Kruskal: edges {(1,2,1),(2,3,2),(1,3,4),(3,4,3)}.

**P15.** Find MST using Prim from same graph.

**P16.** Detect negative cycle in graph using Bellman-Ford.

**P17.** Topological sort of DAG: 1→2, 1→3, 2→4, 3→4.

**P18.** Run SCC on directed graph.

**P19.** Compute max flow on a small network.

**P20.** Identify articulation points in graph.

### Hard

**P21.** Shortest path in DAG with negative weights.

**P22.** Implement Dijkstra with binary heap.

**P23.** Apply Johnson's algorithm.

**P24.** Find min cost flow.

**P25.** Eulerian circuit using Hierholzer.

**P26.** Compare Dijkstra vs Bellman-Ford on dense graph.

**P27.** Implement A* with Manhattan distance heuristic.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | O(V+E) | direct |
| P2 | negative weights | direct |
| P3 | O(V³) | direct |
| P4 | O(VE) | direct |
| P5 | O(VE²) | direct |
| P6 | n−1 | direct |
| P7 | lightest across cut | direct |
| P8 | heaviest in cycle excluded | direct |
| P9 | O(V+E) | direct |
| P10 | O(V+E) | direct |
| P11 | dist: 1→0, 2→1, 3→3, 4→4 | trace |
| P12 | trace | direct |
| P13 | trace 4×4 | direct |
| P14 | edges (1,2),(2,3),(3,4) | direct |
| P15 | similar | direct |
| P16 | V-th relaxation | direct |
| P17 | 1, 2, 3, 4 or 1, 3, 2, 4 | direct |
| P18 | identify cycles, two DFS | direct |
| P19 | augmenting paths | direct |
| P20 | DFS low-link | direct |
| P21 | topological + DP | direct |
| P22 | priority queue | direct |
| P23 | reweight + Dijkstra | direct |
| P24 | LP / specialized algorithm | direct |
| P25 | follow edges, splice subtours | direct |
| P26 | dense favors Bellman-Ford less | direct |
| P27 | f(n) = g(n) + h(n) | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Dijkstra with negative weights | Use Bellman-Ford. |
| 2 | Topological sort on cyclic graph | Detect cycle first. |
| 3 | Confusing Kruskal and Prim complexity | Kruskal: E log E; Prim: E log V. |
| 4 | Bellman-Ford with V iterations (instead of V−1) | V−1 enough; V-th detects neg cycle. |
| 5 | Floyd-Warshall: 3 loops in wrong order | k must be outer. |
| 6 | Edmonds-Karp time | O(VE²), not O(VE). |
| 7 | MST not unique with ties | Possible multiple MSTs. |
| 8 | Eulerian on directed graph | Different conditions. |
| 9 | Adjacency matrix Dijkstra wrong complexity | O(V²) for matrix. |
| 10 | Treating shortest path tree as MST | They're different. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Unweighted shortest path" | BFS. |
| "Single-source non-negative" | Dijkstra. |
| "Single-source any weights" | Bellman-Ford. |
| "All-pairs" | Floyd-Warshall (dense) / Johnson (sparse). |
| "MST" | Kruskal or Prim. |
| "Max flow" | Ford-Fulkerson / Edmonds-Karp. |
| "Cycle in directed graph" | DFS back edge. |
| "DAG ordering" | Topological sort. |
| "SCC" | Kosaraju or Tarjan. |
| "Articulation / bridge" | DFS low-link. |
| "Negative cycle detection" | Bellman-Ford or Floyd-Warshall. |
| "DAG shortest path" | Topological + DP. |

---

## 9. Quick Revision

```
SHORTEST PATHS
 BFS: O(V+E) (unweighted)
 Dijkstra (heap): O((V+E) log V) (non-neg)
 Bellman-Ford: O(VE) (any weights)
 Floyd-Warshall: O(V³) (APSP)
 Johnson: O(V² log V + VE) (sparse APSP)

MST
 Kruskal: O(E log E) (DSU)
 Prim: O(E log V) (heap)

MAX FLOW
 Ford-Fulkerson: generic
 Edmonds-Karp: O(VE²)
 Dinic's: O(V²E)
 max-flow = min-cut

TOPO SORT (DAG): O(V+E)
SCC: Kosaraju / Tarjan, O(V+E)
ARTICULATION / BRIDGE: DFS low-link, O(V+E)
EULERIAN (Hierholzer): O(E)
HAMILTONIAN: NP-hard

A*: f = g + h (admissible h)

NEG CYCLE DETECTION
 Bellman-Ford V-th relax succeeds
 Floyd-Warshall diagonal < 0

DAG SHORTEST PATH: topo + DP, O(V+E)
```
