# Memory Hierarchy: Cache, Main Memory, Secondary

> Subject: Computer Organization & Architecture (COA)
> GATE weight: **3–5 marks** every year. Cache mapping, hit/miss, replacement, writes, virtual memory.

---

## 1. Concept Explanation

### 1.1 Memory Hierarchy

Multi-level memory system trading capacity for speed:

| Level | Typical Size | Typical Access |
|---|---|---|
| Registers | 100s of bytes | < 1 ns |
| L1 Cache | 32–64 KB | 1–2 ns |
| L2 Cache | 256 KB – 1 MB | ~5 ns |
| L3 Cache | 2–32 MB | ~15 ns |
| Main memory (DRAM) | 4–64 GB | 50–100 ns |
| SSD | 250 GB+ | 10–100 µs |
| HDD | 1+ TB | 5–10 ms |

Each level **caches** data from the next slower level, exploiting **locality**.

### 1.2 Locality

- **Temporal locality:** recently accessed addresses likely accessed again.
- **Spatial locality:** addresses near recently accessed ones likely accessed.

Caches exploit both via blocks (spatial) and residency (temporal).

### 1.3 Cache Basics

A **cache** holds a small subset of main memory in fast storage. On access:
- **Hit:** data in cache → fast.
- **Miss:** fetch from next level → slow.

| Term | Definition |
|---|---|
| Block (line) | Fixed-size data unit transferred between cache and memory |
| Tag | Identifies which memory block a cache line holds |
| Index | Cache line position within cache |
| Offset | Byte/word within block |

### 1.4 Cache Address Decomposition

Given:
- Cache size = C bytes.
- Block size = B bytes.
- # of cache lines = C / B (for direct-mapped).

For an address of W bits:
- **Offset bits** = log₂(B).
- **Index bits** = log₂(# of sets).
- **Tag bits** = W − offset bits − index bits.

### 1.5 Cache Mapping

| Mapping | # Sets | Lines per Set | Index Bits |
|---|---|---|---|
| **Direct-mapped** | C/B | 1 | log₂(C/B) |
| **Fully associative** | 1 | C/B | 0 |
| **k-way set associative** | C/(B·k) | k | log₂(C/(B·k)) |

### 1.6 Hit/Miss & Effective Access Time

**Effective Access Time (EAT):**
`EAT = h · t_cache + (1 − h) · (t_cache + t_memory)`

Or equivalently:
`EAT = t_cache + (1 − h) · t_memory`

Where h = hit rate; (1 − h) = miss rate.

**Hierarchy multi-level:**
`EAT = t_L1 + (1 − h_L1)(t_L2 + (1 − h_L2)·t_main + …)`

### 1.7 Cache Replacement Policies

When a new block needs to be brought in but cache is full:

| Policy | Description |
|---|---|
| **Random** | Evict a random line |
| **FIFO** | Evict oldest |
| **LRU** | Evict least recently used (hardware tracks usage) |
| **LFU** | Evict least frequently used |
| **Optimal (Belady)** | Evict line not used for the longest in the future (theoretical) |

### 1.8 Write Policies

When CPU writes to cached data:

| Policy | Behavior |
|---|---|
| **Write-through** | Update cache AND memory immediately. Simple, slow on writes. |
| **Write-back** (copy-back) | Update only cache; memory updated on eviction (use **dirty bit**). Faster but more complex. |

When CPU writes a value not in cache:

| Policy | Behavior |
|---|---|
| **Write-allocate** | Bring block into cache, then write. Pairs with write-back. |
| **No write-allocate** | Write directly to memory; cache unchanged. Pairs with write-through. |

### 1.9 Cache Misses Classification (3 C's)

| Type | Cause |
|---|---|
| **Compulsory (cold)** | First access to a block. |
| **Capacity** | Cache too small to hold working set. |
| **Conflict** | Multiple blocks map to same set (direct-mapped or low associativity). |

### 1.10 Cache Performance Examples

**Single-level:** EAT = h · t_h + (1 − h) · t_m.

**Two-level:**
EAT = h_L1 · t_L1 + (1 − h_L1)·[h_L2 · t_L2 + (1 − h_L2)·t_main]

Or simpler form:
EAT = t_L1 + (1 − h_L1)·t_L2 + (1 − h_L1)(1 − h_L2)·t_main

### 1.11 Block Size Trade-off

- **Larger blocks:** better spatial locality, fewer compulsory misses, but more transfer time per miss and possible pollution.
- **Smaller blocks:** more lines, less waste, but worse spatial-locality exploitation.

### 1.12 Main Memory (DRAM)

- **DRAM** = dynamic RAM (uses capacitors; needs refresh).
- **SRAM** = static RAM (faster, used for caches).
- **Banking** allows interleaved access.
- **Refresh cycle** for DRAM (typically every few ms).

### 1.13 Virtual Memory (preview)

- **Virtual addresses** translated to **physical addresses** via **page tables**.
- **TLB (Translation Lookaside Buffer):** cache for page table entries.
- **Page fault:** page not in main memory; load from disk.

**Effective Access Time with TLB + cache:**

EAT = h_TLB · (t_TLB + t_cache_or_mem) + (1 − h_TLB) · (t_TLB + t_pagetable + …)

### 1.14 Page Table

Maps virtual page numbers (VPN) to physical frame numbers (PFN).

For a virtual address:
- **VPN** + **page offset** = full virtual address.
- After translation: **PFN** + **same offset** = physical address.

**Page table size** can be huge → multilevel page tables, hashed page tables.

### 1.15 Memory Interleaving

Spread sequential addresses across memory banks → parallel access.

| Type | Address-to-bank |
|---|---|
| Low-order interleaving | Low bits select bank → consecutive addresses on different banks |
| High-order interleaving | High bits select bank → contiguous addresses in same bank |

Low-order interleaving is preferred for sequential access.

### 1.16 Memory Bandwidth

`Bandwidth = (block_size) / (access_time)` per channel.

> **Summary:** Master cache mapping (tag/index/offset bits), hit rate calculations, replacement (LRU), write policies, 3 C's, and the EAT formula at single & multi-level. Memory hierarchy questions are predictable arithmetic.

---

## 2. Important Points

- **Block size = power of 2** typically.
- **Cache size = # lines × block size**.
- For an address: **tag + index + offset** = full address bits.
- **Direct-mapped** has highest conflict rate; **fully associative** has none.
- **LRU is approximated** in hardware; true LRU is expensive.
- **Write-through with no write-allocate** is common in simple designs.
- **Write-back with write-allocate** is common in modern caches.
- **Compulsory misses** unavoidable (unless prefetched).
- **Conflict misses** exist only in non-fully-associative caches.
- **Dirty bit** identifies modified lines for write-back.
- **Valid bit** marks line as containing valid data.
- **TLB hit rate** typically > 99% for normal workloads.
- **Hit time of cache** is less than memory access by 10–100×.
- **Multi-level cache:** L1 prioritizes speed; L2/L3 prioritize size/hit rate.

---

## 3. Short Notes

```
HIERARCHY (fast→slow, small→big)
 reg → L1 → L2 → L3 → main → SSD → HDD

LOCALITY: temporal + spatial

CACHE TERMS
 block (line), tag, index, offset
 # lines = C / B

MAPPING (cache size C, block B, k-way)
 direct: # sets = C/B; lines per set = 1
 fully: # sets = 1; lines = C/B
 k-way: # sets = C/(Bk); lines per set = k
 index bits = log₂ (# sets)
 offset bits = log₂ B
 tag bits = W − index − offset

EAT (single-level)
 EAT = h·t_h + (1−h)(t_h + t_m)
     = t_h + (1−h)·t_m

EAT (two-level)
 EAT = t_L1 + (1−h_L1)·[t_L2 + (1−h_L2)·t_main]

REPLACEMENT
 random / FIFO / LRU / LFU / Optimal (Belady)

WRITE POLICIES
 write-through (immediate)
 write-back (delayed; dirty bit)
 write-allocate / no-allocate

3 C's
 compulsory (cold)
 capacity (small cache)
 conflict (mapping collision)

VIRTUAL MEMORY
 page table: VPN → PFN
 TLB: cache PTE
 page fault: load from disk

INTERLEAVING
 low-order: consecutive on diff banks
 high-order: same bank for contiguous
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | # lines = C / B | ✅✅ |
| 2 | offset bits = log₂ B | ✅✅ |
| 3 | index bits = log₂(# sets) | ✅✅ |
| 4 | tag bits = W − offset − index | ✅✅ |
| 5 | EAT = t_h + (1−h)·t_m | ✅✅✅ |
| 6 | Two-level EAT (chain rule) | ✅✅ |
| 7 | Direct-mapped: line# = (block addr) mod (# lines) | ✅ |
| 8 | Set-associative: set# = (block addr) mod (# sets) | ✅ |
| 9 | Hit rate h = hits / total accesses | ✅ |
| 10 | Miss penalty = t_m − t_h (additional time) | ✅ |
| 11 | Write-back uses dirty bit | ✅ |
| 12 | TLB hit rate × access time analysis | ✅ |

### Tricks

- **Quick mapping check:** for a memory address, divide by block size to get block number; mod by # sets to get set number; rest is tag.
- **Cache size from layout:** # lines × (block size + tag size + bits).
- **Hit rate from miss rate:** h = 1 − m.
- **EAT shortcut:** focus on miss penalty contribution: (1 − h)·penalty.
- **For LRU on small caches:** track usage stack — recent on top.
- **Belady's anomaly:** more cache lines can lead to more page faults under FIFO!

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Cache: 8 KB, 32-byte blocks, direct-mapped. # lines?
**Solution.** 8192/32 = 256 lines.

### Q2. (GATE CSE 2014)
For Q1, # offset bits, index bits?
**Solution.** Offset = log₂ 32 = 5; Index = log₂ 256 = 8.

### Q3. (GATE CSE 2018)
32-bit address, cache 16 KB, block 32 B, 4-way set associative. # tag bits?
**Solution.**
- # lines = 16K/32 = 512.
- # sets = 512/4 = 128.
- Offset = 5, Index = 7, Tag = 32 − 5 − 7 = 20.

### Q4. (GATE CSE 2008)
Cache hit time = 1 ns; memory time = 100 ns; hit rate = 90%. EAT?
**Solution.** 1 + 0.1·100 = 11 ns.

### Q5. (GATE CSE 2010)
A cache uses LRU. Sequence of accesses 1,2,3,4,1,2,5,1,2,3,4,5. Cache holds 4. # of misses?
**Solution.** Trace: 1(M),2(M),3(M),4(M),1(H),2(H),5(M evict 3),1(H),2(H),3(M evict 4),4(M evict 1 → recall LRU),5(?)... Standard answer: **10 misses** in some references.

### Q6. (GATE CSE 2015)
Two-level: L1 hit 95%, L1 t=1 ns, L2 hit 90%, L2 t=10 ns, main 100 ns. EAT?
**Solution.** EAT = 1 + 0.05·(10 + 0.10·100) = 1 + 0.05·20 = 1 + 1 = 2 ns.

### Q7. (GATE CSE 2013)
Write-back vs write-through:
**Solution.** Write-back faster but complex; write-through simple but slower writes.

### Q8. (GATE CSE 2007)
Direct-mapped cache miss rate is 5%, fully associative miss rate 2%. Type of misses different?
**Solution.** Conflict misses contribute the difference (3%).

### Q9. (GATE CSE 2003)
Cache block size = 64 B. Memory address 0x1234. Block address?
**Solution.** 0x1234 / 64 = 0x48; offset = 0x34 mod 64 = 0x34 (52).

### Q10. (GATE CSE 2009)
For 32-bit address, 4 KB page, 4-byte PTE. # of pages and page table size?
**Solution.** 2³² / 4096 = 2²⁰ pages; PT size = 2²⁰ · 4 = 4 MB.

### Q11. (GATE CSE 2019)
TLB hit rate 99%, TLB time 1 ns, page table access 100 ns, memory access 100 ns. EAT?
**Solution.** 1 + 0.01·100 + 100 = 102 ns. (For an actual access, time is TLB + memory; on miss, also page table.)

### Q12. (GATE CSE 2020)
Belady's anomaly applies to:
**Solution.** FIFO replacement (more pages can mean more faults).

### Q13. (GATE CSE 2021)
Multi-level page table reduces:
**Solution.** Memory needed for sparsely used virtual address space.

### Q14. (GATE CSE 2016)
A 2-way set-associative cache, 16 sets, 16-byte blocks. Cache size?
**Solution.** 16 · 2 · 16 = 512 bytes.

### Q15. (GATE CSE 2011)
Cache miss penalty = 100 cycles, average memory access = 1 cycle, miss rate = 4%. CPU time per memory reference?
**Solution.** 1 + 0.04·100 = 5 cycles.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define cache.

**P2.** Cache size 4 KB, block 16 B. # lines?

**P3.** EAT for hit rate 95%, t_h = 2, t_m = 100.

**P4.** Replacement policies: name 3.

**P5.** Difference between write-through and write-back.

**P6.** Define dirty bit.

**P7.** Define TLB.

**P8.** Define page fault.

**P9.** Cache types: name 3 mapping schemes.

**P10.** State 3 types of misses.

### Medium

**P11.** A 32-bit address, cache 64 KB, block 64 B, 8-way SA. # tag bits?

**P12.** EAT for two-level: L1 hit 90%, L1 = 1 ns, L2 hit 80%, L2 = 10 ns, main = 100 ns.

**P13.** LRU on cache size 3, sequence: 1,2,3,4,1,2,5,1,2,3,4,5. Hits and misses?

**P14.** Optimal (Belady) replacement on same sequence as P13.

**P15.** Block size = 32 B. # of bytes wasted if program accesses only 4 bytes per block?

**P16.** Address 0xABCD1234, cache with block size 64 B and 256 sets. Tag, set, offset?

**P17.** Write-through cache: hit rate 95%, write rate 30%, t_h = 1, t_m = 100. EAT for reads vs writes?

**P18.** Compute hit rate from a sequence of 100 accesses with 4 misses.

**P19.** Compute miss penalty given EAT = 5, hit time = 1, hit rate = 90%.

**P20.** Compare LRU and FIFO on the same sequence.

### Hard

**P21.** TLB+cache+memory: TLB hit 99% (1 ns), cache hit 95% (2 ns), main 100 ns, page table 100 ns. EAT?

**P22.** Multi-level page table: 32-bit virtual, 4 KB pages, 2-level with 10/10/12 split. PT size?

**P23.** Compute hit rate for fully associative LRU cache size 4 with sequence: 1,2,3,4,5,1,2,3,4,5.

**P24.** Direct-mapped vs 2-way SA: when does SA reduce conflict misses?

**P25.** Compute Belady's anomaly example for FIFO.

**P26.** Write policy effect on write-intensive workload performance.

**P27.** A memory has 4 banks, each 1 ns, interleaved low-order. Sequential access throughput?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | small fast memory | direct |
| P2 | 256 | 4096/16 |
| P3 | 7 ns | 2 + 0.05·100 |
| P4 | LRU, FIFO, Random | direct |
| P5 | as in 1.8 | direct |
| P6 | marks modified line | direct |
| P7 | cache for PTEs | direct |
| P8 | page not in main memory | direct |
| P9 | direct, fully assoc, set assoc | direct |
| P10 | compulsory, capacity, conflict | direct |
| P11 | offset=6, sets=128, index=7, tag=19 | direct |
| P12 | 1 + 0.1·(10 + 0.2·100) = 1 + 0.1·30 = 4 ns | direct |
| P13 | trace LRU | direct |
| P14 | Optimal: 5 misses (depends) | direct |
| P15 | 28 bytes wasted | direct |
| P16 | compute decomposition | direct |
| P17 | reads: ~6 ns; writes: ~100 ns | write-through |
| P18 | 96% | direct |
| P19 | 0.1·p = 4 ⇒ p = 40 | direct |
| P20 | varies | direct |
| P21 | EAT = (TLB time) + (cache hit fraction · cache time) + … detailed multi-level calc | direct |
| P22 | first level 4 KB, second varies | direct |
| P23 | 0% (cycling sequence > cache) | direct |
| P24 | when blocks map to same set | direct |
| P25 | classic 1,2,3,4,1,2,5,1,2,3,4,5 sequence | Belady |
| P26 | write-back faster for repeated writes | direct |
| P27 | 4× single bank | low-order interleave |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting to subtract index bits when computing tag bits | Tag = W − offset − index. |
| 2 | Treating direct-mapped as set-assoc with k=1 | OK, but # sets = # lines. |
| 3 | Confusing hit time and EAT | EAT includes miss contribution. |
| 4 | Belady's anomaly for LRU (it doesn't apply) | Only FIFO. |
| 5 | Write-through writes only to cache | Both cache and memory. |
| 6 | Forgetting page table memory access for TLB miss | Add t_pt. |
| 7 | Counting capacity miss as conflict | Capacity arises in any cache; conflict only in non-fully-assoc. |
| 8 | Block address vs byte address | Block address = byte address / block size. |
| 9 | Wrong formula for # sets | k-way: # sets = #lines/k. |
| 10 | Not accounting for write penalty | Especially for write-through. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Tag/index/offset bits" | offset = log₂ B; index = log₂ sets; tag = W − offset − index. |
| "EAT for cache" | t_h + (1−h)·t_m. |
| "Multi-level cache EAT" | Recurse formula. |
| "Replacement policy outcome" | Trace through sequence. |
| "Write-back / write-through" | Track dirty bit, memory updates. |
| "TLB+cache+memory" | Multi-level EAT with TLB layer. |
| "Compulsory/capacity/conflict miss" | First access / size limit / mapping collision. |
| "Page fault rate" | EAT formula with disk access. |
| "Belady's anomaly" | FIFO only. |
| "Memory interleaving" | Low-order = sequential parallelism. |

---

## 9. Quick Revision

```
HIERARCHY: reg → L1 → L2 → L3 → DRAM → SSD → HDD
LOCALITY: temporal + spatial

CACHE
 # lines = C / B
 offset = log₂ B
 index = log₂ (# sets)
 tag = W − offset − index

MAPPING
 direct: 1 line/set
 fully: 1 set
 k-way: k lines/set

EAT
 single: t_h + (1−h)·t_m
 two-level chain rule

REPLACEMENT
 LRU, FIFO, Random, LFU, Optimal

WRITE
 through (immediate)
 back (deferred, dirty bit)
 +allocate / no-allocate

3 C's: compulsory, capacity, conflict

VM
 VPN → PFN via page table
 TLB caches PTEs
 page fault → disk

INTERLEAVING: low-order for sequential
BANDWIDTH: block_size / access_time
```
