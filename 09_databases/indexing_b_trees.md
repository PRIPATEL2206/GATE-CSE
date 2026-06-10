# File Organization & Indexing (B / B+ Trees)

> Subject: Databases
> GATE weight: **2–4 marks** every year. Index types, B/B+ tree operations, height/capacity calculations.

---

## 1. Concept Explanation

### 1.1 File Organization

Storage of records in a file:

| Type | Description |
|---|---|
| **Heap (unordered)** | Insert anywhere; slow lookup |
| **Sorted (sequential)** | Sorted by key; binary search |
| **Hashed** | Hash function maps key → bucket |
| **Indexed** | Auxiliary structure for fast lookup |
| **Clustered** | Data physically sorted by index |

### 1.2 Index

Data structure mapping search key to record location.

| Type | Description |
|---|---|
| **Primary** | On primary key; dictates data ordering (clustered) |
| **Secondary** | On non-key; doesn't dictate ordering (non-clustered) |
| **Dense** | Index entry per record |
| **Sparse** | Index entry per block |
| **Multi-level** | Index on the index |

### 1.3 Single vs Multi-level Index

**Single-level:** O(log n) seeks via binary search but the index itself can be huge.
**Multi-level:** index of index → O(log_B n) for tree-based.

### 1.4 B-Tree

Self-balancing m-ary tree. Properties:

- All leaves at same depth.
- Root has at least 2 children (unless leaf).
- Internal node (except root) has ≥ ⌈m/2⌉ children.
- All nodes have **≤ m children**.
- A node with k children has **k − 1 keys**.

For order m B-tree:
- Min keys per non-root: ⌈m/2⌉ − 1.
- Max keys: m − 1.

### 1.5 B-Tree Operations

| Operation | Time |
|---|---|
| Search | O(log_m n) disk accesses |
| Insert | O(log_m n) |
| Delete | O(log_m n) |

**Insert:** if leaf full → split.
**Delete:** if underflow → borrow from sibling or merge.

### 1.6 B+ Tree

Variant of B-tree:
- **All data records stored at leaves.**
- Internal nodes only have keys (for routing).
- Leaves linked together (sequential access).

**Advantages:**
- Better for range queries.
- Sequential access via leaf links.
- Less complexity in internal nodes.

### 1.7 B+ Tree Properties

For order m (max children):
- Internal node: ⌈m/2⌉ ≤ children ≤ m.
- Leaf: ⌈(m−1)/2⌉ ≤ keys ≤ m − 1.

### 1.8 B-Tree vs B+ Tree

| Feature | B-Tree | B+ Tree |
|---|---|---|
| Data location | All nodes | Leaves only |
| Key duplicates | No | Yes (in leaves and internal) |
| Range query | Slow | Fast (linked leaves) |
| Sequential access | No | Yes |
| Common use | Less common | DB indexes, file systems |

### 1.9 B+ Tree Height & Capacity

For order m, # records n:
- Height ≈ log_⌈m/2⌉(n)
- # leaf nodes = ⌈n / (m−1)⌉ approx.

**Example:** m = 100, n = 10⁶:
- Height ≈ log_50(10⁶) ≈ 4 levels → 4 disk accesses.

### 1.10 Hash Indexes

Hash key → bucket → records.

**Pros:** O(1) point lookup.
**Cons:** No range queries, hash collisions need management.

**Static hashing:** fixed buckets.
**Dynamic hashing:** extendible hashing, linear hashing.

### 1.11 Extendible Hashing

Directory of pointers to buckets. Directory size = 2^d (global depth d).

**Bucket overflow:** double directory if needed; split bucket.

### 1.12 Linear Hashing

Buckets split in linear order; no full directory doubling.

### 1.13 Bitmap Index

Bitmap per distinct value.

**Best for low-cardinality columns** (e.g., gender, status).

### 1.14 Inverted Index

Map terms → list of documents (used in search engines).

### 1.15 Index Selection

| Need | Index |
|---|---|
| Equality lookup | Hash or B+ tree |
| Range query | B+ tree |
| Low cardinality | Bitmap |
| Full-text search | Inverted index |
| Geographic | R-tree |

### 1.16 Concurrency on B+ Trees

Latch-coupling, B-link trees, optimistic descent — for high concurrency.

### 1.17 Disk-based Considerations

Indexes minimize disk I/O. B+ tree node size matches disk block size (e.g., 4 KB).

### 1.18 Common GATE Calculations

**Order from block size:**
- Block size = 4096 B.
- Key = 16 B, pointer = 8 B.
- Internal: m·8 + (m−1)·16 ≤ 4096 → m ≤ 171.
- Leaf with record pointers: similar.

### 1.19 Range Query

**B+ tree:** find leaf, follow leaf chain.
**B-tree:** in-order traversal.

### 1.20 Bulk Loading

Build B+ tree from sorted data more efficiently than n inserts.

> **Summary:** Indexes speed up lookups. B-tree (data anywhere) vs B+ tree (data at leaves, linked). Hash for equality, B+ tree for range. Multi-level indexing reduces I/O. Compute order from disk block size.

---

## 2. Important Points

- **Primary index** = on primary key; clustered.
- **Secondary index** = on non-key; non-clustered.
- **Dense index:** entry per record.
- **Sparse index:** entry per block.
- **B-tree:** balanced m-ary tree.
- **B+ tree:** data at leaves; leaves linked.
- **B+ tree fanout** typically 50–500 in real systems.
- **Hash index:** O(1) equality but no range.
- **Extendible hashing:** dynamic; doubles directory.
- **Bitmap index:** low cardinality columns.
- **Range query:** B+ tree leaf traversal.
- **Multi-level index:** index of indexes.
- **B+ tree height** logarithmic in n with high fanout.

---

## 3. Short Notes

```
FILE ORGANIZATION
 heap, sorted, hashed, indexed, clustered

INDEX TYPES
 primary (clustered) / secondary (non-clustered)
 dense / sparse
 single-level / multi-level

B-TREE (order m)
 root ≥ 2 children
 internal ≥ ⌈m/2⌉ children
 max m children
 all leaves at same depth
 keys = children − 1
 ops: O(log_m n)

B+ TREE
 data at leaves only
 internal nodes for routing
 leaves linked → range queries
 better for DB indexes

B-TREE vs B+ TREE
 data location, range, sequential access

ORDER CALCULATION
 from block size, key size, pointer size

HASH INDEX
 O(1) equality
 no range
 static or dynamic

EXTENDIBLE HASHING
 directory + buckets, dynamic doubling

LINEAR HASHING: linear bucket split

BITMAP INDEX: low cardinality
INVERTED INDEX: text search
R-TREE: geographic

INDEX SELECTION
 equality → hash
 range → B+ tree
 low cardinality → bitmap

DISK BLOCK = node size for B+ tree

RANGE QUERY: leaf traversal in B+ tree

BULK LOADING for new index
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | B-tree order m: internal ≥ ⌈m/2⌉ children | ✅✅ |
| 2 | B+ tree data at leaves; leaves linked | ✅✅✅ |
| 3 | Search/insert/delete: O(log_m n) | ✅✅ |
| 4 | Primary index = clustered | ✅ |
| 5 | Dense vs sparse | ✅ |
| 6 | Hash O(1) equality only | ✅✅ |
| 7 | Range query → B+ tree | ✅✅ |
| 8 | Bitmap → low cardinality | ✅ |
| 9 | Extendible hashing dynamic | ✅ |
| 10 | Order from block size | ✅ |

### Tricks

- **For order calculation:** total bytes for keys + pointers ≤ block size.
- **For B+ tree height:** log_⌈m/2⌉ of total entries.
- **For range queries:** B+ tree wins.
- **For point queries:** hash wins (typically).
- **For low-cardinality columns:** bitmap.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
B-tree order m: max keys per node:
**Solution.** m − 1.

### Q2. (GATE CSE 2014)
B+ tree advantage over B-tree:
**Solution.** Range queries via linked leaves.

### Q3. (GATE CSE 2018)
Hash index suitable for:
**Solution.** Equality search.

### Q4. (GATE CSE 2008)
Primary index is:
**Solution.** Clustered (data ordered by index).

### Q5. (GATE CSE 2010)
Dense index has:
**Solution.** One entry per record.

### Q6. (GATE CSE 2015)
B+ tree data location:
**Solution.** Leaves only.

### Q7. (GATE CSE 2013)
Order calculation: block 4096 B, key 16 B, pointer 8 B. Max order m for internal node:
**Solution.** 8m + 16(m−1) ≤ 4096 → 24m ≤ 4112 → m ≤ 171.

### Q8. (GATE CSE 2007)
Bitmap index best for:
**Solution.** Low-cardinality columns.

### Q9. (GATE CSE 2003)
Extendible hashing:
**Solution.** Dynamic; directory doubles when bucket overflows.

### Q10. (GATE CSE 2009)
B-tree height of order 100, n = 10⁶:
**Solution.** ≈ log_50(10⁶) ≈ 4.

### Q11. (GATE CSE 2019)
Sparse index entry:
**Solution.** Per block.

### Q12. (GATE CSE 2020)
Range query via B+ tree:
**Solution.** Find lower bound; traverse leaves.

### Q13. (GATE CSE 2021)
Bulk loading B+ tree:
**Solution.** Build from sorted data; bottom-up.

### Q14. (GATE CSE 2016)
B-tree node minimum children:
**Solution.** ⌈m/2⌉ for non-root.

### Q15. (GATE CSE 2011)
B+ tree fanout effect:
**Solution.** Higher fanout → lower height → fewer disk accesses.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define index.

**P2.** Primary vs secondary index.

**P3.** Dense vs sparse.

**P4.** B-tree property.

**P5.** B+ tree key feature.

**P6.** Hash index limitation.

**P7.** Bitmap index ideal use.

**P8.** B-tree max keys.

**P9.** B+ tree leaf links.

**P10.** Range query algorithm in B+ tree.

### Medium

**P11.** Compute B+ tree order: block 8192 B, key 16 B, pointer 4 B.

**P12.** Compute B+ tree height for n = 10⁹, m = 100.

**P13.** Insert key in B+ tree; show split.

**P14.** Delete key; show borrow/merge.

**P15.** Compare hash vs B+ tree for equality.

**P16.** Apply extendible hashing on small example.

**P17.** Bitmap index for gender column.

**P18.** Range query trace in B+ tree.

**P19.** Multi-level index.

**P20.** Identify index type for given query.

### Hard

**P21.** Implement B-tree insert.

**P22.** Implement B+ tree insert and delete.

**P23.** Apply linear hashing to dataset.

**P24.** Compare B+ tree vs hash performance.

**P25.** Bulk load B+ tree from sorted records.

**P26.** Choose index for OLTP vs OLAP.

**P27.** Concurrent B+ tree operations.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | search structure | direct |
| P2 | clustered vs non | direct |
| P3 | per record vs per block | direct |
| P4 | balanced m-ary | direct |
| P5 | data at leaves | direct |
| P6 | no range | direct |
| P7 | low cardinality | direct |
| P8 | m − 1 | direct |
| P9 | sequential access | direct |
| P10 | find lower; traverse | direct |
| P11 | trace formula | direct |
| P12 | log_50(10⁹) ≈ 6 | direct |
| P13 | trace | direct |
| P14 | trace | direct |
| P15 | hash O(1); B+ O(log) | direct |
| P16 | trace | direct |
| P17 | 2 bitmaps | direct |
| P18 | leaf chain | direct |
| P19 | index of index | direct |
| P20 | match query type | direct |
| P21 | balanced insert | direct |
| P22 | classic | direct |
| P23 | linear bucket | direct |
| P24 | depends on query | direct |
| P25 | bottom-up | direct |
| P26 | B+ for OLTP | direct |
| P27 | latching | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | B-tree = B+ tree | Different. |
| 2 | Hash supports range | Doesn't. |
| 3 | Primary key requires unique | Yes. |
| 4 | Sparse index always smaller | Usually yes. |
| 5 | B+ tree leaves not linked | They are. |
| 6 | Bitmap good for high cardinality | No: low. |
| 7 | Order = max keys | Order = max children typically. |
| 8 | Multi-level same as B-tree | Different concepts. |
| 9 | Index always speeds up | Insert/update slower with index. |
| 10 | Hash index for SELECT | Only equality. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Compute B+ tree order" | Block size / (key + pointer). |
| "B+ tree height" | log_⌈m/2⌉(n). |
| "Range query" | B+ tree. |
| "Equality lookup" | Hash or B+ tree. |
| "Low cardinality" | Bitmap. |
| "Full-text" | Inverted index. |
| "Primary vs secondary" | Clustered vs non. |
| "Dense vs sparse" | Per record vs per block. |
| "Extendible hashing" | Dynamic doubling. |
| "Bulk load" | Bottom-up. |

---

## 9. Quick Revision

```
FILE ORGANIZATION
 heap / sorted / hashed / indexed / clustered

INDEX
 primary (clustered) / secondary
 dense / sparse
 single / multi-level

B-TREE (order m)
 root ≥ 2 children
 internal ≥ ⌈m/2⌉ children
 max m children
 keys = children − 1
 ops O(log_m n)
 all leaves same depth

B+ TREE
 data at leaves
 leaves linked
 better for range queries

ORDER from block size:
 m·ptr_size + (m−1)·key_size ≤ block_size

HASH
 O(1) equality only
 static or dynamic
 extendible (directory) / linear

BITMAP: low cardinality
INVERTED: text search
R-TREE: spatial

CHOICE
 equality → hash
 range → B+ tree
 low card → bitmap

DISK BLOCK = node size

BULK LOADING for new index
```
