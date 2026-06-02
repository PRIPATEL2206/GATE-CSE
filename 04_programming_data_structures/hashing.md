# Hashing

> Subject: Programming & Data Structures
> GATE weight: **1–3 marks** every year. Hash functions, collision resolution, load factor, expected time.

---

## 1. Concept Explanation

### 1.1 Hashing Idea

Map keys → integer indices in a fixed-size table for O(1) average-time access.

| Component | Description |
|---|---|
| **Universe U** | All possible keys |
| **Table size m** | Number of buckets |
| **Hash function h: U → [0, m−1]** | Maps key to bucket |
| **Collision** | h(k₁) = h(k₂) for distinct k₁, k₂ |

### 1.2 Hash Function Properties

A good hash function:
- Distributes keys **uniformly** across [0, m−1].
- Computes in O(1).
- Deterministic (same key → same hash).
- Minimizes collisions.

### 1.3 Common Hash Functions

| Method | Formula |
|---|---|
| **Division** | h(k) = k mod m. Pick m = prime, not near 2^p. |
| **Multiplication** | h(k) = ⌊m · (k · A mod 1)⌋, A ∈ (0,1). Knuth: A = (√5−1)/2. |
| **Universal** | Random h from a family; for any (k₁, k₂), Pr[h(k₁)=h(k₂)] ≤ 1/m. |
| **Folding** | Split key into pieces, combine. |
| **Mid-square** | Square key, take middle digits. |

### 1.4 Collision Resolution: Chaining

Each slot holds a **linked list** of all colliding keys.

| Operation | Time |
|---|---|
| Search | O(1 + α) avg |
| Insert | O(1) (or O(1+α) with check for duplicates) |
| Delete | O(1 + α) avg |

Where α = n/m = **load factor**.

**Worst case:** O(n) if all keys collide.

### 1.5 Collision Resolution: Open Addressing

All keys stored in the table itself. On collision, probe alternative slots.

**Probe sequence:** h(k, 0), h(k, 1), h(k, 2), …

| Method | Probe Function |
|---|---|
| **Linear probing** | h(k, i) = (h'(k) + i) mod m |
| **Quadratic probing** | h(k, i) = (h'(k) + c₁·i + c₂·i²) mod m |
| **Double hashing** | h(k, i) = (h₁(k) + i·h₂(k)) mod m |

**Load factor α = n/m, must be < 1.** Open addressing degrades sharply as α → 1.

### 1.6 Linear Probing Issues

**Primary clustering:** consecutive occupied slots grow → long probe sequences.

Expected probes:
- Successful: ~ ½(1 + 1/(1 − α))
- Unsuccessful: ~ ½(1 + 1/(1 − α)²)

For α = 0.5: ~1.5 / ~2.5 probes.

### 1.7 Quadratic Probing Issues

**Secondary clustering:** keys hashing to same index follow same probe sequence.

Better than linear, but still has clustering.

### 1.8 Double Hashing

Best collision resolution among open-addressing.

`h(k, i) = (h₁(k) + i · h₂(k)) mod m`

Choose h₂(k) so that gcd(h₂(k), m) = 1 (relatively prime) → all m slots reachable.

Expected probes ≈ 1/(1 − α).

### 1.9 Deletion in Open Addressing

Cannot simply mark slot as empty (would break probe chain). Use **TOMBSTONE** marker.

### 1.10 Load Factor & Resizing

When α exceeds threshold (typically 0.75), **rehash** into a larger table (typically 2m).

- Allocate new table of size 2m (or next prime).
- Reinsert each existing key with new hash.

Rehashing cost amortized O(1) per insertion.

### 1.11 Performance Comparison

| Strategy | Avg Search | Worst Search |
|---|---|---|
| Chaining | O(1 + α) | O(n) |
| Linear probing | O(1/(1−α)) | O(n) |
| Quadratic | O(1/(1−α)) | O(n) |
| Double hashing | O(1/(1−α)) | O(n) |

### 1.12 Universal Hashing

Family H of hash functions where for any k₁ ≠ k₂:
`Pr_{h ∈ H}[h(k₁) = h(k₂)] ≤ 1/m`

Random selection prevents adversary from causing worst-case.

### 1.13 Cryptographic Hashing (overview)

- MD5 (broken), SHA-1 (broken), SHA-256 (current).
- Used for integrity, signatures, password storage.
- **Not** designed for hash tables.

### 1.14 Bloom Filter (preview)

Probabilistic structure for set membership.
- Multiple hash functions.
- Bit array.
- False positives possible; no false negatives.
- Space-efficient.

### 1.15 Applications of Hashing

- Hash tables (Python dict, Java HashMap, C++ unordered_map).
- Caches.
- Symbol tables in compilers.
- Database indexing.
- Cryptography.

### 1.16 Common GATE Problem Types

1. Compute hash table state after a sequence of inserts.
2. Compute load factor.
3. Compute expected probes.
4. Identify collisions.
5. Apply linear/quadratic/double hashing on a sequence.

> **Summary:** Master chaining vs open addressing, load factor effects, common probe sequences, deletion handling. Compute hash table contents step-by-step for problems.

---

## 2. Important Points

- **Hash function:** uniform, fast, deterministic.
- **Load factor α = n/m**.
- **Chaining:** allows α > 1; performance degrades linearly.
- **Open addressing:** requires α < 1; performance degrades sharply.
- **Linear probing:** simple but causes primary clustering.
- **Quadratic probing:** reduces primary, still secondary.
- **Double hashing:** uses 2 hash functions; minimal clustering.
- **Tombstones** required for deletion in open addressing.
- For chaining, **expected search time = O(1 + α)**.
- For open addressing, expected probes ≈ 1/(1 − α).
- **m should be prime** for division-method hash to avoid clustering on factors.
- **Universal hashing** prevents adversarial inputs.
- Hash table operations average O(1) but worst-case O(n) (all collide).
- **Rehashing** doubles table when α > 0.75 (typical).
- **Cryptographic hashes** are different — focus on integrity, not bucket distribution.

---

## 3. Short Notes

```
HASH TABLE
 universe U → [0, m−1]
 hash function h(k)
 load factor α = n/m

HASH FUNCTIONS
 division: k mod m (m prime)
 multiplication: ⌊m·(k·A mod 1)⌋
 universal: random h from family

COLLISION: h(k₁) = h(k₂)

CHAINING
 each slot: linked list
 search: O(1+α) avg, O(n) worst
 insert: O(1)
 α can exceed 1

OPEN ADDRESSING
 linear: (h'(k) + i) mod m
 quadratic: (h'(k) + c₁i + c₂i²) mod m
 double: (h₁(k) + i·h₂(k)) mod m
 α < 1 required
 expected probes ≈ 1/(1−α)

DELETION
 chaining: remove from list
 open addr: tombstone marker

REHASHING
 when α > threshold (e.g., 0.75)
 allocate 2m, rehash all keys

CRYPTO HASHES
 MD5/SHA-1 broken; SHA-256 current
 not for hash tables

BLOOM FILTER
 multiple hash functions, bit array
 false positives possible, no false negatives
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | Load factor α = n/m | ✅✅ |
| 2 | Chaining avg search = O(1+α) | ✅✅ |
| 3 | Open addressing probes ≈ 1/(1−α) | ✅✅ |
| 4 | Linear probing successful probes ≈ ½(1 + 1/(1−α)) | ✅ |
| 5 | Linear probing unsuccessful ≈ ½(1 + 1/(1−α)²) | ✅ |
| 6 | Double hashing best of open addressing | ✅ |
| 7 | Use prime m for division method | ✅ |
| 8 | Tombstone for open-address deletion | ✅ |
| 9 | Rehash threshold ~ 0.75 | ✅ |
| 10 | Universal hashing prevents adversarial worst-case | ✅ |

### Tricks

- **Compute hash table state:** track each insert step.
- **Identify collisions:** apply hash to each key; group same-bucket keys.
- **For linear probing problems:** trace probe chain.
- **For quadratic probing problems:** add 1², 2², 3², … to base hash.
- **For double hashing:** apply h₁ first, then add h₂ multiples.
- **Compute final position after collisions:** trace one step at a time.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Hash table size 7 with linear probing. Insert keys 12, 22, 9, 36, 24 using h(k) = k mod 7. Final positions?

**Solution.**
- 12 mod 7 = 5 → slot 5.
- 22 mod 7 = 1 → slot 1.
- 9 mod 7 = 2 → slot 2.
- 36 mod 7 = 1 → collision; probe slot 2 (occupied by 9); slot 3 free → 36 at 3.
- 24 mod 7 = 3 → collision; probe slot 4 free → 24 at 4.

**Final:** [_, 22, 9, 36, 24, 12, _]

### Q2. (GATE CSE 2014)
Load factor 0.75 — what does it mean?
**Solution.** 75% of slots occupied (n/m = 0.75).

### Q3. (GATE CSE 2018)
Best collision resolution to avoid clustering:
**Solution.** Double hashing.

### Q4. (GATE CSE 2008)
Linear probing successful search expected probes when α = 0.5:
**Solution.** ½·(1 + 1/0.5) = 1.5.

### Q5. (GATE CSE 2010)
Universal hashing prevents:
**Solution.** Adversarial worst-case (deterministic collisions).

### Q6. (GATE CSE 2015)
Hash function h(k) = k mod 10 with chaining; load factor for n = 50 keys?
**Solution.** α = 5.

### Q7. (GATE CSE 2013)
Quadratic probing fixes primary clustering but not:
**Solution.** Secondary clustering.

### Q8. (GATE CSE 2007)
Why prime m for division hashing?
**Solution.** Avoid clustering on factors of m.

### Q9. (GATE CSE 2003)
Insert 1, 2, 3, 4 in hash table size 5 with h(k) = k mod 5. Use linear probing. Position of 5 after 1,2,3,4 inserts then 5?
**Solution.** Slots 1, 2, 3, 4 occupied; 5 mod 5 = 0; position 0 free → slot 0.

### Q10. (GATE CSE 2009)
Tombstone in hash table is for:
**Solution.** Marking deleted slot in open addressing.

### Q11. (GATE CSE 2019)
Hash table with chaining, 100 keys, 50 buckets. Avg search?
**Solution.** O(1 + 2) = O(3). Practically: 2.5 (avg of 1+α).

### Q12. (GATE CSE 2020)
Insert 5, 13, 21 in hash table m=8 with h(k)=k mod 8. Collisions?
**Solution.** 5 mod 8 = 5; 13 mod 8 = 5 → collide; 21 mod 8 = 5 → collide.

### Q13. (GATE CSE 2021)
Double hashing requires:
**Solution.** Two different hash functions; gcd(h₂(k), m) = 1.

### Q14. (GATE CSE 2016)
Hashing with chaining inserting n keys into m slots: expected length of longest chain?
**Solution.** O(log n / log log n) (probabilistic balls-and-bins).

### Q15. (GATE CSE 2011)
Closed hashing = open addressing — true?
**Solution.** Yes (terminology).

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define load factor.

**P2.** What is collision in hashing?

**P3.** Open addressing requires α < ?

**P4.** Chaining can have α > 1?

**P5.** Best collision-resolution method avoiding clustering?

**P6.** What's a tombstone?

**P7.** Compute h(25) for h(k) = k mod 7.

**P8.** Hash function should be deterministic — why?

**P9.** Why prime m for division hashing?

**P10.** Cryptographic hash example?

### Medium

**P11.** Insert 11, 22, 33 into hash table size 10 with chaining. Show buckets.

**P12.** Insert keys 7, 14, 21 with linear probing into size 7 table.

**P13.** Compute load factor for 200 keys in 250-slot table.

**P14.** Quadratic probe: h(k, i) = (h(k) + i²) mod m. Show probes for collision.

**P15.** Double hashing: h₁(k)=k mod 7, h₂(k)=5−(k mod 5). Insert 49, 50.

**P16.** Expected probes in linear probing when α = 0.8?

**P17.** Why use universal hashing?

**P18.** Bloom filter property:

**P19.** Insert 12, 18, 13, 2, 3 in hash table m=10, h(k)=k mod 10. Find bucket of each.

**P20.** Implement chaining in pseudocode.

### Hard

**P21.** Trace linear probing for keys 1, 11, 21, 31 with m=10, h(k)=k mod 10.

**P22.** Quadratic probing trace for 4 keys all hashing to slot 2, m=11.

**P23.** Compute # probes for unsuccessful search in linear probing α=0.9.

**P24.** Hash table with chaining; analyze worst-case time.

**P25.** Implement deletion with tombstone.

**P26.** Compare expected probes for linear, quadratic, double hashing at α=0.5.

**P27.** Resize hash table when α exceeds 0.75.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | n/m | direct |
| P2 | h(k₁) = h(k₂) | direct |
| P3 | < 1 | direct |
| P4 | yes | direct |
| P5 | double hashing | direct |
| P6 | deletion marker | direct |
| P7 | 4 | direct |
| P8 | reproducible | direct |
| P9 | avoid clustering | direct |
| P10 | SHA-256 | direct |
| P11 | all to bucket 1 (chained) | direct |
| P12 | trace probes | direct |
| P13 | 0.8 | direct |
| P14 | trace | direct |
| P15 | trace | direct |
| P16 | ½·(1 + 1/0.2) = 3 | direct |
| P17 | adversarial protection | direct |
| P18 | false positives possible | direct |
| P19 | trace | direct |
| P20 | direct | direct |
| P21 | 1, 2, 3, 4 (after probe) | direct |
| P22 | 2, 3, 7, 0 (with i² probes) | direct |
| P23 | ~50.5 | direct |
| P24 | O(n) all-collision | direct |
| P25 | mark deleted slot | direct |
| P26 | linear ~1.5, quad ~1.4, double ~1.39 | direct |
| P27 | rehash all keys | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Treating α > 1 in open addressing | Only chaining allows it. |
| 2 | Forgetting tombstones in open addressing | Required for correctness. |
| 3 | Linear probing on m = 2^k | Causes severe clustering. |
| 4 | Using non-prime m | Clusters on factors. |
| 5 | Hash function depends on data position | Must be uniform. |
| 6 | Cryptographic hash for hash table | They're different goals. |
| 7 | Bloom filter false negatives | They don't exist; only false positives. |
| 8 | Mixing chaining and open addressing | Pick one. |
| 9 | Forgetting to rehash on resize | Old hashes won't fit new size. |
| 10 | Treating load factor as percentage capacity | It's n/m, can exceed 1 for chaining. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Insert and find positions in linear probing" | Trace step-by-step. |
| "Compute load factor" | n/m. |
| "Best collision resolution" | Double hashing. |
| "Probes for successful/unsuccessful linear" | Use formulas. |
| "Universal hashing benefit" | Adversarial protection. |
| "Tombstone usage" | Open addressing deletion. |
| "Rehash threshold" | Typically 0.75. |
| "Why prime m" | Division method clustering. |
| "Expected longest chain" | Balls-and-bins. |
| "Bloom filter" | Probabilistic, no false negatives. |

---

## 9. Quick Revision

```
HASH TABLE
 h(k): U → [0, m−1]
 load α = n/m

HASH FNS
 division: k mod m (prime m)
 multiplication
 universal (randomized)

COLLISIONS
 chaining: list per slot
   avg O(1+α); α can be > 1
 open addressing: probe
   linear, quadratic, double hashing
   α < 1
   probes ≈ 1/(1−α)

DELETION
 chaining: remove from list
 open addr: tombstone

REHASH at α threshold (~0.75) → 2m

CRYPTO HASHES: SHA-256 for integrity (not tables)

BLOOM FILTER: probabilistic, false positives only

LINEAR PROBING
 successful: ½(1 + 1/(1−α))
 unsuccessful: ½(1 + 1/(1−α)²)

DOUBLE HASHING: h₁(k) + i·h₂(k); gcd(h₂, m) = 1
```
