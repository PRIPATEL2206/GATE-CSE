# Synchronization & Deadlocks

> Subject: Operating Systems
> GATE weight: **3–5 marks** every year. Mutual exclusion, semaphores, deadlock conditions/avoidance/detection, classic problems.

---

## 1. Concept Explanation

### 1.1 Race Conditions

When multiple processes access shared data concurrently and outcome depends on order of execution.

**Example:** two threads incrementing shared `count`:
```
load → increment → store
```
If interleaved, increments may be lost.

### 1.2 Critical Section

Code accessing shared data. Must satisfy:
1. **Mutual exclusion:** only one process inside.
2. **Progress:** if no process inside, others must enter.
3. **Bounded waiting:** finite waiting time before entry.

### 1.3 Solutions

**Software:**
- Peterson's algorithm (2 processes).
- Bakery algorithm (n processes).

**Hardware:**
- Disable interrupts (single CPU only).
- Test-and-set, compare-and-swap (atomic).

**OS-level:**
- Semaphores, mutexes, condition variables, monitors.

### 1.4 Peterson's Algorithm (2 processes)

```
flag[i] = true;
turn = j;
while (flag[j] && turn == j);   // wait
// critical section
flag[i] = false;
```

Satisfies all 3 conditions for 2 processes.

### 1.5 Test-and-Set (TAS)

Atomic instruction:
```
bool TAS(bool *lock):
  old = *lock
  *lock = true
  return old
```

**Spinlock:**
```
while (TAS(&lock));     // busy wait
// critical section
lock = false;
```

### 1.6 Compare-and-Swap (CAS)

```
bool CAS(int *p, int old, int new):
  if (*p == old) { *p = new; return true; }
  return false;
```

Used in lock-free data structures.

### 1.7 Semaphores

Integer variable with two atomic operations:
- **wait(S) / P(S):**
```
while (S <= 0); S--;
```
- **signal(S) / V(S):**
```
S++;
```

Modern semaphores **block** rather than busy-wait.

### 1.8 Binary vs Counting Semaphore

- **Binary semaphore:** value 0 or 1 (mutex).
- **Counting semaphore:** integer ≥ 0.

### 1.9 Mutex

Lightweight binary semaphore for mutual exclusion. Has **ownership** (only locker can unlock).

### 1.10 Producer-Consumer Problem

Buffer of size n. Producers add items; consumers remove.

**Solution with semaphores:**
- `mutex` = 1 (mutual exclusion).
- `empty` = n (empty slots).
- `full` = 0 (full slots).

Producer:
```
wait(empty); wait(mutex);
add item; signal(mutex); signal(full);
```

Consumer:
```
wait(full); wait(mutex);
remove; signal(mutex); signal(empty);
```

### 1.11 Readers-Writers Problem

Multiple readers can read; only one writer at a time.

**First readers-writers (readers preference):**
```
mutex (over rcount), wrt (writer access)

Reader:
wait(mutex); rcount++; if (rcount==1) wait(wrt); signal(mutex);
read; wait(mutex); rcount--; if (rcount==0) signal(wrt); signal(mutex);

Writer:
wait(wrt); write; signal(wrt);
```

**Issue:** writers may starve.

### 1.12 Dining Philosophers

5 philosophers, 5 forks. Each needs 2 forks to eat.

**Naive deadlock:** all pick left → wait for right.

**Solutions:**
- At most n−1 in dining room.
- One picks right first.
- Resource hierarchy.
- Monitor-based.

### 1.13 Monitors

High-level synchronization construct.
- Procedures with mutual exclusion.
- **Condition variables:** wait, signal.

```
monitor X {
  shared data;
  procedure m() { ... }
  condition c;
  wait(c); / signal(c);
}
```

### 1.14 Deadlock Definition

A set of processes where each is waiting for an event only another in the set can cause.

### 1.15 Necessary Conditions (Coffman)

1. **Mutual exclusion:** resources non-shareable.
2. **Hold and wait:** holds resources while waiting for others.
3. **No preemption:** resources released only voluntarily.
4. **Circular wait:** chain of waiting processes.

All 4 must hold for deadlock.

### 1.16 Deadlock Strategies

| Strategy | Description |
|---|---|
| **Prevention** | Ensure ≥ 1 condition cannot hold |
| **Avoidance** | Use info to avoid unsafe states |
| **Detection** | Allow; check periodically |
| **Recovery** | Kill or rollback |
| **Ignore** | Reboot if it happens (Ostrich algorithm) |

### 1.17 Deadlock Prevention

| Condition broken | How |
|---|---|
| Mutual exclusion | Make resources shareable (not always possible) |
| Hold and wait | Acquire all at once, or none held when requesting |
| No preemption | Allow preemption |
| Circular wait | Total ordering of resources |

### 1.18 Deadlock Avoidance — Banker's Algorithm

Each process declares max needs. System grants only if **safe state** results.

**Safe state:** there exists an ordering of processes such that all can complete.

**Banker's:** simulate granting; check if a safe sequence exists.

**Time complexity:** O(m·n²) where m = resources, n = processes.

### 1.19 Resource Allocation Graph (RAG)

Nodes: processes (circles), resources (squares).
Edges: request, assignment.

**Single instance per resource:** cycle ⇔ deadlock.
**Multiple instances:** cycle is necessary but not sufficient for deadlock.

### 1.20 Deadlock Detection

For multi-instance: use Banker-like algorithm. For single-instance: detect cycle in RAG.

### 1.21 Deadlock Recovery

- **Process termination:** kill all in deadlock or kill one at a time.
- **Resource preemption:** snatch resources.
- **Rollback:** restart from checkpoint.

### 1.22 Starvation vs Deadlock

| Term | Description |
|---|---|
| **Deadlock** | All blocked, no progress |
| **Starvation** | Specific process indefinitely waits |
| **Livelock** | Processes change state but no progress |

### 1.23 Priority Inversion

High-priority process indirectly blocked by lower priority holding shared resource. Fix: **priority inheritance**.

> **Summary:** Synchronization solves race conditions via mutual exclusion. Semaphores, mutexes, monitors. Deadlock = 4 Coffman conditions; handle via prevention/avoidance/detection. Banker's algorithm for safe state.

---

## 2. Important Points

- **Critical section** must be mutually exclusive.
- **Peterson's** works for 2 processes; needs atomic loads/stores.
- **TAS / CAS** are atomic primitives.
- **Counting semaphore** initialized to # available resources.
- **Producer-consumer:** mutex + empty + full.
- **Readers-writers:** can favor readers or writers.
- **Dining philosophers:** classic deadlock if naive.
- **Monitors** are higher-level synchronization.
- **Deadlock** needs all 4 Coffman conditions.
- **Banker's algorithm** detects unsafe states.
- **Single-instance:** RAG cycle ⇔ deadlock.
- **Multi-instance:** cycle necessary, not sufficient.
- **Deadlock prevention** breaks at least one condition.
- **Starvation** ≠ deadlock; processes still running, but some never get resource.
- **Livelock:** active but no progress.
- **Priority inversion** fixed via priority inheritance.

---

## 3. Short Notes

```
RACE CONDITION
 shared data, unsynchronized access

CRITICAL SECTION req's
 mutual exclusion, progress, bounded waiting

SOLUTIONS
 software: Peterson, Bakery
 hardware: disable interrupts, TAS, CAS
 OS: semaphore, mutex, monitor

PETERSON (2 processes)
 flag, turn

TAS / CAS: atomic

SEMAPHORE
 wait(S): S--
 signal(S): S++
 binary or counting

PRODUCER-CONSUMER
 mutex (1), empty (N), full (0)
 producer: wait(empty), wait(mutex), prod, signal(mutex), signal(full)
 consumer: wait(full), wait(mutex), cons, signal(mutex), signal(empty)

READERS-WRITERS
 reader-pref / writer-pref / fair

DINING PHILOSOPHERS
 deadlock if all grab left
 fix: limit, asymmetry, hierarchy, monitor

MONITOR: procedures + condition vars
 wait(c), signal(c)

DEADLOCK CONDITIONS (Coffman)
 1. mutual exclusion
 2. hold and wait
 3. no preemption
 4. circular wait

DEADLOCK STRATEGIES
 prevention: break a condition
 avoidance: Banker's safe state
 detection: cycle in RAG / Banker-like
 recovery: kill / preempt / rollback
 ignore (Ostrich)

RAG
 single-instance: cycle ⇔ deadlock
 multi-instance: cycle necessary, not sufficient

BANKER'S
 declare max; safe sequence check
 O(m n²)

STARVATION vs DEADLOCK vs LIVELOCK

PRIORITY INVERSION → priority inheritance
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | 4 Coffman conditions | ✅✅✅ |
| 2 | Banker's safe state check | ✅✅ |
| 3 | Single-instance: cycle ⇔ deadlock | ✅✅ |
| 4 | Critical section requirements | ✅✅ |
| 5 | Semaphore wait/signal | ✅✅ |
| 6 | Producer-consumer template | ✅✅ |
| 7 | Readers-writers preference | ✅ |
| 8 | Dining philosophers fixes | ✅ |
| 9 | Monitor structure | ✅ |
| 10 | Priority inversion fix | ✅ |
| 11 | TAS / CAS atomic | ✅ |
| 12 | Banker's complexity O(m n²) | ✅ |

### Tricks

- **Detect deadlock potential:** check if all 4 conditions can hold.
- **For Banker's:** simulate granting with available resources.
- **For RAG:** identify cycle visually.
- **Producer-consumer template:** memorize the mutex+empty+full pattern.
- **For readers-writers:** track count + first/last reader takes/releases the writer lock.
- **Always release locks** in reverse order of acquisition (avoid deadlock).

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Coffman's 4 conditions:
**Solution.** Mutual exclusion, hold-and-wait, no preemption, circular wait.

### Q2. (GATE CSE 2014)
Single-instance RAG cycle:
**Solution.** Implies deadlock.

### Q3. (GATE CSE 2018)
Multiple-instance RAG cycle:
**Solution.** Necessary, not sufficient.

### Q4. (GATE CSE 2008)
Counting semaphore initialized to N for resource pool of N:
**Solution.** Yes — N available.

### Q5. (GATE CSE 2010)
Banker's algorithm purpose:
**Solution.** Deadlock avoidance.

### Q6. (GATE CSE 2015)
Critical section requirements:
**Solution.** Mutual exclusion + progress + bounded waiting.

### Q7. (GATE CSE 2013)
Peterson's algorithm:
**Solution.** Mutual exclusion for 2 processes.

### Q8. (GATE CSE 2007)
TAS instruction:
**Solution.** Atomic test-and-set; for spinlocks.

### Q9. (GATE CSE 2003)
Producer-consumer semaphores:
**Solution.** mutex, empty (=N), full (=0).

### Q10. (GATE CSE 2009)
Dining philosophers naive solution problem:
**Solution.** Deadlock when all grab left.

### Q11. (GATE CSE 2019)
Monitors offer:
**Solution.** Higher-level synchronization with condition variables.

### Q12. (GATE CSE 2020)
Banker's safe state:
**Solution.** Some ordering of processes can complete.

### Q13. (GATE CSE 2021)
Priority inversion fix:
**Solution.** Priority inheritance.

### Q14. (GATE CSE 2016)
Difference deadlock vs starvation:
**Solution.** Deadlock: all blocked; starvation: some never get resource.

### Q15. (GATE CSE 2011)
Deadlock prevention by breaking circular wait:
**Solution.** Total ordering of resource types.

---

## 6. Practice Questions (20+)

### Easy

**P1.** What is a race condition?

**P2.** Critical section requirements?

**P3.** Semaphore operations?

**P4.** Counting vs binary semaphore?

**P5.** Coffman conditions?

**P6.** Banker's algorithm purpose?

**P7.** Peterson's algorithm scope?

**P8.** Difference: deadlock vs starvation.

**P9.** What is livelock?

**P10.** Priority inversion fix?

### Medium

**P11.** Implement producer-consumer with semaphores.

**P12.** Implement readers-writers (readers preference).

**P13.** Apply Banker's: 3 processes, 3 resources; trace.

**P14.** Detect deadlock from RAG with 4 processes.

**P15.** Test-and-Set spinlock implementation.

**P16.** Compare-and-Swap example use.

**P17.** Dining philosophers deadlock-free solution.

**P18.** Monitor implementation of producer-consumer.

**P19.** Detect critical section violations.

**P20.** Prevent deadlock by total ordering.

### Hard

**P21.** Trace Banker's algorithm on full example.

**P22.** Show readers-writers writer-preference.

**P23.** Implement bounded buffer with monitors.

**P24.** Detect all cycles in RAG.

**P25.** Recovery from deadlock via rollback.

**P26.** Dining philosophers with semaphore array.

**P27.** Compare semaphore vs monitor.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | unsynchronized concurrent access | direct |
| P2 | mutex + progress + bounded wait | direct |
| P3 | wait, signal | direct |
| P4 | binary 0/1; counting any | direct |
| P5 | as in 1.15 | direct |
| P6 | safe state check | direct |
| P7 | 2 processes | direct |
| P8 | all blocked vs some never gets | direct |
| P9 | active but no progress | direct |
| P10 | priority inheritance | direct |
| P11 | mutex+empty+full pattern | direct |
| P12 | classic | direct |
| P13 | trace | direct |
| P14 | look for cycle | direct |
| P15 | atomic loop | direct |
| P16 | lock-free queue | direct |
| P17 | asymmetric/hierarchy | direct |
| P18 | wait/signal on conditions | direct |
| P19 | violation = race | direct |
| P20 | enforce request order | direct |
| P21 | full Banker's trace | direct |
| P22 | track waiting writer | direct |
| P23 | classic | direct |
| P24 | DFS | direct |
| P25 | restore state | direct |
| P26 | one semaphore per fork | direct |
| P27 | monitor higher-level | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Counting semaphore can be negative | Some implementations: yes (waiters); usually queued. |
| 2 | Multi-instance cycle = deadlock | Not sufficient. |
| 3 | Banker's prevents deadlock | It detects unsafe states; doesn't grant. |
| 4 | Mutual exclusion always required | Some resources sharable. |
| 5 | Forget priority inversion | Use priority inheritance. |
| 6 | Confuse starvation with deadlock | Different. |
| 7 | Producer-consumer without mutex | Race condition on buffer. |
| 8 | Disable interrupts on multi-CPU | Doesn't work. |
| 9 | Spinlock on uniprocessor | Wastes CPU. |
| 10 | Treat livelock as deadlock | Different (active). |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Coffman's 4 conditions" | Mutex + Hold-Wait + No Preempt + Circular Wait. |
| "Banker's algorithm" | Safe state via simulation. |
| "RAG cycle (single-instance)" | Deadlock. |
| "Producer-consumer" | Use mutex + empty + full. |
| "Readers-writers" | Reader-preference vs writer-preference. |
| "Dining philosophers" | Asymmetry/hierarchy/limit. |
| "Monitor" | High-level sync. |
| "Spinlock" | TAS/CAS atomic. |
| "Priority inversion" | Inheritance fix. |
| "Deadlock prevention" | Break a condition. |

---

## 9. Quick Revision

```
RACE CONDITION = shared data + unsync

CRITICAL SECTION
 mutex + progress + bounded wait

SOLUTIONS
 sw: Peterson (2 proc), Bakery (n proc)
 hw: disable interrupts, TAS, CAS
 os: semaphore, mutex, monitor

SEMAPHORE: wait, signal
 binary (0/1) or counting

PRODUCER-CONSUMER
 mutex(1) + empty(N) + full(0)

READERS-WRITERS
 reader-pref / writer-pref / fair

DINING PHILOSOPHERS
 deadlock if naive
 fix: limit, asymmetry, hierarchy, monitor

MONITOR: procedures + condition vars

DEADLOCK = 4 Coffman conditions
 mutual exclusion
 hold and wait
 no preemption
 circular wait

DEADLOCK STRATEGIES
 prevent: break condition
 avoid: Banker's safe state
 detect: cycle / Banker-like
 recover: kill / preempt / rollback
 ignore (Ostrich)

RAG: single-inst cycle ⇔ deadlock
       multi-inst cycle ⇒ may

DEADLOCK ≠ STARVATION ≠ LIVELOCK

PRIORITY INVERSION → inheritance
```
