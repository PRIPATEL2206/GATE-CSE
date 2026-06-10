# File Systems & Disk Scheduling

> Subject: Operating Systems
> GATE weight: **2–3 marks** every year. File allocation, directory structure, disk scheduling algorithms.

---

## 1. Concept Explanation

### 1.1 File

Named, persistent collection of related data on storage. OS provides abstraction over hardware.

**File attributes:**
- Name, identifier (inode #), type.
- Location (disk address).
- Size, owner, permissions, timestamps.

### 1.2 File Operations

Create, write, read, reposition (seek), delete, truncate, open, close.

### 1.3 File Access Methods

| Method | Description |
|---|---|
| **Sequential** | Read in order |
| **Direct (random)** | Read any block |
| **Indexed** | Index block points to data blocks |

### 1.4 Directory Structure

| Type | Description |
|---|---|
| **Single-level** | All files in one directory |
| **Two-level** | Per-user directory |
| **Tree** | Hierarchical (Unix, Windows) |
| **Acyclic graph** | Allows sharing via links |
| **General graph** | Cycles possible (need ref counting) |

### 1.5 File Allocation Methods

| Method | Description |
|---|---|
| **Contiguous** | Consecutive blocks; fast sequential, suffers fragmentation |
| **Linked** | Each block has pointer to next; no random access |
| **Indexed** | Index block holds pointers to all data blocks |
| **Multi-level indexed** | Index blocks chain for large files |
| **Combined (Unix inode)** | Direct + single + double + triple indirect |

### 1.6 Unix Inode Structure

```
| Direct pointers (12)     |
| Single indirect          |  → block of pointers
| Double indirect          |  → block of single indirects
| Triple indirect          |  → block of double indirects
```

For 4 KB blocks, 4-byte pointers (1024 ptrs/block):
- Direct: 12 × 4 KB = 48 KB.
- Single indirect: 1024 × 4 KB = 4 MB.
- Double: 1024² × 4 KB = 4 GB.
- Triple: 1024³ × 4 KB = 4 TB.

### 1.7 Free Space Management

| Method | Description |
|---|---|
| **Bit map** | One bit per block (free/used) |
| **Linked list** | Free blocks chained |
| **Grouping** | First free block holds addresses of next n |
| **Counting** | Track free contiguous runs |

### 1.8 File System Layers

```
Application
    │
File interface (open/read/write)
    │
File-organization module
    │
Logical file system (metadata, security)
    │
Block-level (buffer cache)
    │
Device driver
    │
Storage device
```

### 1.9 Disk Structure

- **Tracks:** concentric circles.
- **Sectors:** divisions of tracks.
- **Cylinders:** same track on all platters.
- **Blocks:** OS-level unit (group of sectors).

### 1.10 Disk Access Time

```
Total = seek time + rotational latency + transfer time
```

| Component | Description |
|---|---|
| Seek | Move head to track (5–10 ms) |
| Rotational latency | Sector rotates under head (avg = 0.5 / RPM) |
| Transfer | Read/write data |

### 1.11 Disk Scheduling Algorithms

| Algorithm | Description |
|---|---|
| **FCFS** | First come, first served |
| **SSTF** | Shortest seek time first |
| **SCAN (elevator)** | Move one direction, reverse at end |
| **C-SCAN** | One direction; jump back to start |
| **LOOK** | SCAN but reverse at last request |
| **C-LOOK** | C-SCAN but jump back to first request |

### 1.12 Disk Scheduling Examples

**Request queue:** 98, 183, 37, 122, 14, 124, 65, 67. Head at 53.

**FCFS:** 53→98→183→37→122→14→124→65→67. Total head movement: |53−98|+...

**SSTF:** at each step, pick closest. Greedy.

**SCAN:** moves one direction, e.g., toward end then reverses.

### 1.13 RAID

| Level | Description |
|---|---|
| **RAID 0** | Striping; no redundancy; speed |
| **RAID 1** | Mirroring; full redundancy |
| **RAID 2** | Bit-level Hamming; rare |
| **RAID 3** | Byte-level parity |
| **RAID 4** | Block-level parity (single parity disk) |
| **RAID 5** | Block-level distributed parity |
| **RAID 6** | Double distributed parity |
| **RAID 10 (1+0)** | Mirror + stripe |

### 1.14 Buffer Cache

OS caches recent disk blocks in memory. Reduces I/O.

**Write strategies:**
- **Write-through:** immediate.
- **Write-back:** lazy.

### 1.15 Journaling

File system writes log of changes before applying. Recovery via replay.
**Examples:** ext3, ext4, NTFS.

### 1.16 Mounting

Attach a file system to a directory in another file system.

### 1.17 File System Types

| Type | OS |
|---|---|
| FAT, exFAT | Older Windows / removable |
| NTFS | Modern Windows |
| ext3 / ext4 | Linux |
| HFS+ / APFS | macOS |
| ZFS | Solaris / FreeBSD |

### 1.18 Disk Performance Calculations

For 7200 RPM disk:
- Avg rotational latency = 0.5 · (60/7200) s = 4.17 ms.
- Avg seek = ~10 ms.
- Total avg ≈ 14 ms + transfer.

> **Summary:** File systems organize, name, and protect data. Allocation (contiguous/linked/indexed). Disk access = seek + rotation + transfer. Scheduling: FCFS / SSTF / SCAN / C-SCAN / LOOK. RAID levels for redundancy.

---

## 2. Important Points

- **Inode** = file metadata + pointers.
- **Unix inode** combines direct + indirect pointers.
- **Bit map** for free space is space-efficient and fast.
- **Disk access** has 3 components.
- **SSTF** can starve far requests.
- **SCAN/LOOK** prevents starvation.
- **RAID 5** common for performance + 1-disk fault tolerance.
- **RAID 6** tolerates 2-disk failure.
- **Mirroring** doubles read speed but halves usable capacity.
- **Striping** splits across disks.
- **Journaling** ensures consistency on crash.
- **Buffer cache** reduces disk I/O.
- **Avg rotational latency** = 0.5 / (RPM/60).

---

## 3. Short Notes

```
FILE: named persistent data collection
ATTRIBUTES: name, type, location, size, perm, timestamps

OPERATIONS: create, read, write, seek, delete, truncate, open, close

ACCESS METHODS
 sequential, direct, indexed

DIRECTORY
 single, two-level, tree, acyclic graph, general

ALLOCATION
 contiguous, linked, indexed (single/multi/Unix)

UNIX INODE
 direct (12), single, double, triple indirect

FREE SPACE
 bit map / linked list / grouping / counting

DISK STRUCTURE
 platter / track / sector / cylinder / block

DISK ACCESS = seek + rotation + transfer
 avg rotation = 0.5 · 60 / RPM

DISK SCHEDULING
 FCFS, SSTF, SCAN, C-SCAN, LOOK, C-LOOK

RAID
 0: stripe (no redundancy)
 1: mirror
 5: distributed parity (1-fault tolerant)
 6: double parity (2-fault)
 10: mirror + stripe

BUFFER CACHE
 write-through / write-back

JOURNALING for crash recovery
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Disk access = seek + rotation + transfer | ✅✅✅ |
| 2 | Avg rotation = 0.5 · (60 / RPM) | ✅✅ |
| 3 | Unix inode: 12 direct + 1 single + 1 double + 1 triple | ✅✅ |
| 4 | RAID 0 = stripe; 1 = mirror; 5 = distributed parity; 6 = double | ✅✅ |
| 5 | SCAN prevents starvation (vs SSTF) | ✅ |
| 6 | LOOK reverses at last request | ✅ |
| 7 | Bit map free-space efficient | ✅ |
| 8 | Avg seek time depends on disk | ✅ |
| 9 | Direct access for indexed allocation | ✅ |
| 10 | Mounting attaches FS | ✅ |

### Tricks

- **For inode capacity:** sum direct + each level.
- **For disk scheduling problems:** trace head movement step by step.
- **For RAID capacity:** RAID 0 = sum; RAID 1 = half; RAID 5 = (n−1)/n.
- **For latency calculations:** avg = total/2 typically.
- **C-SCAN treats disk as circular** — uniform wait.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Inode in Unix has:
**Solution.** 12 direct + 1 single + 1 double + 1 triple indirect.

### Q2. (GATE CSE 2014)
Disk access components:
**Solution.** Seek + rotational latency + transfer.

### Q3. (GATE CSE 2018)
SSTF problem:
**Solution.** Starvation of far requests.

### Q4. (GATE CSE 2008)
RAID 5 fault tolerance:
**Solution.** 1 disk failure.

### Q5. (GATE CSE 2010)
Avg rotational latency for 7200 RPM:
**Solution.** 0.5 · (60/7200) s = 4.17 ms.

### Q6. (GATE CSE 2015)
Bitmap for free space management:
**Solution.** 1 bit per block.

### Q7. (GATE CSE 2013)
SCAN scheduling:
**Solution.** Elevator: one direction, reverse at end.

### Q8. (GATE CSE 2007)
File allocation methods:
**Solution.** Contiguous, linked, indexed.

### Q9. (GATE CSE 2003)
Indexed allocation advantage:
**Solution.** Direct access; no fragmentation.

### Q10. (GATE CSE 2009)
Unix inode max file size with 4 KB blocks, 4-byte pointers:
**Solution.** ≈ direct (48 KB) + single (4 MB) + double (4 GB) + triple (4 TB) ≈ 4 TB.

### Q11. (GATE CSE 2019)
RAID 1 advantage:
**Solution.** Full mirror; reads can be parallel.

### Q12. (GATE CSE 2020)
C-SCAN over SCAN:
**Solution.** Uniform wait time.

### Q13. (GATE CSE 2021)
Journaling FS purpose:
**Solution.** Recovery from crashes.

### Q14. (GATE CSE 2016)
LOOK vs SCAN:
**Solution.** LOOK reverses at last request.

### Q15. (GATE CSE 2011)
Disk scheduling: FCFS request queue 95, 180, 34, 119, 11, 123, 62, 64. Head at 50. Total movement?
**Solution.** Sum of |head transitions|. 45+85+146+85+108+112+61+2 = 644 (varies).

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define file.

**P2.** Inode contents.

**P3.** Unix inode pointer types.

**P4.** Disk access components.

**P5.** SSTF disadvantage.

**P6.** SCAN scheduling.

**P7.** RAID 0 vs RAID 1.

**P8.** RAID 5 fault tolerance.

**P9.** Avg rotational latency formula.

**P10.** Bitmap usage.

### Medium

**P11.** Compute total head movement for FCFS: queue 100, 50, 200, 25, 175 with head at 75.

**P12.** Apply SSTF to same.

**P13.** Apply SCAN (toward 0) to same.

**P14.** Apply C-SCAN.

**P15.** Apply LOOK.

**P16.** Compute Unix inode max file size with 4 KB blocks.

**P17.** RAID capacity for 4-disk RAID 5 with 1 TB drives.

**P18.** Average rotational latency for 5400 RPM.

**P19.** Free space bitmap size for 1 TB / 4 KB blocks.

**P20.** Tree directory vs acyclic.

### Hard

**P21.** Compare disk scheduling algorithms on same queue.

**P22.** Calculate rotational + seek + transfer time.

**P23.** RAID 6 parity calculation.

**P24.** Buffer cache write-through vs write-back.

**P25.** Journaling implementation steps.

**P26.** Multi-level indexing capacity calculation.

**P27.** File system mount semantics.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | named persistent data | direct |
| P2 | metadata + pointers | direct |
| P3 | direct, single, double, triple | direct |
| P4 | seek + rotation + transfer | direct |
| P5 | starvation | direct |
| P6 | elevator | direct |
| P7 | stripe vs mirror | direct |
| P8 | 1 disk | direct |
| P9 | 0.5 · 60 / RPM | direct |
| P10 | 1 bit per block | direct |
| P11 | trace | direct |
| P12 | trace | direct |
| P13 | trace | direct |
| P14 | trace | direct |
| P15 | trace | direct |
| P16 | as in 1.6 | direct |
| P17 | (n−1)/n · total = 3 TB | direct |
| P18 | 5.56 ms | direct |
| P19 | 2³⁰ bits = 128 MB | direct |
| P20 | acyclic allows sharing via links | direct |
| P21 | trace each | direct |
| P22 | sum components | direct |
| P23 | XOR + Reed-Solomon | direct |
| P24 | as in 1.14 | direct |
| P25 | log + apply + replay | direct |
| P26 | sum levels | direct |
| P27 | attach to directory | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Inode has data (myth) | Inode has metadata + pointers. |
| 2 | Avg rotation = full rotation | Half rotation. |
| 3 | RAID 0 fault tolerant | No redundancy. |
| 4 | SSTF optimal | Causes starvation. |
| 5 | Linked allocation random access | No, sequential only. |
| 6 | Contiguous = no fragmentation | External fragmentation possible. |
| 7 | Bit map slow | Actually fast for typical sizes. |
| 8 | RAID 5 = 2 disk fault tolerant | 1 disk only. |
| 9 | LOOK = SCAN | LOOK reverses earlier. |
| 10 | Buffer cache always write-through | Often write-back. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Disk access time" | Sum 3 components. |
| "Inode max file size" | Sum direct + indirect levels. |
| "Disk scheduling head movement" | Trace + sum |Δ|. |
| "RAID redundancy" | Level-specific. |
| "Avg rotational latency" | Half a full rotation. |
| "Bitmap free space" | 1 bit per block. |
| "Acyclic vs general directory" | Cycles allowed? |
| "Journaling" | Crash recovery via log. |
| "Linked allocation random" | Slow. |
| "Indexed allocation random" | Direct. |

---

## 9. Quick Revision

```
FILE: name, type, location, size, perm, timestamps
OPERATIONS: open, read, write, seek, close, delete

ACCESS: sequential / direct / indexed
DIRECTORY: tree / acyclic graph (most common)

ALLOCATION
 contiguous / linked / indexed
 Unix inode: 12 direct + single + double + triple

FREE SPACE
 bit map / linked / grouping / counting

DISK
 seek + rotation + transfer
 avg rotation = 0.5 · 60 / RPM

DISK SCHEDULING
 FCFS, SSTF (starvation), SCAN, C-SCAN, LOOK, C-LOOK

RAID
 0 stripe; 1 mirror
 5 distributed parity (1-fault)
 6 double parity (2-fault)
 10 mirror+stripe

BUFFER CACHE: write-through / write-back
JOURNALING: log-based recovery

MOUNTING: attach FS

INODE CAPACITY = sum of direct + indirect levels
```
