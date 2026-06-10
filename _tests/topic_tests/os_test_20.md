# Topic Test 20 — OS (Memory · File Systems & Disk · I/O & Protection)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] In paging, page size = 4 KB. Offset bits:
(A) 4  (B) 8  (C) 12  (D) 16

**Q2.** [NAT] # virtual pages for 32-bit VA, 4 KB pages = 2^`____`

**Q3.** [MCQ] Belady's anomaly applies to:
(A) LRU  (B) OPT  (C) FIFO  (D) Clock

**Q4.** [MCQ] Optimal page replacement evicts:
(A) Oldest  (B) LRU  (C) Used furthest in future  (D) Random

**Q5.** [MCQ] TLB caches:
(A) Memory blocks  (B) Page table entries  (C) File data  (D) Disk sectors

**Q6.** [MCQ] Demand paging loads:
(A) Whole program  (B) On first access  (C) Eagerly  (D) Never

**Q7.** [MCQ] Disk access components:
(A) Seek + transfer  (B) Seek + rotation + transfer  (C) Rotation only  (D) Seek only

**Q8.** [NAT] Avg rotational latency for 7200 RPM (in ms) = `____` (round to 2 decimals)

**Q9.** [MCQ] SSTF scheduling problem:
(A) Slow  (B) Starvation  (C) Convoy  (D) Deadlock

**Q10.** [MCQ] Unix inode contains:
(A) File data  (B) Metadata + pointers  (C) Directory  (D) None

**Q11.** [MCQ] RAID 5 fault tolerance:
(A) 0 disks  (B) 1 disk  (C) 2 disks  (D) All disks

**Q12.** [MCQ] DMA transfer:
(A) Always uses CPU  (B) Doesn't use CPU for bulk  (C) Slower than polling  (D) Always polled

**Q13.** [MCQ] User vs kernel mode bit:
(A) Process state  (B) Memory protection  (C) Privilege level  (D) Page table flag

**Q14.** [MCQ] ACL stands for:
(A) Access Control List  (B) Address Capability List  (C) Application Code Library  (D) None

**Q15.** [MCQ] Symmetric crypto example:
(A) RSA  (B) AES  (C) ECC  (D) DSA

---

## Section B — 2 marks each

**Q16.** [MCQ] Reference string 1,2,3,4,1,2,5,1,2,3,4,5; 3 frames; FIFO. Page faults?
(A) 7  (B) 8  (C) 9  (D) 10

**Q17.** [NAT] EAT for ma=100ns, p=0.001, fault time=10ms = `____` ns (closest integer)

**Q18.** [MCQ] Disk scheduling: requests {98, 183, 37, 122, 14, 124, 65, 67}, head=53, FCFS total head movement:
(A) 640  (B) 232  (C) 224  (D) 408

**Q19.** [MCQ] LOOK vs SCAN difference:
(A) LOOK reverses at last request  (B) SCAN reverses at last request  (C) Same algorithm  (D) Random

**Q20.** [MCQ] Capability list is:
(A) Per-object  (B) Per-subject  (C) Per-file  (D) Centralized

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (C) 12 | log₂ 4096 |
| 2 | 20 | 32 − 12 |
| 3 | (C) | direct |
| 4 | (C) | direct |
| 5 | (B) | direct |
| 6 | (B) | direct |
| 7 | (B) | direct |
| 8 | 4.17 | 0.5·60/7200·1000 |
| 9 | (B) | direct |
| 10 | (B) | direct |
| 11 | (B) | direct |
| 12 | (B) | direct |
| 13 | (C) | direct |
| 14 | (A) | direct |
| 15 | (B) | direct |
| 16 | (C) 9 | trace FIFO |
| 17 | 10100 | 100·0.999 + 10000000·0.001 ≈ 10099.9 ≈ 10100 |
| 18 | (A) 640 | sum |Δ| as in classic problem |
| 19 | (A) | direct |
| 20 | (B) | direct |

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
