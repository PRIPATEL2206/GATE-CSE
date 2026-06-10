# Topic Test 22 — DBMS (Normalization · Transactions/Concurrency · Indexing)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] FD trivial means:
(A) X → Y where Y ⊆ X  (B) X → Y where Y ⊄ X  (C) X = Y  (D) None

**Q2.** [MCQ] Armstrong's axioms (3 basic):
(A) Reflexivity, Augmentation, Transitivity  (B) Union, Decomposition, Pseudo  (C) Both  (D) Neither

**Q3.** [MCQ] BCNF condition:
(A) Every FD has prime LHS  (B) Every FD X → Y has X super key  (C) No partial dep  (D) No transitive dep

**Q4.** [MCQ] 3NF allows transitive dep iff:
(A) RHS is prime  (B) LHS is super key  (C) Always  (D) Never

**Q5.** [MCQ] Lossless decomposition condition:
(A) Common attr is super key in one fragment  (B) All FDs preserved  (C) Both  (D) Neither

**Q6.** [MCQ] ACID property of "all or nothing":
(A) Atomicity  (B) Consistency  (C) Isolation  (D) Durability

**Q7.** [MCQ] Conflict serializable iff:
(A) All schedules equal  (B) Precedence graph acyclic  (C) Two-phase locking used  (D) Strict 2PL

**Q8.** [MCQ] 2PL phases:
(A) Acquire then release  (B) Release then acquire  (C) Random  (D) None

**Q9.** [MCQ] Strict 2PL prevents:
(A) Deadlocks  (B) Cascading aborts  (C) All anomalies  (D) Phantom reads

**Q10.** [MCQ] WAL rule:
(A) Log after data write  (B) Log before data write  (C) Both same time  (D) No log

**Q11.** [MCQ] UNDO operation:
(A) Re-apply committed  (B) Roll back uncommitted  (C) Backup  (D) Restore

**Q12.** [MCQ] B+ tree data location:
(A) All nodes  (B) Leaves only  (C) Internal only  (D) Root only

**Q13.** [MCQ] Hash index drawback:
(A) Slow point query  (B) No range queries  (C) High disk usage  (D) Complex implementation

**Q14.** [MCQ] Bitmap index ideal for:
(A) High cardinality  (B) Low cardinality  (C) Text search  (D) Geographic

**Q15.** [MCQ] Primary index is:
(A) Clustered  (B) Non-clustered  (C) Both  (D) Neither

---

## Section B — 2 marks each

**Q16.** [NAT] Closure of {A} given F = {A → B, B → C, AB → D}: result attributes = `____` (count)

**Q17.** [MCQ] Strict 2PL holds X-locks until:
(A) Transaction starts  (B) Operation completes  (C) Transaction commits  (D) Random

**Q18.** [MCQ] B+ tree height for n = 10⁹ records, fanout 100:
(A) 2  (B) 4  (C) 5  (D) 9

**Q19.** [MCQ] Phantom read can occur in:
(A) Read uncommitted  (B) Read committed  (C) Repeatable read  (D) All except serializable

**Q20.** [MCQ] BCNF vs 3NF dependency preservation:
(A) Both preserve  (B) BCNF preserves but not 3NF  (C) 3NF preserves but BCNF may not  (D) Neither

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (A) | direct |
| 2 | (A) | direct |
| 3 | (B) | direct |
| 4 | (A) | direct |
| 5 | (A) | direct |
| 6 | (A) | direct |
| 7 | (B) | direct |
| 8 | (A) | growing then shrinking |
| 9 | (B) | direct |
| 10 | (B) | direct |
| 11 | (B) | direct |
| 12 | (B) | direct |
| 13 | (B) | direct |
| 14 | (B) | direct |
| 15 | (A) | direct |
| 16 | 4 | A,B,C,D |
| 17 | (C) | direct |
| 18 | (C) 5 | log_50(10⁹) ≈ 5 |
| 19 | (D) | direct |
| 20 | (C) | direct |

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
