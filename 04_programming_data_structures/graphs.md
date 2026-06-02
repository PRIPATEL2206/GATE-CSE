# Graphs (Representation, Traversal)

> Subject: Programming & Data Structures
> GATE weight: **2–4 marks** every year. Adjacency rep, BFS/DFS, properties (graph theory cross-link → discrete maths).

---

## 1. Concept Explanation

### 1.1 Graph Basics (cross-link)

See [graph_theory.md](../../01_engineering_mathematics/discrete_mathematics/graph_theory.md) for graph theoretical properties (handshake, planarity, chromatic number, etc.). This file focuses on **representation and traversal** — the algorithmic side.

### 1.2 Representations

| Representation | Space | Edge query (u,v) | Iterate neighbours |
|---|---|---|---|
| **Adjacency Matrix** | O(V²) | O(1) | O(V) |
| **Adjacency List** | O(V + E) | O(deg) | O(deg) |
| **Edge List** | O(E) | O(E) | O(E) |
| **Incidence Matrix** | O(V·E) | O(E) | O(E) |

**Adjacency Matrix:** A[i][j] = 1 if (i, j) ∈ E, else 0. Symmetric for undirected.

**Adjacency List:** array (or vector) of lists, one per vertex.

### 1.3 When to Use Which

- **Dense graphs (E ≈ V²):** adjacency matrix.
- **Sparse graphs (E ≪ V²):** adjacency list (most common).
- **Algorithms needing edge weights:** matrix or list-of-pairs.

### 1.4 Properties from Representation

For adjacency matrix A of an unweighted graph:
- (A^k)[i][j] = # of walks of length k from i to j.
- A² gives # paths of length 2.

For adjacency list:
- Computing degree: list size for that vertex.

### 1.5 BFS (Breadth-First Search)

Traverses level by level using a **queue**.

```
mark all unvisited
BFS(s):
  enqueue s; mark visited
  while queue not empty:
    u = dequeue()
    for each neighbour v:
      if not visited:
        mark; enqueue
```

**Time:** O(V + E) using adjacency list.
**Space:** O(V) for queue + visited.

**Properties:**
- Visits vertices in non-decreasing order of distance from source.
- Computes **shortest path** in unweighted graph.

### 1.6 DFS (Depth-First Search)

Traverses depth-first using a **stack** (recursion).

```
mark all unvisited
DFS(u):
  mark u visited
  for each neighbour v:
    if not visited:
      DFS(v)
```

**Time:** O(V + E).
**Space:** O(V) for recursion / stack + visited.

### 1.7 DFS Properties

- Discovers **strongly connected components** (Tarjan, Kosaraju).
- Topological sort (DAG).
- Cycle detection.
- Bridge / articulation point detection.

### 1.8 Edge Classification (DFS)

For directed graphs, DFS edges classified as:
- **Tree edge:** new node discovered.
- **Back edge:** to ancestor (indicates cycle).
- **Forward edge:** to descendant via non-tree.
- **Cross edge:** to neither ancestor nor descendant.

For undirected: only tree and back edges.

### 1.9 Connected Components

For undirected graph: # components = # of DFS/BFS runs to visit all vertices.

### 1.10 Strongly Connected Components (SCC)

For directed graph: max set where every pair is mutually reachable.

**Algorithms:**
- **Kosaraju:** 2 DFS passes (original, then reverse graph).
- **Tarjan:** single DFS with low-link values.

Both O(V + E).

### 1.11 Topological Sort (DAG)

Linear ordering of vertices such that every edge u→v has u before v.

**Algorithms:**
- **DFS-based:** finish times in reverse.
- **Kahn's:** repeatedly remove zero-indegree vertices.

O(V + E).

### 1.12 Cycle Detection

**Undirected:** DFS — if revisits non-parent vertex, cycle exists.
**Directed:** DFS — back edge indicates cycle. Or topological sort fails.

### 1.13 Shortest Path (preview)

Covered in [graph_algorithms.md](../../05_algorithms/graph_algorithms.md):
- **BFS:** unweighted shortest path.
- **Dijkstra:** non-negative weights.
- **Bellman-Ford:** negative weights, no negative cycle.
- **Floyd-Warshall:** all pairs, O(V³).

### 1.14 Minimum Spanning Tree (preview)

Also in graph_algorithms:
- **Kruskal:** sort edges, union-find. O(E log E).
- **Prim:** priority queue. O(E log V).

### 1.15 Counting from Adjacency Matrix

- Row sum = out-degree.
- Column sum = in-degree.
- For undirected: row sum = degree.
- A^k[i][j] counts walks of length k.
- For symmetric A: A is diagonalizable; eigenvalues encode graph properties.

### 1.16 Bipartite Detection

Graph is bipartite ⇔ 2-colorable ⇔ no odd cycle.

**BFS/DFS check:** color alternately; if conflict, not bipartite.

### 1.17 Special Algorithms

- **Articulation Point** (cut vertex): removal disconnects graph.
- **Bridge:** edge whose removal disconnects.
- **Eulerian Circuit:** uses every edge once; connected + all even degree.
- **Hamiltonian Cycle:** uses every vertex once; NP-hard.

### 1.18 Graph Representation Trade-offs

For algorithm running time:
- BFS/DFS: O(V + E) with adjacency list; O(V²) with matrix.
- Edge-weight queries: matrix faster.
- Sparse graphs: list saves space significantly.

> **Summary:** Master adjacency matrix vs list trade-offs, BFS/DFS algorithms (O(V + E)), edge classifications, SCC algorithms, topological sort, cycle detection. The big O depends on representation.

---

## 2. Important Points

- Adjacency list space O(V + E) typically beats matrix for sparse graphs.
- BFS gives **shortest path** in **unweighted** graph.
- DFS naturally gives topological sort for DAG (reverse postorder).
- # connected components found by counting DFS calls in main loop.
- **Tree edges** + **back edges** in undirected DFS classify everything.
- **Back edge** indicates cycle.
- Bipartite graph has no odd cycle.
- For directed: SCCs found via Kosaraju or Tarjan in O(V + E).
- **Topological sort** exists iff DAG (no cycle).
- **Eulerian circuit** exists iff every vertex has even degree (undirected, connected).
- A^k counts walks of length k between vertex pairs.
- Articulation point detection: O(V + E) using DFS low-link.
- DFS recursion depth can be up to O(V) — risk of stack overflow on large graphs.
- BFS queue size also up to O(V).

---

## 3. Short Notes

```
REPRESENTATIONS
 matrix: O(V²); edge query O(1)
 list: O(V+E); edge iter O(deg)
 dense → matrix; sparse → list

BFS
 queue-based, visits by level
 O(V+E)
 unweighted shortest path

DFS
 recursion / explicit stack
 O(V+E)
 cycle detection, topological sort, SCC

DFS EDGE CLASSIFICATION (directed)
 tree, back, forward, cross
 undirected: tree, back

CONNECTED COMPONENTS (undirected)
 DFS/BFS from each unvisited

SCC (directed)
 Kosaraju (2 DFS), Tarjan (1 DFS) — O(V+E)

TOPOLOGICAL SORT (DAG)
 DFS finish times reversed
 Kahn's: remove indegree-0 nodes

CYCLE DETECTION
 undirected: DFS non-parent revisit
 directed: back edge

BIPARTITE: 2-color via BFS/DFS

A^k: walks of length k

ARTICULATION POINTS / BRIDGES
 DFS low-link, O(V+E)

EULERIAN: all even degree (undirected)
HAMILTONIAN: NP-hard

(SHORTEST PATH / MST → algorithms file)
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Adjacency list space O(V+E) | ✅✅ |
| 2 | Adjacency matrix space O(V²) | ✅✅ |
| 3 | BFS/DFS time O(V+E) with list | ✅✅ |
| 4 | BFS for unweighted shortest path | ✅✅ |
| 5 | DFS for topological sort, cycle detect, SCC | ✅✅ |
| 6 | A^k counts walks of length k | ✅ |
| 7 | Bipartite ⇔ no odd cycle | ✅✅ |
| 8 | DFS edge types | ✅ |
| 9 | Topological sort works only on DAG | ✅✅ |
| 10 | Eulerian: all even degree (undirected, connected) | ✅ |
| 11 | Hamiltonian: NP-hard | ✅ |
| 12 | SCC algorithms O(V+E) | ✅ |

### Tricks

- **Quick test for bipartite:** 2-coloring BFS; conflict → not bipartite.
- **Topological sort via Kahn:** repeatedly pick zero-indegree.
- **DFS for cycle (undirected):** track parent; if visited and not parent → cycle.
- **For directed cycle:** track current path (gray nodes); revisit gray → cycle.
- **Articulation point shortcut:** DFS low-link; node u is articulation if low[v] ≥ disc[u] for some child v.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Adjacency matrix vs list space — which for dense graph?
**Solution.** Matrix.

### Q2. (GATE CSE 2014)
BFS visits which vertex first?
**Solution.** Source.

### Q3. (GATE CSE 2018)
DFS time complexity with adjacency list:
**Solution.** O(V + E).

### Q4. (GATE CSE 2008)
Topological sort can be done on:
**Solution.** DAG (directed acyclic graph).

### Q5. (GATE CSE 2010)
Detecting cycle in undirected graph:
**Solution.** DFS, check if visited node is non-parent.

### Q6. (GATE CSE 2015)
SCC of digraph in O(V+E):
**Solution.** Kosaraju or Tarjan.

### Q7. (GATE CSE 2013)
BFS gives shortest path in:
**Solution.** Unweighted graph.

### Q8. (GATE CSE 2007)
Adjacency matrix size for graph with 1000 vertices:
**Solution.** 10⁶ entries.

### Q9. (GATE CSE 2003)
Number of connected components of n-vertex graph with no edges:
**Solution.** n.

### Q10. (GATE CSE 2009)
DFS edge classification: which edge confirms cycle in directed graph?
**Solution.** Back edge.

### Q11. (GATE CSE 2019)
Bipartite check using:
**Solution.** BFS/DFS 2-coloring.

### Q12. (GATE CSE 2020)
Number of distinct topological orderings of a DAG with edges A→B, A→C, B→D, C→D:
**Solution.** 2 (ABCD and ACBD).

### Q13. (GATE CSE 2021)
Articulation points found by:
**Solution.** DFS with low-link values.

### Q14. (GATE CSE 2016)
Adjacency matrix M of undirected graph: M = M^T?
**Solution.** Yes (symmetric).

### Q15. (GATE CSE 2011)
Power M^2 of adjacency matrix gives:
**Solution.** Number of walks of length 2.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Adjacency list space?

**P2.** Adjacency matrix space?

**P3.** BFS uses which DS?

**P4.** DFS uses which DS?

**P5.** Time complexity of DFS with list?

**P6.** Cycle detection in undirected graph?

**P7.** Bipartite check approach?

**P8.** Number of distinct topological orderings of A→B?

**P9.** SCC found by which algorithms?

**P10.** Eulerian condition?

### Medium

**P11.** BFS from vertex 1 in graph: 1-2, 1-3, 2-4, 3-4. Order?

**P12.** DFS from vertex 1 (same graph). Order?

**P13.** Topological sort of DAG: A→B, A→C, B→D, C→D, D→E.

**P14.** Find SCCs of graph: 1→2, 2→3, 3→1, 3→4.

**P15.** Articulation points in graph: 1-2, 2-3, 3-4, 4-2.

**P16.** Diameter of unweighted graph: BFS from each vertex.

**P17.** Compute A^2 for adjacency matrix.

**P18.** Detect cycle in directed graph (algorithm).

**P19.** Number of edges in complete graph K₅.

**P20.** Connected components: graph 1-2, 3-4, 5.

### Hard

**P21.** Find bridges in graph using DFS.

**P22.** Detect Eulerian circuit existence.

**P23.** Construct topological order using Kahn's algorithm.

**P24.** Bipartite check on cycle of length 5.

**P25.** Compare BFS vs DFS memory usage.

**P26.** Count walks of length 3 from u to v using adjacency matrix.

**P27.** Find shortest path tree using BFS.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | O(V+E) | direct |
| P2 | O(V²) | direct |
| P3 | queue | direct |
| P4 | stack/recursion | direct |
| P5 | O(V+E) | direct |
| P6 | DFS, non-parent revisit | direct |
| P7 | 2-coloring | direct |
| P8 | 1 | only A→B order |
| P9 | Kosaraju, Tarjan | direct |
| P10 | all even degrees | undirected |
| P11 | 1, 2, 3, 4 | level-order |
| P12 | 1, 2, 4, 3 (depending on order) | direct |
| P13 | A, B, C, D, E or A, C, B, D, E | DAG |
| P14 | {1,2,3}, {4} | direct |
| P15 | 2 | bridge to 1 |
| P16 | run BFS from each, max | direct |
| P17 | matrix multiply | direct |
| P18 | DFS with current path tracking | direct |
| P19 | 10 | 5·4/2 |
| P20 | 3 | direct |
| P21 | DFS low-link < disc | direct |
| P22 | check all degrees even, connected | direct |
| P23 | repeatedly pick zero-indegree | direct |
| P24 | not bipartite (odd cycle) | direct |
| P25 | DFS uses O(V) recursion; BFS uses O(V) queue | direct |
| P26 | A³[u][v] | matrix power |
| P27 | BFS from source, parent pointers form tree | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Adjacency matrix space O(V+E) | It's O(V²). |
| 2 | BFS gives shortest path always | Only unweighted. |
| 3 | DFS for shortest path | BFS instead. |
| 4 | Topological sort works on cyclic | Only DAG. |
| 5 | Bipartite test fails on disconnected | Run on each component. |
| 6 | SCC for undirected graph | SCC is for directed. |
| 7 | Counting edges by row sums for directed | Each edge counted once. |
| 8 | Forgetting visited[] in BFS/DFS | Infinite loop. |
| 9 | Using DFS recursion for huge graphs | Stack overflow risk. |
| 10 | Treating tree edges = all edges in DFS | Many edge types. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Shortest path unweighted" | BFS. |
| "All paths / cycle" | DFS. |
| "Topological sort" | Kahn or DFS finish times. |
| "SCC" | Kosaraju or Tarjan. |
| "Bipartite" | 2-coloring BFS/DFS. |
| "Articulation / bridge" | DFS low-link. |
| "Walks of length k" | A^k. |
| "Cycle detection" | DFS back edge. |
| "Adjacency space" | matrix V² vs list V+E. |
| "Eulerian / Hamiltonian" | even degrees / NP-hard. |

---

## 9. Quick Revision

```
REPRESENTATIONS
 matrix: O(V²); edge query O(1)
 list: O(V+E); iterate O(deg)
 dense → matrix; sparse → list

BFS
 queue, level-by-level
 O(V+E)
 unweighted shortest path

DFS
 stack/recursion
 O(V+E)
 topological, SCC, cycle

EDGE TYPES (directed DFS)
 tree, back, forward, cross
 back ⇒ cycle

UNDIRECTED DFS
 tree, back only

TOPO SORT (DAG only)
 DFS finish reversed, or Kahn

SCC: Kosaraju (2 DFS), Tarjan (1 DFS)

BIPARTITE: 2-coloring; ⇔ no odd cycle

A^k: walks of length k
ARTICULATION / BRIDGE: DFS low-link

EULERIAN (undirected): all even, connected
HAMILTONIAN: NP-hard
```
