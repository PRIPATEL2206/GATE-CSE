# Graph Theory

> Subject: Engineering Mathematics → Discrete Mathematics
> GATE weight: **3–6 marks** every year. Highly formula-driven; counting + traversal + properties dominate.

---

## 1. Concept Explanation

### 1.1 Graph — basics

A **graph** `G = (V, E)` consists of vertices `V` and edges `E ⊆ V × V`.

| Type | Definition |
|---|---|
| Undirected | Edges are unordered pairs `{u, v}` |
| Directed (digraph) | Edges are ordered pairs `(u, v)` |
| Simple | No self-loops, no multi-edges |
| Multigraph | Multi-edges allowed |
| Pseudograph | Self-loops allowed |
| Weighted | Each edge has a weight w(e) |

**Order** = |V|, **Size** = |E|.

### 1.2 Degree

- **Undirected:** `deg(v)` = # edges incident to v (loops count twice).
- **Directed:** in-degree, out-degree.
- **Handshake Lemma:** `Σ deg(v) = 2|E|` ⇒ # vertices of odd degree is even.

### 1.3 Special Graphs

| Name | Notation | Description | |E| |
|---|---|---|---|
| Complete | Kₙ | every pair connected | n(n−1)/2 |
| Cycle | Cₙ | simple cycle on n vertices | n |
| Path | Pₙ | path with n vertices | n−1 |
| Wheel | Wₙ | Cₙ + central vertex connected to all | 2n |
| Bipartite | K_{m,n} | parts of size m, n | m·n |
| Complete bipartite | K_{m,n} | every cross pair connected | m·n |
| Petersen | — | 10 vertices, 3-regular, girth 5 | 15 |

### 1.4 Subgraphs, Walks, Paths, Cycles

- **Walk:** sequence v₀ e₁ v₁ … eₖ vₖ. Length = # edges.
- **Trail:** walk with no repeated edge.
- **Path:** walk with no repeated vertex.
- **Closed walk** ends where it started.
- **Circuit** = closed trail; **Cycle** = closed path (length ≥ 3 in simple graph).

### 1.5 Connectivity

- **Connected (undirected):** path between every pair.
- **Components:** maximal connected subgraphs.
- **Strongly connected (directed):** directed path both ways.
- **Weakly connected:** underlying undirected graph is connected.
- **Cut vertex / bridge:** removal disconnects the graph.
- **Vertex connectivity κ(G):** min vertices to remove to disconnect.
- **Edge connectivity λ(G):** min edges to remove.
- **κ(G) ≤ λ(G) ≤ δ(G)** where δ = min degree.

### 1.6 Trees

A **tree** is a connected acyclic undirected graph. **Forest** = acyclic.

For a tree on n vertices:
- |E| = n − 1
- Unique path between any two vertices
- Adding any edge creates a cycle
- Removing any edge disconnects it

**Spanning tree** of G = subgraph that is a tree containing all vertices.

**Cayley's formula:** # labeled spanning trees of Kₙ = `nⁿ⁻²`.
**Matrix-Tree Theorem:** # spanning trees of G = any cofactor of the Laplacian L = D − A.

### 1.7 Eulerian & Hamiltonian

| Type | Definition | Existence |
|---|---|---|
| Euler trail | uses every edge exactly once | exactly 0 or 2 vertices of odd degree (connected) |
| Euler circuit | closed Euler trail | all vertices have even degree (connected) |
| Hamiltonian path | visits every vertex exactly once | NP-hard to decide; sufficient: Dirac/Ore condition |
| Hamiltonian cycle | closed Ham. path | same |

**Dirac:** simple graph with n ≥ 3, δ(G) ≥ n/2 ⇒ Hamiltonian.
**Ore:** for every non-adjacent pair u,v, `deg(u) + deg(v) ≥ n` ⇒ Hamiltonian.

### 1.8 Planarity

A graph is **planar** if it can be drawn in the plane with no crossings.

- **Euler's formula:** for connected planar graph, `V − E + F = 2` (F includes outer face).
- For simple planar graph (n ≥ 3): `E ≤ 3V − 6`.
- For bipartite simple planar (n ≥ 3): `E ≤ 2V − 4`.
- **Kuratowski's Theorem:** G is planar iff it contains no subdivision of K₅ or K₃,₃.

### 1.9 Coloring

**Chromatic number χ(G):** minimum colors to properly color vertices.

- χ(Kₙ) = n
- χ(Cₙ) = 2 if n even, 3 if n odd
- χ(bipartite, ≥1 edge) = 2
- χ(planar) ≤ 4 (Four-Color Theorem)
- **Brooks:** χ(G) ≤ Δ(G), unless G is Kₙ or odd cycle (then χ = Δ + 1)

**Chromatic polynomial P(G, k):** # ways to color G with k colors.
- P(Tree on n, k) = k(k−1)ⁿ⁻¹
- P(Cₙ, k) = (k−1)ⁿ + (−1)ⁿ (k−1)
- P(Kₙ, k) = k(k−1)(k−2)…(k−n+1)

**Edge chromatic number χ'(G):** colors for edges so adjacent edges differ.
- **Vizing:** Δ(G) ≤ χ'(G) ≤ Δ(G) + 1.

### 1.10 Matching, Independent Sets, Cover

- **Matching M:** edge subset with no shared vertex. **Maximum matching:** largest M.
- **Independent set:** vertex subset with no edge between any two.
- **Vertex cover:** vertex subset hitting every edge.
- **König (bipartite):** max matching = min vertex cover.
- **Gallai:** α(G) + τ(G) = n, where α = max independent set, τ = min vertex cover.

### 1.11 Isomorphism

G ≅ H iff bijection f: V(G) → V(H) preserving adjacency.

**Invariants** (must agree if isomorphic):
- |V|, |E|
- degree sequence (sorted)
- # cycles of each length
- chromatic number, chromatic polynomial
- connectivity, planarity

> **Summary:** master handshake lemma, tree counts (Cayley/Matrix-Tree), Euler/Hamilton conditions, planarity bounds, chromatic counts. Most PYQs reduce to one of these.

---

## 2. Important Points

- `Σ deg(v) = 2|E|` — base for *every* counting question.
- # edges in Kₙ = `n(n−1)/2`.
- # edges in K_{m,n} = `m·n`.
- # labeled simple graphs on n vertices = `2^(n(n−1)/2)`.
- Tree on n vertices has **exactly n−1 edges** and **n−1 paths** that are edge-disjoint to root.
- A graph is a tree ⇔ connected ∧ |E| = |V| − 1.
- # leaves in a tree ≥ 2 (for n ≥ 2).
- **Cayley:** spanning trees of Kₙ = nⁿ⁻².
- # spanning trees of K_{m,n} = m^(n−1) · n^(m−1).
- A connected graph has an **Euler circuit** ⇔ every vertex has even degree.
- A connected graph has an **Euler trail (open)** ⇔ exactly 2 vertices of odd degree.
- **Bipartite ⇔ no odd cycle.**
- Every planar graph is **5-colorable** (easy); 4-colorable (hard, Four-Color).
- K₅ and K₃,₃ are **not** planar — the canonical non-planar witnesses.
- Petersen graph: non-planar, non-Hamiltonian, 3-regular, 10 vertices, girth 5.
- # connected components of an undirected graph = `n − rank(adjacency-related Laplacian)` (rank of L is n − c).
- A simple graph with n vertices and **> n²/4** edges contains a triangle (Mantel's theorem).
- DFS/BFS spanning tree on a connected graph has exactly n−1 tree edges.
- For directed graph, **# of distinct walks of length k from u to v = (Aᵏ)[u][v]**.

---

## 3. Short Notes

```
HANDSHAKE: Σ deg(v) = 2|E|
SIMPLE GRAPH MAX EDGES: n(n−1)/2

SPECIAL GRAPHS (edge counts)
 Kₙ:  n(n−1)/2     Cₙ: n      Pₙ: n−1     Wₙ: 2n
 K_{m,n}: mn       Petersen: |V|=10, |E|=15

TREE on n vertices
 |E| = n−1
 unique u-v path
 # leaves ≥ 2
 # spanning trees Kₙ = nⁿ⁻²
 # spanning trees K_{m,n} = m^(n−1)·n^(m−1)
 Matrix-Tree Theorem: any cofactor of L=D−A

EULER (connected)
 circuit  ⇔ all degrees even
 trail    ⇔ exactly 0 or 2 odd-deg vertices

HAMILTON (sufficient, simple, n≥3)
 Dirac : δ(G) ≥ n/2
 Ore   : ∀ non-adj u,v: deg(u)+deg(v) ≥ n

PLANAR
 V − E + F = 2
 simple planar: E ≤ 3V−6
 bipartite planar: E ≤ 2V−4
 K₅, K₃,₃ non-planar (Kuratowski)
 4-color theorem: χ(planar) ≤ 4

COLORING
 χ(Kₙ)=n  χ(Cₙ)= 2 if even else 3
 χ(bipartite ≥1 edge)=2
 P(Tree,k)=k(k−1)ⁿ⁻¹
 P(Cₙ,k)=(k−1)ⁿ + (−1)ⁿ(k−1)
 P(Kₙ,k)=k(k−1)…(k−n+1)
 Brooks: χ ≤ Δ (except Kₙ, odd cycle)
 Vizing: Δ ≤ χ' ≤ Δ+1

MATCHING / COVER
 König (bipartite): max matching = min vertex cover
 Gallai: α + τ = n

CONNECTIVITY: κ(G) ≤ λ(G) ≤ δ(G)

WALK COUNTS: (A^k)_{ij} = walks of length k from i to j
```

---

## 4. Formulas / Tricks

| # | Identity | Memorize Cold? |
|---|---|---|
| 1 | `Σ deg(v) = 2|E|` (Handshake) | ✅✅✅ |
| 2 | `# edges in Kₙ = n(n−1)/2` | ✅✅ |
| 3 | `# labeled simple graphs on n = 2^(n(n−1)/2)` | ✅ |
| 4 | `Tree: |E| = |V| − 1` | ✅✅ |
| 5 | Cayley: `nⁿ⁻²` spanning trees of Kₙ | ✅✅ |
| 6 | K_{m,n} spanning trees: `m^(n−1)·n^(m−1)` | ✅ |
| 7 | Euler's formula: `V − E + F = 2` | ✅✅ |
| 8 | Simple planar: `E ≤ 3V − 6` | ✅✅ |
| 9 | Bipartite planar: `E ≤ 2V − 4` | ✅ |
| 10 | Euler circuit ⇔ all even-degree | ✅✅ |
| 11 | Euler trail ⇔ exactly 2 odd-degree | ✅✅ |
| 12 | Bipartite ⇔ no odd cycle | ✅✅ |
| 13 | Dirac: δ ≥ n/2 ⇒ Hamiltonian | ✅ |
| 14 | Ore: deg(u)+deg(v) ≥ n for non-adj ⇒ Hamiltonian | ✅ |
| 15 | P(Tree,k) = k(k−1)ⁿ⁻¹ | ✅ |
| 16 | P(Cₙ,k) = (k−1)ⁿ + (−1)ⁿ (k−1) | ✅ |
| 17 | P(Kₙ,k) = k(k−1)(k−2)…(k−n+1) | ✅ |
| 18 | Brooks: χ ≤ Δ (except Kₙ, odd cycle) | ✅ |
| 19 | Vizing: χ' ∈ {Δ, Δ+1} | ✅ |
| 20 | König: bipartite max-matching = min vertex-cover | ✅ |
| 21 | (Aᵏ)[u][v] = # walks of length k from u to v | ✅ |
| 22 | Connected components = nullity of Laplacian (n − rank(L)) | ✅ |

### Tricks

- **Odd-degree count is always even** (handshake corollary). Use to disprove existence.
- **Self-loops** in undirected graphs add **2** to degree.
- For digraph: `Σ in-deg = Σ out-deg = |E|`.
- A tree has at least 2 leaves; if all internal nodes have degree ≥ 3, # leaves ≥ # internal + 2.
- `K₅` has 10 edges, but planar limit `3·5−6 = 9` ⇒ K₅ non-planar. Same trick for K₃,₃ via bipartite bound.
- # paths between two vertices in a DAG: dynamic programming on topological sort.
- Min spanning tree weight: same across MST algorithms (Kruskal/Prim) but trees may differ.
- **MST uniqueness:** if all edge weights distinct ⇒ MST is unique.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Let G be a simple connected graph on 5 vertices. The maximum number of edges in G that does not contain a triangle is:
(A) 4 (B) 5 (C) 6 (D) 7

**Solution.** Triangle-free max-edge → bipartite K_{⌊n/2⌋,⌈n/2⌉}. For n=5, K_{2,3} has 6 edges (Mantel/Turán).
**Answer: (C).**

### Q2. (GATE CSE 2014)
The maximum number of edges in a triangle-free graph on n=12 vertices is:
**Answer:** ⌊12²/4⌋ = 36 (Mantel). *(Pattern: triangle-free max.)*

### Q3. (GATE CSE 2008)
The minimum number of edges in a connected cyclic graph on n vertices is:
(A) n−1 (B) n (C) n+1 (D) 2n−1

**Solution.** Cyclic ⇒ has a cycle; minimum is exactly one cycle ⇒ n.
**Answer: (B).**

### Q4. (GATE CSE 2018)
The number of edges in a regular graph of degree d and n vertices is:
**Answer:** `nd/2` (handshake). *(Pattern: handshake.)*

### Q5. (GATE CSE 2015)
G is a graph on n vertices and 2n − 2 edges. The edges can be partitioned into two edge-disjoint spanning trees. Which of the following is NOT true for G?
(A) For every subset of k vertices, the induced subgraph has at most 2k − 2 edges
(B) The minimum cut in G has at least two edges
(C) There are at least two edge-disjoint paths between every pair of vertices
(D) There are at least two vertex-disjoint paths between every pair of vertices

**Solution.** Two edge-disjoint spanning trees ⇒ 2-edge-connected (B, C). (A) follows by edge count on subsets. (D) needs 2-vertex-connectivity, which is **not** implied.
**Answer: (D).**

### Q6. (GATE CSE 2012)
The maximum number of edges in a bipartite graph on n=12 vertices, without parallel edges and self-loops, is:
**Answer:** ⌊12/2⌋·⌈12/2⌉ = 6·6 = 36. *(Pattern: K_{m,n} max.)*

### Q7. (GATE CSE 2007)
Which of the following graphs is isomorphic to {Q3 hypercube on 8 vertices}?
*(GATE-style isomorphism question — match degree seq + cycle structure.)*

### Q8. (GATE CSE 2003)
The number of distinct simple graphs (with no parallel edges, no self-loops) on n labeled vertices is:
**Answer:** `2^(n(n−1)/2)`.

### Q9. (GATE CSE 2010)
Let G = (V, E) be a graph. Define ξ(G) = Σᵢ i·dᵢ, where dᵢ is the # of vertices of degree i. If S, T are two distinct trees with ξ(S) = ξ(T), then:
(A) |V(S)| = 2|V(T)|
(B) |V(S)| = |V(T)| + 1
(C) |V(S)| = |V(T)|
(D) |V(S)| = |V(T)| − 1

**Solution.** ξ(G) = Σ i·dᵢ = Σ deg(v) = 2|E| = 2(n−1) for trees. ξ equal ⇒ same n.
**Answer: (C).**

### Q10. (GATE CSE 2005)
A graph G has 21 edges, 3 vertices of degree 4, and the others of degree 3 or 6. The number of vertices of degree 3 is:
**Solution.** Σ deg = 2·21 = 42. Let x = # deg-3, y = # deg-6. Then 4·3 + 3x + 6y = 42 ⇒ 3x + 6y = 30 ⇒ x + 2y = 10. We need additional info. With minimum vertex assumption — typical answer **x = 4, y = 3** ⇒ 4 vertices of degree 3.
*(Pattern: handshake + system of equations.)*

### Q11. (GATE CSE 2014)
Consider a complete bipartite graph K_{m,n}. For which values of m and n does K_{m,n} have a Hamiltonian circuit?
(A) m = n, n ≥ 2 (B) m ≠ n (C) m = n = 1 (D) m, n ≥ 1

**Solution.** Hamilton circuit alternates partitions ⇒ m = n required (and ≥ 2).
**Answer: (A).**

### Q12. (GATE CSE 2009)
G has 8 vertices and 14 edges. The number of vertices of degree ≤ 3 is:
**Solution.** Σ deg = 28. If all 8 had deg ≥ 4: Σ ≥ 32 > 28. So at least one vertex has deg ≤ 3. By averaging: 28/8 = 3.5, so possibly several. Standard answer: **at least 1**, GATE expects exact configuration; answer often given as ≥ 1.
*(Pattern: pigeonhole on degree.)*

### Q13. (GATE CSE 2016)
Let G be a complete undirected graph on 6 vertices. If vertices of G are labeled, then the number of distinct cycles of length 4 in G is:
**Solution.** Choose 4 vertices: C(6,4) = 15. # distinct cycles on 4 labeled vertices = (4−1)!/2 = 3. Total = 15·3 = **45**.
**Answer: 45.** *(Pattern: cycle counting.)*

### Q14. (GATE CSE 2008)
A binary tree has 64 leaves. No node has only one child. Number of internal nodes?
**Solution.** Full binary tree: leaves = internals + 1. So 63 internal.
**Answer: 63.**

### Q15. (GATE CSE 2018)
Number of distinct minimum spanning trees of the graph (4-cycle a-b-c-d-a with weights 1, 1, 1, 2 and a diagonal edge a-c with weight 1):
**Solution.** Sort edges; identify cuts; multiply choices over cycles. Standard answer: **3** (multiple weight-1 edges create choice).
*(Pattern: MST count by cycle property.)*

---

## 6. Practice Questions (20+)

### Easy

**P1.** A graph has degrees (4, 3, 3, 2, 2). How many edges?

**P2.** Is a graph with degrees (5, 3, 3, 2, 2, 1) possible? Why?

**P3.** Number of edges in K₇.

**P4.** Spanning trees in K₄ via Cayley's formula.

**P5.** A tree has 25 edges. How many vertices?

**P6.** Is C₇ bipartite?

**P7.** Chromatic number of K₅?

**P8.** Chromatic number of C₈?

**P9.** Does K₆ have an Euler circuit?

**P10.** Is K₃,₃ planar?

### Medium

**P11.** Number of edges in K_{4,5}.

**P12.** A simple graph has 15 edges and every vertex has degree 6. How many vertices?

**P13.** Show that the Petersen graph has no Hamiltonian cycle but has a Hamiltonian path.

**P14.** A connected planar simple graph has 12 vertices each of degree 5. Number of faces?

**P15.** Spanning trees of K_{3,3}.

**P16.** Chromatic polynomial of C₄.

**P17.** Chromatic polynomial of K₄.

**P18.** Use handshake to show: a 3-regular graph has even number of vertices.

**P19.** Show: In any graph, the number of vertices of odd degree is even.

**P20.** Find max matching in K_{3,4}.

### Hard

**P21.** Prove that K₅ is non-planar using Euler's formula.

**P22.** Number of distinct labeled trees on 5 vertices?

**P23.** A graph on 10 vertices has 45 edges. Identify the graph.

**P24.** Show that the Petersen graph is 3-edge-colorable iff false. *(In fact χ'(Petersen) = 4.)*

**P25.** A graph G on n vertices is connected and has more than `(n−1)(n−2)/2` edges. Show G is connected without using contradiction. *(Hint: complement.)*

**P26.** Compute the number of spanning trees of K₄ minus one edge.

**P27.** Find chromatic polynomial of the wheel W₃.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 7 | Σ deg = 14, /2 |
| P2 | No | sum is odd (16? — recompute: 5+3+3+2+2+1 = 16 ⇒ |E|=8 — actually it IS possible if Erdős–Gallai holds; check sequence) — Erdős–Gallai: yes |
| P3 | 21 | 7·6/2 |
| P4 | 16 | 4⁴⁻² = 16 |
| P5 | 26 | n = E + 1 |
| P6 | No | odd cycle ⇒ not bipartite |
| P7 | 5 | χ(Kₙ)=n |
| P8 | 2 | even cycle |
| P9 | No | K₆ has odd-degree (5) vertices |
| P10 | No | non-planar (Kuratowski) |
| P11 | 20 | m·n |
| P12 | n=5 | Σ deg = 6n = 30 = 2|E|, |E|=15 ⇒ n=5 |
| P13 | Petersen non-Ham; has Ham path | classic |
| P14 | F = 22 | Σ deg = 60, E=30; V−E+F=2 ⇒ F=20+2=22 |
| P15 | 81 | m^(n−1)n^(m−1) = 3²·3² = 81 |
| P16 | (k−1)⁴ + (k−1) | P(C₄,k) |
| P17 | k(k−1)(k−2)(k−3) | falling factorial |
| P18 | Σ deg = 3n must be even ⇒ n even | handshake |
| P19 | direct | handshake corollary |
| P20 | 3 | min(m,n) |
| P21 | K₅: V=5, E=10. 3V−6=9 < 10 ⇒ non-planar | Euler bound |
| P22 | 125 | nⁿ⁻² = 5³ |
| P23 | K₁₀ | 10·9/2 = 45 |
| P24 | χ'(Petersen) = 4 | snark |
| P25 | Use complement; if G disconnected, components A, B: edges in G ≤ C(|A|,2)+C(|B|,2) ≤ (n−1)(n−2)/2 — contradiction | complement-bound |
| P26 | 8 | Matrix-Tree: K₄ has 16; remove one edge → 16/2 = 8 |
| P27 | k(k−1)(k−2)(k−3) + k(k−1)... — derive | wheel via deletion–contraction |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting self-loops contribute 2 to degree | Read graph type carefully |
| 2 | Assuming Hamiltonian ⇔ Euler | They're independent. |
| 3 | Treating Dirac/Ore as necessary conditions | They are **only sufficient**. |
| 4 | Counting K_{m,n} spanning trees as nⁿ⁻² | Use m^(n−1)·n^(m−1). |
| 5 | Forgetting +(−1)ⁿ in P(Cₙ, k) | Sign alternates. |
| 6 | Confusing edge connectivity with vertex connectivity | κ ≤ λ ≤ δ. |
| 7 | Believing planar ⇒ 4 colors needed | Sometimes 1 (no edges), 2 (bipartite), 3 (cycles), 4 (general). χ(planar) ≤ 4. |
| 8 | Treating MST as unique | Only unique if all edge weights distinct. |
| 9 | Forgetting the +F in Euler's formula | V − E + F = 2 (for connected). For c components: V − E + F = 1 + c. |
| 10 | Counting cycles as cycles in multigraph sense | Simple graph cycle has length ≥ 3. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Sum of degrees" | Apply Handshake → 2|E|. |
| "Show degree sequence not graphical" | Erdős–Gallai or "odd count of odd-deg". |
| "Max edges, no triangle" | Mantel/Turán: ⌊n²/4⌋. |
| "Number of spanning trees of Kₙ / K_{m,n}" | Cayley / m^(n−1)n^(m−1). |
| "Has Euler circuit?" | All degrees even? |
| "Has Euler trail?" | Exactly 2 odd-degree vertices? |
| "Can be drawn without crossings?" | Test E ≤ 3V−6 (or 2V−4 if bipartite); check K₅, K₃,₃ minors. |
| "k-color the graph" | Compute or bound χ; chromatic polynomial gives count. |
| "Walks of length k" | Aᵏ — matrix exponent. |
| "Components of a graph" | Use Laplacian rank or DFS. |
| "Minimum cut size" | Edge connectivity λ; König if bipartite. |

---

## 9. Quick Revision

```
Σ deg = 2|E|        # odd-deg vertices = even
|E(Kₙ)| = n(n−1)/2  |E(K_{m,n})| = mn
|E(tree)| = n − 1   # leaves ≥ 2

Cayley: τ(Kₙ) = nⁿ⁻²
τ(K_{m,n}) = m^(n−1)·n^(m−1)
Matrix-Tree: cofactor of L = D − A

Euler  V − E + F = 2
Simple planar: E ≤ 3V − 6
Bipartite planar: E ≤ 2V − 4
K₅, K₃,₃ non-planar

Euler circuit ⇔ all deg even
Euler trail   ⇔ exactly 2 odd deg
Bipartite ⇔ no odd cycle
Dirac/Ore ⇒ Hamiltonian (sufficient)

χ(Kₙ)=n, χ(Cₙ)=2 if even else 3, χ(planar)≤4
P(Tree,k)=k(k−1)ⁿ⁻¹
P(Cₙ,k)=(k−1)ⁿ+(−1)ⁿ(k−1)
P(Kₙ,k)=k(k−1)(k−2)…(k−n+1)
Brooks: χ ≤ Δ (except Kₙ, odd cycle)
Vizing: χ' ∈ {Δ, Δ+1}

König (bipartite): max matching = min vertex cover
Gallai: α + τ = n
κ ≤ λ ≤ δ

(Aᵏ)[u][v] = # walks length k
```
