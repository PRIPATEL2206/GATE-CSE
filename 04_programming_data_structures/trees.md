# Trees (BST, AVL, Heaps)

> Subject: Programming & Data Structures
> GATE weight: **3–6 marks** every year. Tree traversals, BST operations, AVL rotations, heap operations.

---

## 1. Concept Explanation

### 1.1 Tree Terminology

| Term | Definition |
|---|---|
| **Root** | Topmost node (no parent) |
| **Parent / Child** | Direct ancestor / descendant |
| **Leaf** | Node with no children |
| **Internal node** | Non-leaf |
| **Edge** | Connection between two nodes |
| **Depth(v)** | Length of path from root to v (root has depth 0) |
| **Height(v)** | Longest path from v to a leaf |
| **Height of tree** | Height of root |
| **Level** | Set of nodes at same depth |
| **Degree of node** | # children |
| **Forest** | Disjoint union of trees |

### 1.2 Binary Tree

Each node has **at most 2** children (left, right).

| Type | Definition |
|---|---|
| **Full / Strict** | Every internal node has 2 children |
| **Complete** | All levels filled except possibly last; last filled left-to-right |
| **Perfect** | All internal have 2 children, all leaves at same level |
| **Balanced** | Heights of subtrees differ by ≤ constant |
| **Skewed** | All nodes have only one child (worst-case BST) |

### 1.3 Counting Properties (n nodes, height h)

| Property |
|---|
| Min height of n-node binary tree = ⌈log₂(n+1)⌉ − 1 (~ log₂ n) |
| Max height = n − 1 (skewed) |
| Max # nodes at depth d = 2^d |
| Max # nodes in tree of height h = 2^(h+1) − 1 |
| Min # leaves of full binary tree with n nodes = (n+1)/2 |
| In any binary tree: # leaves = (# internal nodes with 2 children) + 1 |

### 1.4 Tree Traversals

For binary tree with root, left subtree L, right subtree R:

| Traversal | Order |
|---|---|
| **Preorder** | Root, L, R |
| **Inorder** | L, Root, R |
| **Postorder** | L, R, Root |
| **Level-order (BFS)** | Level by level |

Each takes O(n).

### 1.5 Reconstructing Tree from Traversals

- **Inorder + Preorder** → unique tree.
- **Inorder + Postorder** → unique tree.
- **Preorder + Postorder** alone → not unique (need full tree).
- **Inorder alone or any single traversal** → not enough.

**Algorithm (Preorder + Inorder):**
1. First element of preorder = root.
2. Find root in inorder; left part = left subtree, right part = right subtree.
3. Recurse.

### 1.6 Binary Search Tree (BST)

Property: for every node, left subtree keys < node key < right subtree keys.

| Operation | Average | Worst |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Min/Max | O(log n) | O(n) |

**Inorder traversal** of BST → **sorted order**.

### 1.7 BST Insertion

```
1. Compare key with node.
2. Smaller → go left; greater → go right.
3. Insert at first NULL.
```

### 1.8 BST Deletion (3 cases)

| Case | Action |
|---|---|
| Leaf | Just remove |
| One child | Replace with child |
| Two children | Replace with **inorder successor** (min of right subtree) or predecessor; then delete that node |

### 1.9 BST Worst-Case Issue

If insertions are sorted → skewed tree, height O(n) → operations degrade to O(n).

**Solution:** self-balancing trees (AVL, Red-Black).

### 1.10 AVL Tree

Self-balancing BST. **Balance factor** of a node = height(left) − height(right) ∈ {−1, 0, +1}.

If balance factor goes outside, perform rotations.

### 1.11 AVL Rotations

| Imbalance | Rotation |
|---|---|
| **LL** (left subtree of left child too heavy) | Right rotate |
| **RR** (right subtree of right child too heavy) | Left rotate |
| **LR** (left's right too heavy) | Left rotate child, then right rotate |
| **RL** (right's left too heavy) | Right rotate child, then left rotate |

Each rotation is O(1); insertion/deletion still O(log n).

### 1.12 AVL Properties

- Height of AVL with n nodes is O(log n).
- Minimum nodes in AVL of height h: `N(h) = N(h−1) + N(h−2) + 1` (Fibonacci-like; N(0)=1, N(1)=2).
- Search/Insert/Delete: O(log n) worst-case.

### 1.13 Red-Black Tree

Another self-balancing BST. Properties:
- Every node is red or black.
- Root and NIL leaves are black.
- Red node's children are black.
- Every path from root to NIL has same # of black nodes.
- Height ≤ 2 log₂(n+1).

Faster modifications (fewer rotations) than AVL but slightly higher height.

### 1.14 Binary Heap

Complete binary tree with **heap property**:
- **Max-heap:** parent ≥ children.
- **Min-heap:** parent ≤ children.

**Storage:** array, root at index 1 (or 0).
- Parent of i: i/2 (i−1)/2 if 0-indexed.
- Left child: 2i (2i+1).
- Right child: 2i+1 (2i+2).

### 1.15 Heap Operations

| Operation | Time |
|---|---|
| Insert | O(log n) — bubble up |
| Extract-Max/Min | O(log n) — replace root with last, sift down |
| Build-Heap (from array) | O(n) — bottom-up sift-down |
| Heapify (sift-down) | O(log n) |
| Decrease-key (with index) | O(log n) |

**Build-Heap analysis:** Σ heights ≤ 2n ⇒ O(n).

### 1.16 Heap Sort

1. Build max-heap: O(n).
2. Repeatedly extract-max; place at end: O(n log n).
3. Total: O(n log n).

In-place; not stable.

### 1.17 Priority Queue

ADT with:
- Insert(x, priority)
- ExtractMax (or Min)

Implemented with binary heap (most common), Fibonacci heap (better amortized), or sorted/unsorted array.

### 1.18 Other Trees (overview)

| Tree | Use |
|---|---|
| **B-tree / B+-tree** | Disk-based indexes (DBMS) |
| **Trie** | String prefix matching |
| **Segment tree** | Range queries, updates |
| **Fenwick (BIT)** | Prefix sum updates |
| **Suffix tree / array** | String pattern matching |
| **Splay tree** | Self-adjusting, amortized O(log n) |

### 1.19 N-ary Tree

Each node has at most N children. Generalizes binary tree. Used in file systems, syntax trees.

### 1.20 Special Counting Identities

For a binary tree with n internal nodes:
- # leaves = n + 1 (in full binary tree).
- Total nodes = 2n + 1.

For a tree (non-binary):
- # leaves + # internal = n; # edges = n − 1.

> **Summary:** Master tree traversals, BST operations + complexity, reconstruction from traversals, AVL rotations (4 cases), heap as array, heap operations, and counting identities.

---

## 2. Important Points

- **In any rooted tree:** # of edges = n − 1 (n nodes).
- **Inorder of BST** is sorted.
- **Pre+In** or **Post+In** uniquely reconstructs tree; pre+post doesn't.
- **AVL height** is O(log n) — guaranteed.
- **Binary heap** is **complete** binary tree → can be stored in array.
- **Build-heap** is **O(n)**, not O(n log n).
- **Insertions in sorted order** create skewed BST, not AVL.
- **Number of distinct BSTs with n keys** = Catalan Cₙ.
- **Number of distinct binary trees with n nodes** = Catalan Cₙ.
- **Heap is NOT BST** — heap property allows any order between siblings.
- **Binary heap insert** rebalances by sift-up; extract by sift-down.
- **Min-heap finds min in O(1)**; max in O(n).
- **Successor in BST**: min of right subtree, or first ancestor where you turned right going up.
- **AVL minimum nodes(h)** ≈ Fibonacci → AVL height ≤ 1.44 · log₂(n).
- **Red-Black** allows more flexibility, common in C++ map/set, Java TreeMap.

---

## 3. Short Notes

```
TREE TERMS
 root, leaf, parent, child, depth, height, level, degree
 height of tree = height of root

BINARY TREE
 full: every internal has 2 children
 complete: filled L-R level by level
 perfect: all leaves at same depth
 balanced: heights diff ≤ const
 skewed: linear chain

PROPERTIES (n nodes, h height)
 min h ≈ log₂ n
 max h = n − 1
 max nodes at depth d = 2^d
 max nodes in h-height tree = 2^(h+1) − 1
 # leaves = #(2-children internal) + 1

TRAVERSALS
 preorder (R,L,R) [misprint] preorder = R, L_subtree, R_subtree
 inorder = L, R, R_subtree
 postorder = L, R, R_subtree
 level-order (BFS)
 each O(n)

RECONSTRUCT
 in + pre or in + post → unique
 pre + post insufficient

BST
 left < node < right
 search/insert/delete: O(log n) avg, O(n) worst
 inorder = sorted

BST DELETION
 leaf: remove
 1 child: replace with child
 2 children: replace with inorder successor

AVL
 BF = h(L) − h(R) ∈ {−1, 0, +1}
 rotations: LL → R; RR → L; LR → L+R; RL → R+L
 height O(log n) guaranteed

HEAP (binary)
 complete binary tree
 max-heap: parent ≥ children
 min-heap: parent ≤ children
 array storage:
   parent: i/2; left: 2i; right: 2i+1

HEAP OPS
 insert: O(log n) sift-up
 extract: O(log n) sift-down
 build-heap: O(n) bottom-up
 heap-sort: O(n log n) in-place

#BSTs with n keys = #binary trees with n nodes = Catalan Cₙ

OTHER TREES
 B+-tree (DB), Trie (strings)
 Segment tree, Fenwick (range)
 Splay (amortized self-adjust)
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | Edges = n − 1 in tree | ✅✅ |
| 2 | Max nodes at depth d = 2^d | ✅✅ |
| 3 | Max nodes in tree height h = 2^(h+1) − 1 | ✅✅ |
| 4 | Min height ≈ log₂(n+1) − 1 | ✅✅ |
| 5 | Max height = n − 1 (skewed) | ✅ |
| 6 | # distinct BSTs / binary trees with n nodes = Cₙ | ✅✅ |
| 7 | Heap parent: i/2; children: 2i, 2i+1 | ✅✅ |
| 8 | Build-heap: O(n) | ✅✅ |
| 9 | Heap sort: O(n log n) | ✅ |
| 10 | AVL rotations: LL/RR/LR/RL | ✅✅ |
| 11 | AVL height bound: ≤ 1.44 log₂ n | ✅ |
| 12 | Inorder of BST = sorted | ✅✅ |
| 13 | # leaves = #(2-child internal) + 1 in binary tree | ✅ |

### Tricks

- **Reconstructing tree from inorder + preorder:** root = preorder[0]; partition inorder around root; recurse.
- **Find successor in BST without parent ptr:** stack-based or iterative inorder.
- **Heap from array:** use bottom-up sift-down (build-heap), not n inserts (which would be O(n log n)).
- **AVL imbalance detection:** while inserting, update balance factor at each ancestor; first node with |BF| > 1 = imbalance point.
- **Counting trees:** apply Catalan formula `Cₙ = C(2n,n)/(n+1)`.
- **For BST with n distinct keys:** # arrangements producing same BST varies; specific question types use Catalan.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Inorder of a BST gives:
**Solution.** Sorted order.

### Q2. (GATE CSE 2014)
Number of distinct BSTs with 5 keys:
**Solution.** C₅ = 42.

### Q3. (GATE CSE 2018)
Build-heap from n elements:
**Solution.** O(n).

### Q4. (GATE CSE 2008)
Tree with preorder ABCDEF and inorder CBADEF. Postorder?
**Solution.** Reconstruct: Root A; inorder L = CBA, wait must split correctly. Actually inorder is "CBADEF" — A is root, left subtree inorder = "CB", right subtree = "DEF". Preorder of left = "BC" (after A: take next 2). Build... continue until full. Postorder typically: CBFEDA.

### Q5. (GATE CSE 2010)
Min height of BST with 16 distinct keys:
**Solution.** ⌈log₂(17)⌉ − 1 = 4.

### Q6. (GATE CSE 2015)
AVL rotation when inserting causes left-right imbalance:
**Solution.** LR rotation (left rotate child then right rotate).

### Q7. (GATE CSE 2013)
Heap with 100 elements; max-heap. Min element location?
**Solution.** Some leaf — could be at any leaf position.

### Q8. (GATE CSE 2007)
Insert sequence 5, 3, 8, 2, 4 into BST. Inorder?
**Solution.** 2 3 4 5 8.

### Q9. (GATE CSE 2003)
A complete binary tree with 15 nodes. Height?
**Solution.** ⌈log₂(16)⌉ − 1 = 3.

### Q10. (GATE CSE 2009)
Number of nodes in min-height AVL of height 4:
**Solution.** N(4) = N(3) + N(2) + 1; with N(0)=1, N(1)=2 → N(2)=4, N(3)=7, N(4)=12.

### Q11. (GATE CSE 2019)
Heap sort time complexity:
**Solution.** O(n log n).

### Q12. (GATE CSE 2020)
Binary tree with n nodes; max # of leaves?
**Solution.** ⌈n/2⌉ for complete binary tree, but in general up to (n+1)/2 for full binary tree.

### Q13. (GATE CSE 2021)
Number of binary trees with 4 distinct nodes (unlabeled in shape):
**Solution.** C₄ = 14.

### Q14. (GATE CSE 2016)
A min-heap stored as array: index 1 root. Children of index 4?
**Solution.** 8 and 9.

### Q15. (GATE CSE 2011)
BST: search 5 in tree with root 7, left subtree {3, 1, 5}, right {10}. Comparisons?
**Solution.** 7→3→5: 3 comparisons.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define BST.

**P2.** Inorder of BST gives what order?

**P3.** Max # of nodes at depth d?

**P4.** AVL balance factor ranges?

**P5.** Heap parent index of node 10?

**P6.** Heap children of index 5?

**P7.** Time complexity of heap insert?

**P8.** Number of edges in tree with 100 nodes?

**P9.** Postorder of BST {2,3,5} inserted in order 3,2,5?

**P10.** AVL rotation for RR imbalance?

### Medium

**P11.** Reconstruct tree: preorder ABDCEF, inorder DBAECF.

**P12.** AVL minimum nodes for height 5.

**P13.** Insert sequence 50,30,70,20,40,60,80 into AVL. Final tree?

**P14.** Build min-heap from [5, 9, 3, 7, 1].

**P15.** Heap sort steps for [4, 10, 3, 5, 1].

**P16.** Number of distinct BSTs with 4 keys.

**P17.** Find inorder successor in BST.

**P18.** Convert BST to sorted doubly LL.

**P19.** Diameter of binary tree definition.

**P20.** Recursively compute height of binary tree.

### Hard

**P21.** Find LCA of two nodes in BST.

**P22.** Number of binary trees with n nodes (Catalan).

**P23.** AVL after inserting 30, 20, 10 — show rotation.

**P24.** Convert max-heap to min-heap.

**P25.** Find k-th smallest in BST.

**P26.** Reconstruct binary tree from postorder + inorder.

**P27.** Implement priority queue using min-heap.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | left < node < right | direct |
| P2 | sorted | direct |
| P3 | 2^d | direct |
| P4 | {−1, 0, +1} | direct |
| P5 | 5 | i/2 |
| P6 | 10 and 11 | 2i and 2i+1 |
| P7 | O(log n) | direct |
| P8 | 99 | n − 1 |
| P9 | 2 5 3 | direct |
| P10 | left rotate | direct |
| P11 | recursive | direct |
| P12 | N(5) = N(4) + N(3) + 1 = 12 + 7 + 1 = 20 | direct |
| P13 | balanced | direct |
| P14 | [1,5,3,7,9] | sift-down |
| P15 | trace | direct |
| P16 | C₄ = 14 | Catalan |
| P17 | min of right subtree | direct |
| P18 | inorder + reassign pointers | direct |
| P19 | longest path between any two nodes | direct |
| P20 | 1 + max(h(L), h(R)) | direct |
| P21 | first node where keys diverge | direct |
| P22 | Cₙ = C(2n,n)/(n+1) | direct |
| P23 | LL imbalance → right rotate | direct |
| P24 | rebuild | direct |
| P25 | inorder traversal, count k | direct |
| P26 | root = postorder[end]; partition; recurse | direct |
| P27 | insert + extract | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Treating heap as BST | Heap allows any order between siblings. |
| 2 | Confusing pre/in/post order | Memorize positions. |
| 3 | Using BST insert order assumption | BST shape depends on insertion order. |
| 4 | Forgetting AVL rotation cases | LL, RR, LR, RL — 4 cases. |
| 5 | Build-heap = O(n log n) (myth) | It's O(n). |
| 6 | Assuming heap is balanced AVL | Heap is complete, not balanced BST. |
| 7 | Number of BSTs with n keys ≠ Catalan? | It is Cₙ for distinct unlabeled. |
| 8 | Confusing complete vs full vs perfect | Definitions differ. |
| 9 | Inorder doesn't imply BST | Only sorted-output is sorted. |
| 10 | Postorder of BST not necessarily sorted | Only inorder is. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Inorder of BST" | Sorted. |
| "Reconstruct tree from traversals" | Need (in + pre) or (in + post). |
| "AVL rotation" | Identify imbalance type (LL/RR/LR/RL). |
| "Heap operations" | Use array indexing; sift-up / sift-down. |
| "# distinct BSTs with n keys" | Catalan Cₙ. |
| "Min height of n-node tree" | ⌈log₂(n+1)⌉ − 1. |
| "Build heap in O(n)" | Bottom-up sift-down. |
| "Heap sort" | Build-heap + n extracts. |
| "Successor in BST" | Min of right subtree. |
| "LCA in BST" | First node where keys diverge. |

---

## 9. Quick Revision

```
TREE
 edges = n − 1
 max nodes at d = 2^d
 max nodes in h tree = 2^(h+1) − 1
 min h ≈ log₂(n+1) − 1

TRAVERSALS
 preorder: root, L, R
 inorder: L, root, R
 postorder: L, R, root
 BFS: level-order

RECONSTRUCT
 in + pre or in + post

BST
 left < node < right
 inorder = sorted
 ops O(log n) avg, O(n) worst

BST DELETE
 leaf, 1 child, 2 children (use successor)

AVL
 BF ∈ {−1, 0, +1}
 rotations: LL, RR, LR, RL
 height O(log n)
 N(h) ≈ Fibonacci

HEAP
 complete BT
 array: parent i/2; children 2i, 2i+1
 insert: sift-up O(log n)
 extract: sift-down O(log n)
 build-heap: O(n)
 heap-sort: O(n log n)

#BSTs with n distinct keys = Cₙ

OTHER
 B-tree (disk)
 Trie (strings)
 Segment / Fenwick (range)
 Splay (amortized)
```
