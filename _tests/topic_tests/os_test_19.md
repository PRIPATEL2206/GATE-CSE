# Topic Test 19 — OS (Processes/Threads/Scheduling · Synchronization & Deadlocks)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] TAT formula:
(A) Burst − Arrival  (B) Completion − Arrival  (C) Burst + Wait  (D) Wait − Burst

**Q2.** [MCQ] WT (non-preemptive) formula:
(A) Completion − Burst  (B) TAT − Burst  (C) Completion − Arrival  (D) Burst

**Q3.** [MCQ] Optimal avg WT (non-preemptive):
(A) FCFS  (B) SJF  (C) RR  (D) Priority

**Q4.** [MCQ] Convoy effect occurs in:
(A) FCFS  (B) SJF  (C) SRTF  (D) RR

**Q5.** [MCQ] Round Robin requires:
(A) Static priority  (B) Time quantum  (C) Burst time known  (D) Aging

**Q6.** [MCQ] Process state when waiting for I/O:
(A) Ready  (B) Running  (C) Waiting/Blocked  (D) Terminated

**Q7.** [MCQ] PCB does NOT store:
(A) PC  (B) State  (C) Open files  (D) Source code

**Q8.** [MCQ] Threads share with peers:
(A) Stack  (B) Memory (heap, code)  (C) Registers  (D) PCB

**Q9.** [MCQ] Aging combats:
(A) Convoy effect  (B) Starvation  (C) Deadlock  (D) Priority inversion

**Q10.** [MCQ] Coffman conditions count:
(A) 2  (B) 3  (C) 4  (D) 5

**Q11.** [MCQ] Single-instance RAG cycle:
(A) Implies deadlock  (B) May be deadlock  (C) Safe always  (D) None

**Q12.** [MCQ] Banker's algorithm purpose:
(A) Detect deadlock  (B) Avoid deadlock  (C) Recover  (D) Prevent

**Q13.** [MCQ] Producer-consumer needs:
(A) 1 semaphore  (B) 2 semaphores  (C) 3 semaphores  (D) None

**Q14.** [MCQ] Mutex has:
(A) Counter  (B) Ownership  (C) No ownership  (D) FIFO queue only

**Q15.** [MCQ] Priority inversion fix:
(A) Aging  (B) Priority inheritance  (C) Banker's  (D) Round robin

---

## Section B — 2 marks each

**Q16.** [MCQ] FCFS for P1(0,5), P2(1,3), P3(2,8). Avg WT?
(A) 3  (B) 4.33  (C) 6  (D) 0

**Q17.** [NAT] SRTF for P1(0,5), P2(1,3), P3(2,8). Avg WT = `____`

**Q18.** [MCQ] Producer-consumer: 3 semaphores typically initialized to:
(A) (1, 0, N)  (B) (0, 0, 0)  (C) (1, 1, 1)  (D) (N, N, N)

**Q19.** [MCQ] Deadlock prevention by enforcing:
(A) Random order  (B) Total resource ordering  (C) Aging  (D) RR

**Q20.** [MCQ] Dining philosophers naive solution causes:
(A) Starvation only  (B) Deadlock  (C) Live lock  (D) No problem

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | direct |
| 2 | (B) | direct |
| 3 | (B) | direct |
| 4 | (A) | direct |
| 5 | (B) | direct |
| 6 | (C) | direct |
| 7 | (D) | code is in text segment |
| 8 | (B) | shared heap, code, files |
| 9 | (B) | direct |
| 10 | (C) 4 | direct |
| 11 | (A) | direct |
| 12 | (B) | direct |
| 13 | (C) 3 | mutex + empty + full |
| 14 | (B) | direct |
| 15 | (B) | direct |
| 16 | (B) 4.33 | (0+4+6)/3 |
| 17 | 3 | trace SRTF |
| 18 | (A) | mutex=1, full=0, empty=N |
| 19 | (B) | direct |
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
- < 18 → re-do PYQs of both topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
