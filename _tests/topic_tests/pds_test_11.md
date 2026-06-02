# Topic Test 11 — PDS (Trees · Graphs · Hashing)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Inorder traversal of BST gives:
(A) Reverse sorted  (B) Sorted ascending  (C) Random  (D) Pre-order

**Q2.** [NAT] Min height of BST with 31 distinct keys = `____`

**Q3.** [MCQ] Number of distinct BSTs with 4 keys:
(A) 14  (B) 24  (C) 16  (D) 12

**Q4.** [MCQ] AVL balance factor range:
(A) {0,1}  (B) {-1,0,1}  (C) {-2,-1,0,1,2}  (D) {-1,0}

**Q5.** [MCQ] Build-heap from n elements:
(A) O(log n)  (B) O(n)  (C) O(n log n)  (D) O(n²)

**Q6.** [MCQ] Heap parent of index 10 (1-indexed):
(A) 4  (B) 5  (C) 9  (D) 20

**Q7.** [NAT] Max nodes in binary tree of height 5 = `____`

**Q8.** [MCQ] Adjacency matrix space:
(A) O(V+E)  (B) O(V²)  (C) O(E)  (D) O(V·E)

**Q9.** [MCQ] BFS uses:
(A) Stack  (B) Queue  (C) Heap  (D) Hash table

**Q10.** [MCQ] DFS time with adjacency list:
(A) O(V)  (B) O(E)  (C) O(V+E)  (D) O(V·E)

**Q11.** [MCQ] BFS gives shortest path in:
(A) Unweighted  (B) Negative weights  (C) DAG  (D) Any graph

**Q12.** [MCQ] Topological sort works only on:
(A) Trees  (B) DAG  (C) Cyclic  (D) Bipartite

**Q13.** [MCQ] Best collision resolution to avoid clustering:
(A) Linear probing  (B) Quadratic  (C) Double hashing  (D) Chaining

**Q14.** [NAT] Hash table m=10, h(k)=k mod 10. Bucket of 47 = `____`

**Q15.** [MCQ] Load factor for 100 keys in 50-slot chained hash table:
(A) 0.5  (B) 1  (C) 2  (D) 5

---

## Section B — 2 marks each

**Q16.** [MCQ] Postorder of BST built by inserting 5,3,8,2,4,7,9:
(A) 2 4 3 7 9 8 5  (B) 2 4 3 7 9 8 5  (C) 5 3 8 2 4 7 9  (D) 9 8 7 5 4 3 2

**Q17.** [NAT] Min nodes in AVL of height 4 = `____`

**Q18.** [MCQ] Heap [50, 30, 40, 10, 20]: is it a max-heap?
(A) Yes  (B) No  (C) Min-heap  (D) Neither

**Q19.** [MCQ] Insert keys 12, 19, 23, 5 into hash table m=7 with linear probing, h(k)=k mod 7. Final array (- = empty):
(A) [-, -, 23, -, -, 12, 19, 5] *(wait this is m=8)*; m=7: [-, -, 23, 5, 12, 19, -] check positions
(B) Slots: 12→5, 19→5(coll)→6, 23→2, 5→5(coll)→6(coll)→0
(C) Final pos for 5 in slot 0
(D) None of above

**Q20.** [MCQ] Adjacency matrix M of undirected graph with 4 vertices, 5 edges. # of 1's in M?
(A) 5  (B) 10  (C) 16  (D) 20

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | sorted |
| 2 | 4 | ⌈log₂ 32⌉ − 1 |
| 3 | (A) 14 | C₄ |
| 4 | (B) | direct |
| 5 | (B) O(n) | bottom-up sift-down |
| 6 | (B) 5 | i/2 |
| 7 | 63 | 2⁶ − 1 |
| 8 | (B) O(V²) | direct |
| 9 | (B) Queue | direct |
| 10 | (C) O(V+E) | direct |
| 11 | (A) Unweighted | direct |
| 12 | (B) DAG | direct |
| 13 | (C) Double hashing | direct |
| 14 | 7 | 47 mod 10 |
| 15 | (C) 2 | n/m |
| 16 | (A) 2 4 3 7 9 8 5 | trace BST |
| 17 | 12 | N(0)=1, N(1)=2, N(2)=4, N(3)=7, N(4)=12 |
| 18 | (A) Yes | each parent ≥ children |
| 19 | (C) | 5 ends at slot 0 after probes |
| 20 | (B) 10 | undirected: 2E |

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
- < 18 → re-do PYQs of all three topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
