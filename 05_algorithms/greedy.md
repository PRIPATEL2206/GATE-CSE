# Greedy Algorithms

> Subject: Algorithms
> GATE weight: **2–4 marks** every year. Activity selection, fractional knapsack, Huffman, MST (Kruskal/Prim), Dijkstra preview.

---

## 1. Concept Explanation

### 1.1 Greedy Strategy

A **greedy algorithm** makes the locally optimal choice at each step, hoping it leads to a globally optimal solution.

**Two key properties** must hold for correctness:
1. **Greedy choice property:** a globally optimal solution can be reached by making a locally optimal choice.
2. **Optimal substructure:** an optimal solution to the problem contains optimal solutions to subproblems.

### 1.2 General Recipe

1. Cast problem as making a sequence of choices.
2. Define greedy criterion (e.g., earliest finish, smallest weight).
3. Prove greedy correctness (exchange argument or induction).
4. Implement.

### 1.3 Activity Selection Problem

Given n activities with start sᵢ and finish fᵢ. Select max number of non-overlapping activities.

**Greedy:** sort by finish time; pick earliest finish; skip overlapping; repeat.

**Time:** O(n log n) for sort.

**Correctness (exchange argument):** any optimal solution can be modified to start with the earliest-finishing activity without reducing count.

### 1.4 Fractional Knapsack

n items with weight wᵢ and value vᵢ. Bag capacity W. Items can be split.

**Greedy:** sort by **value/weight ratio**; pack highest-ratio first; if last item exceeds remaining capacity, take fraction.

**Time:** O(n log n).

**Difference from 0/1 knapsack:** 0/1 must be solved with DP; greedy doesn't work.

### 1.5 Huffman Coding

Build prefix-free binary code minimizing expected codeword length, given character frequencies.

**Greedy:**
1. Build min-heap of all chars (priority = frequency).
2. Extract two smallest; create new node with sum frequency; insert.
3. Repeat until one node remains.
4. Tree edges: 0 (left) / 1 (right) → codes.

**Time:** O(n log n).

**Property:**
- Most frequent char → shortest code.
- Codes are prefix-free.
- Optimal among prefix codes.

### 1.6 Job Scheduling with Deadlines

n jobs, each with deadline dᵢ and profit pᵢ. Each takes 1 unit time. Maximize profit.

**Greedy:** sort by profit desc; place each job in latest free slot ≤ its deadline.

**Time:** O(n²) naive; O(n log n) with union-find.

### 1.7 Minimum Spanning Tree (MST)

Spanning tree of weighted connected graph with minimum total edge weight.

**Two greedy algorithms:**

| Algorithm | Approach | Time |
|---|---|---|
| **Kruskal** | Pick smallest edge that doesn't form cycle | O(E log E) |
| **Prim** | Grow tree from vertex; pick min outgoing edge | O(E log V) with heap |

### 1.8 Kruskal's Algorithm

```
Sort edges by weight.
For each edge (u, v):
  If u and v are in different components:
    Add (u, v) to MST.
    Union components.
Stop when n − 1 edges added.
```

**Data structure:** Union-Find (Disjoint Set Union, DSU).

### 1.9 Prim's Algorithm

```
Start at any vertex; mark visited.
While there are unvisited vertices:
  Find min-weight edge (u, v) where u is visited, v is not.
  Add (u, v) to MST; mark v visited.
```

**Implementations:**
- Adjacency matrix: O(V²).
- Adjacency list + binary heap: O(E log V).
- + Fibonacci heap: O(E + V log V).

### 1.10 Cut Property (MST Correctness)

For any cut (S, V−S), the **lightest edge** crossing the cut is in **some** MST. (Greedy choice is safe.)

### 1.11 Cycle Property

For any cycle C, the **heaviest edge** in C is **not** in any MST (unless ties).

### 1.12 Dijkstra's Algorithm (preview)

Shortest path from source to all vertices in graph with **non-negative** weights.

**Greedy:** repeatedly select unvisited vertex with smallest known distance; relax neighbours.

**Time:** O((V + E) log V) with binary heap.

(Full coverage in [graph_algorithms.md](graph_algorithms.md).)

### 1.13 Set Cover (counterexample)

Greedy doesn't always give optimum. For Set Cover, greedy gives **O(log n)** approximation, not exact.

### 1.14 Coin Change Problem

Given coins {c₁, …, cₖ} and amount W. Minimize coins.

**Greedy works** for canonical systems (e.g., {1, 5, 10, 25}).
**Greedy fails** for arbitrary systems (e.g., {1, 3, 4} for W = 6: greedy picks 4+1+1 = 3 coins; optimal is 3+3 = 2 coins).

For arbitrary systems, use DP.

### 1.15 Huffman Properties Summary

- Optimal prefix code.
- Codes have variable length.
- Building Huffman tree: O(n log n).
- Encoding: O(message length × avg code length).
- Decoding: traverse tree.

### 1.16 When Greedy Fails

- 0/1 Knapsack (use DP).
- Coin change with arbitrary denominations.
- Longest path (NP-hard in general).
- TSP (NP-hard).

For these, DP, branch-and-bound, or approximation needed.

### 1.17 Exchange Argument

To prove greedy correctness:
1. Assume optimal solution differs from greedy.
2. Show that swapping a greedy choice into the optimal doesn't decrease quality.
3. Iterate; reach pure greedy without losing optimality.

> **Summary:** Greedy = locally optimal choices. Master activity selection, fractional knapsack, Huffman, Kruskal/Prim. Know when greedy works (matroid structure / exchange argument) and when it fails (0/1 knapsack, arbitrary coin change).

---

## 2. Important Points

- **Greedy needs both** greedy choice property AND optimal substructure.
- **Activity selection** uses earliest-finish-time first.
- **Fractional knapsack** uses highest value/weight ratio.
- **0/1 knapsack** is NOT solvable greedily (use DP).
- **Huffman codes** are optimal **prefix-free** codes.
- **Most frequent char** in Huffman has **shortest code**.
- **Kruskal** uses union-find; **Prim** uses priority queue.
- **MST is unique** if all edge weights are distinct.
- **Cut property** justifies greedy MST.
- **Cycle property:** heaviest edge in any cycle is excluded from MST.
- **Dijkstra fails on negative edges** — use Bellman-Ford instead.
- **Coin change greedy** works only for canonical systems.
- **Exchange argument** is the standard proof technique.
- **Greedy approximations** can give bounded-ratio solutions for NP-hard problems.

---

## 3. Short Notes

```
GREEDY PROPERTIES
 1. greedy choice
 2. optimal substructure

ACTIVITY SELECTION
 sort by finish time
 pick earliest finish
 O(n log n)

FRACTIONAL KNAPSACK
 sort by v/w ratio desc
 pack greedily, fraction at end
 O(n log n)
 (0/1 knapsack: DP only)

HUFFMAN
 min-heap of frequencies
 extract 2 smallest, combine
 most frequent → shortest code
 O(n log n)

JOB SCHEDULING (deadlines)
 sort by profit desc
 latest free slot ≤ deadline
 O(n log n) with DSU

MST
 Kruskal: sort edges + union-find — O(E log E)
 Prim: priority queue — O(E log V)
 cut property: lightest edge across cut in some MST
 cycle property: heaviest edge in cycle not in MST
 unique MST if edges distinct

DIJKSTRA (preview)
 non-negative weights only
 O((V+E) log V) with heap

COIN CHANGE
 greedy works for canonical (1, 5, 10, 25)
 fails for {1, 3, 4} on W=6

WHEN GREEDY FAILS
 0/1 knapsack
 coin change (general)
 TSP, longest path

EXCHANGE ARGUMENT
 swap greedy choice into optimal
 quality preserved
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Activity selection: earliest finish | ✅✅ |
| 2 | Fractional knapsack: max v/w ratio | ✅✅ |
| 3 | 0/1 knapsack: DP, not greedy | ✅✅ |
| 4 | Huffman: combine two smallest | ✅✅ |
| 5 | Kruskal: O(E log E) | ✅✅ |
| 6 | Prim: O(E log V) with heap | ✅✅ |
| 7 | Cut property | ✅ |
| 8 | Cycle property | ✅ |
| 9 | Unique MST when weights distinct | ✅ |
| 10 | Dijkstra: non-negative weights | ✅ |
| 11 | Coin change greedy fails on {1,3,4} | ✅ |

### Tricks

- **Activity selection trick:** finish-time ordering ensures each pick leaves max room.
- **Knapsack: 0/1 vs fractional:** the divisibility unlocks greedy correctness.
- **Huffman frequency counting:** sum of weighted depths = avg code length.
- **MST with negative weights** still works (only Dijkstra fails).
- **Kruskal with parallel edges:** sort + skip duplicates.
- **For large MST problems:** Prim with Fibonacci heap → O(E + V log V).

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Activity selection greedy criterion:
**Solution.** Earliest finish time.

### Q2. (GATE CSE 2014)
Fractional knapsack greedy criterion:
**Solution.** Max value-to-weight ratio.

### Q3. (GATE CSE 2018)
Number of edges in MST of n-vertex connected graph:
**Solution.** n − 1.

### Q4. (GATE CSE 2008)
Kruskal time complexity:
**Solution.** O(E log E) = O(E log V).

### Q5. (GATE CSE 2010)
Huffman code: most frequent char has:
**Solution.** Shortest code.

### Q6. (GATE CSE 2015)
Prim's complexity with binary heap:
**Solution.** O(E log V).

### Q7. (GATE CSE 2013)
Coin change for {1, 3, 4} with W = 6 using greedy:
**Solution.** 4 + 1 + 1 = 3 coins (suboptimal); optimal is 3 + 3 = 2.

### Q8. (GATE CSE 2007)
For 0/1 knapsack, greedy gives:
**Solution.** Sub-optimal (use DP).

### Q9. (GATE CSE 2003)
Number of distinct MSTs of a graph:
**Solution.** Depends on edge-weight multiplicity.

### Q10. (GATE CSE 2009)
Activity selection time:
**Solution.** O(n log n).

### Q11. (GATE CSE 2019)
Huffman tree of {a:5, b:9, c:12, d:13, e:16, f:45}: avg code length?
**Solution.** Build tree; sum f · code length.

### Q12. (GATE CSE 2020)
MST with negative-weight edges allowed?
**Solution.** Yes (greedy still works).

### Q13. (GATE CSE 2021)
Cut property:
**Solution.** Lightest edge across cut is in some MST.

### Q14. (GATE CSE 2016)
Dijkstra fails on:
**Solution.** Negative edge weights.

### Q15. (GATE CSE 2011)
Difference between Kruskal and Prim:
**Solution.** Kruskal sorts edges globally; Prim grows tree from start vertex.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Greedy criterion for activity selection?

**P2.** Greedy criterion for fractional knapsack?

**P3.** Does greedy work for 0/1 knapsack?

**P4.** Huffman greedy property?

**P5.** Kruskal data structure?

**P6.** Prim data structure?

**P7.** Number of edges in MST?

**P8.** Cut property statement?

**P9.** Cycle property?

**P10.** Dijkstra with negative weights?

### Medium

**P11.** Activities (1,4),(3,5),(0,6),(5,7),(8,9). Max non-overlapping?

**P12.** Fractional knapsack: items (v,w) = (60,10),(100,20),(120,30); W=50. Optimal value?

**P13.** Build Huffman tree for {a:1, b:2, c:3, d:4, e:5}.

**P14.** Run Kruskal on graph: edges (1,2,1),(2,3,2),(1,3,3),(3,4,4). MST?

**P15.** Run Prim from vertex 1 on same graph.

**P16.** Coin change {1,3,5}, W=11 — greedy result?

**P17.** Job scheduling: jobs (deadline, profit) = (2,100),(1,50),(2,30),(1,20). Max profit?

**P18.** MST for graph with all equal weights?

**P19.** Greedy for set cover — approximation ratio?

**P20.** Difference between fractional and 0/1 knapsack?

### Hard

**P21.** Prove Kruskal's correctness using cut property.

**P22.** Implement Huffman encoding and decoding.

**P23.** Prove activity selection greedy works (exchange argument).

**P24.** Find MST of weighted graph with 6 vertices using both Kruskal and Prim; compare.

**P25.** Show greedy fails for 0/1 knapsack with example.

**P26.** Optimal merge pattern: minimize merging cost of n sorted lists.

**P27.** Construct Huffman code for English alphabet with given frequencies.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | earliest finish | direct |
| P2 | max v/w | direct |
| P3 | no | direct |
| P4 | merge smallest two | direct |
| P5 | union-find | direct |
| P6 | priority queue | direct |
| P7 | n − 1 | direct |
| P8 | lightest edge across cut in MST | direct |
| P9 | heaviest edge in cycle not in MST | direct |
| P10 | fails | direct |
| P11 | 3 | (1,4),(5,7),(8,9) |
| P12 | 240 | items 1, 2 fully + 2/3 of 3 |
| P13 | trace | direct |
| P14 | edges (1,2),(2,3),(3,4) | direct |
| P15 | similar | direct |
| P16 | 5+5+1 = 3 coins (greedy = optimal here) | canonical |
| P17 | 100 + 50 = 150 | greedy with deadlines |
| P18 | many possible MSTs | direct |
| P19 | O(log n) | direct |
| P20 | divisibility | direct |
| P21 | use cut property | direct |
| P22 | tree-based | direct |
| P23 | swap last activity to earliest | direct |
| P24 | trace | direct |
| P25 | items (40,1),(50,2),(60,3) W=4: greedy=40+50=90; optimal=60+40=100 | direct |
| P26 | Huffman-like merging | direct |
| P27 | apply Huffman | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Using greedy for 0/1 knapsack | Only fractional. |
| 2 | Wrong MST algorithm complexity | Kruskal: E log E; Prim: E log V. |
| 3 | Dijkstra with negative weights | Use Bellman-Ford. |
| 4 | Coin change greedy on arbitrary system | May be suboptimal. |
| 5 | Forgetting Huffman is optimal only among prefix codes | Other codes (e.g., arithmetic) can do better. |
| 6 | MST not unique with duplicate weights | May have multiple MSTs. |
| 7 | Activity selection sort by start time | Use finish time. |
| 8 | Set cover greedy gives optimal | Only O(log n) approximation. |
| 9 | Cut property gives the unique MST edge | Only lightest. |
| 10 | Treating local optimum as global | Need exchange argument or matroid. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Activity selection" | Sort by finish; pick earliest. |
| "Fractional knapsack" | Sort by v/w; pack greedily. |
| "0/1 knapsack" | DP, not greedy. |
| "Huffman code" | Min-heap merge. |
| "MST" | Kruskal or Prim. |
| "Shortest path non-negative" | Dijkstra. |
| "Coin change canonical" | Greedy. |
| "Coin change arbitrary" | DP. |
| "Job scheduling deadlines" | Sort by profit, greedy slot fill. |
| "Greedy fails: example" | 0/1 knapsack or arbitrary coin change. |
| "Cut property" | Lightest across cut. |
| "Cycle property" | Heaviest in cycle not in MST. |

---

## 9. Quick Revision

```
GREEDY PROPERTIES
 greedy choice + optimal substructure

ACTIVITY SELECTION: earliest finish; O(n log n)

FRACTIONAL KNAPSACK: max v/w; O(n log n)
0/1 KNAPSACK: DP only

HUFFMAN: min-heap merge two smallest
 most freq → shortest code; O(n log n)

JOB SCHED (deadlines): sort by profit; latest slot
 O(n log n) with DSU

MST
 Kruskal: O(E log E) (union-find)
 Prim: O(E log V) (heap)
 cut property; cycle property
 unique iff weights distinct

DIJKSTRA: non-negative; O((V+E) log V)

COIN CHANGE
 canonical → greedy
 arbitrary → DP

EXCHANGE ARGUMENT
 swap greedy into optimal; preserve quality
```
