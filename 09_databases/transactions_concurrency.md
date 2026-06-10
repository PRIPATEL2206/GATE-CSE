# Transactions, Concurrency & Recovery

> Subject: Databases
> GATE weight: **2–4 marks** every year. ACID, conflict serializability, 2PL, recovery (UNDO/REDO).

---

## 1. Concept Explanation

### 1.1 Transaction

A logical unit of work; sequence of operations on database that must be **atomic**.

**Operations:** READ(X), WRITE(X), COMMIT, ABORT/ROLLBACK.

### 1.2 ACID Properties

| Property | Description |
|---|---|
| **Atomicity** | All or nothing |
| **Consistency** | Preserves integrity constraints |
| **Isolation** | Concurrent transactions don't interfere |
| **Durability** | Committed changes persist |

### 1.3 Transaction States

```
Active → Partially Committed → Committed
         ↓                    ↓
        Failed → Aborted
```

### 1.4 Concurrency Issues

| Issue | Description |
|---|---|
| **Lost update** | Two writes; later overwrites earlier |
| **Dirty read** | Read uncommitted value |
| **Non-repeatable read** | Re-read returns different value |
| **Phantom read** | Re-read returns extra rows |

### 1.5 Schedule

Sequence of operations from concurrent transactions.

| Type | Description |
|---|---|
| **Serial** | Transactions one at a time |
| **Serializable** | Equivalent to some serial schedule |
| **Conflict serializable** | Conflict-equivalent to a serial schedule |
| **View serializable** | View-equivalent (broader than conflict) |

### 1.6 Conflict Operations

Two operations **conflict** iff:
- Both from different transactions.
- Both on **same data item**.
- At least one is **WRITE**.

**Types:**
- READ-WRITE
- WRITE-READ
- WRITE-WRITE

### 1.7 Conflict Equivalence & Serializability

Schedule S₁ ≡_c S₂ if same conflicting operations in same relative order (between same pair of transactions).

**Conflict serializable** = conflict equivalent to some serial schedule.

### 1.8 Precedence Graph

Nodes: transactions. Edge T_i → T_j if some op of T_i conflicts and precedes one of T_j.

**Conflict serializable ⇔ acyclic precedence graph.**

### 1.9 View Serializability

Stronger than conflict serializability for some cases (with blind writes). View equivalence based on:
- Initial reads same.
- Final writes same.
- Read-from same.

**Conflict serializable ⊆ view serializable.**

### 1.10 Recoverable Schedule

A schedule is **recoverable** if no transaction commits before transactions it read from commit.

**Cascadeless:** transactions only read from committed.

**Strict:** stronger; reads/writes of T_i wait for commit of producer.

`Strict ⊊ Cascadeless ⊊ Recoverable`.

### 1.11 Locking

Acquire locks before access; release after.

| Lock | Compatible with |
|---|---|
| **Shared (S)** | Other S |
| **Exclusive (X)** | None |

### 1.12 Two-Phase Locking (2PL)

Two phases per transaction:
1. **Growing:** acquire locks (no release).
2. **Shrinking:** release locks (no acquire).

**Theorem:** 2PL ⇒ conflict serializable.

### 1.13 Variants of 2PL

| Variant | Description |
|---|---|
| **Basic 2PL** | Standard |
| **Strict 2PL** | All X-locks held until commit |
| **Rigorous 2PL** | All locks held until commit |
| **Conservative 2PL** | All locks acquired at start |

**Strict 2PL** prevents cascading aborts.

### 1.14 Deadlock in Locking

Possible: T1 holds A, wants B; T2 holds B, wants A.

**Detection:** wait-for graph; cycle ⇒ deadlock.

**Prevention:**
- **Wait-die:** older waits, younger dies (timestamp-based).
- **Wound-wait:** older wounds (aborts) younger, older waits.

### 1.15 Timestamp Ordering

Each transaction has timestamp (TS).

For each data item X:
- read_TS(X), write_TS(X).

**Rules:**
- **Read X by T:** if TS(T) < write_TS(X), abort. Else update read_TS(X).
- **Write X by T:** if TS(T) < read_TS(X) or write_TS(X), abort. Else write.

### 1.16 Multi-version Concurrency Control (MVCC)

Multiple versions of data item; readers don't block writers.

Used in PostgreSQL, Oracle.

### 1.17 Optimistic Concurrency Control

Transactions execute without locking. At commit, validate; abort if conflict.

**Phases:** Read, Validation, Write.

### 1.18 Recovery

After crash: restore consistent state.

**Log records:**
- `<T_i, X, old, new>` (write).
- `<T_i, START>`, `<T_i, COMMIT>`, `<T_i, ABORT>`.

### 1.19 UNDO / REDO

| Action | Triggered by |
|---|---|
| **UNDO** | Rollback uncommitted transactions |
| **REDO** | Re-apply committed transactions after crash |

### 1.20 Recovery Algorithms

| Algorithm | Description |
|---|---|
| **Deferred update** | Don't modify DB until commit; UNDO not needed |
| **Immediate update** | Modify DB but log changes; both UNDO & REDO needed |
| **Shadow paging** | Copy-on-write; no log needed |
| **ARIES** | Industry-standard; uses LSN, checkpoints |

### 1.21 Checkpointing

Periodic snapshot to limit recovery time.

**During checkpoint:** flush dirty buffers; write checkpoint record.

**After crash:** start recovery from last checkpoint.

### 1.22 Log-Based Recovery (Write-Ahead Logging - WAL)

**Rule:** log record must be written before corresponding data block is written to disk.

Ensures durability.

### 1.23 Isolation Levels (SQL)

| Level | Allows |
|---|---|
| **Read Uncommitted** | Dirty reads |
| **Read Committed** | No dirty; non-repeatable possible |
| **Repeatable Read** | No dirty / non-repeatable; phantom possible |
| **Serializable** | All prevented |

### 1.24 Common GATE Patterns

- Test if schedule is conflict serializable.
- Build precedence graph.
- Apply 2PL to schedule.
- Identify deadlock.
- Apply UNDO/REDO.

> **Summary:** ACID ensures correctness. Concurrency via locking (2PL), timestamps, or MVCC. Conflict serializability via precedence graph. Recovery via UNDO/REDO + WAL + checkpoints.

---

## 2. Important Points

- **ACID** = Atomicity / Consistency / Isolation / Durability.
- **Conflict serializable** ⇔ acyclic precedence graph.
- **2PL** guarantees conflict serializability.
- **Strict 2PL** prevents cascading aborts.
- **Conflict serializable** ⊆ view serializable.
- **Wait-for graph cycle** = deadlock.
- **Wait-die / Wound-wait** are timestamp-based prevention.
- **MVCC** allows readers to bypass writers.
- **WAL** ensures log written before data.
- **Recoverable / cascadeless / strict** form a hierarchy.
- **UNDO** for uncommitted; **REDO** for committed.
- **Checkpointing** limits recovery scope.
- **Isolation levels** trade consistency for concurrency.

---

## 3. Short Notes

```
TRANSACTION
 logical unit; READ, WRITE, COMMIT, ABORT
 states: active → partially committed → committed (or failed → aborted)

ACID
 atomicity / consistency / isolation / durability

CONCURRENCY ISSUES
 lost update, dirty read, non-repeatable, phantom

SCHEDULES
 serial, serializable
 conflict serializable, view serializable
 conflict ⊆ view

CONFLICT
 different transactions, same data, ≥ 1 write

PRECEDENCE GRAPH
 conflict serializable ⇔ acyclic

VIEW EQUIVALENCE
 initial reads, final writes, read-from same

RECOVERABLE
 commit only after dependencies commit

CASCADELESS
 read only committed values

STRICT
 read/write only after commit of producer

LOCKING
 S (shared) compatible with S
 X (exclusive) incompatible

2PL
 growing + shrinking phases
 ⇒ conflict serializable

VARIANTS
 strict 2PL: hold X till commit
 rigorous: hold all till commit
 conservative: lock at start

DEADLOCK
 wait-for graph cycle
 wait-die / wound-wait prevention

TIMESTAMP ORDERING
 read/write rules; abort if violated

MVCC: multiple versions, readers no block

OPTIMISTIC: read → validate → write

RECOVERY
 log: <T, X, old, new>, START, COMMIT, ABORT
 UNDO uncommitted; REDO committed
 deferred / immediate / shadow / ARIES

WAL: log before data

CHECKPOINTING limits recovery

ISOLATION LEVELS (SQL)
 read uncommitted / committed / repeatable read / serializable
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | ACID 4 properties | ✅✅✅ |
| 2 | Conflict serializable ⇔ acyclic precedence graph | ✅✅✅ |
| 3 | 2PL ⇒ conflict serializable | ✅✅ |
| 4 | Strict 2PL prevents cascading aborts | ✅✅ |
| 5 | Wait-die: older waits, younger dies | ✅ |
| 6 | Wound-wait: older wounds younger | ✅ |
| 7 | UNDO uncommitted; REDO committed | ✅✅ |
| 8 | WAL: log before data | ✅✅ |
| 9 | MVCC for high concurrency | ✅ |
| 10 | Isolation levels: 4 standard | ✅✅ |
| 11 | View serializable ⊋ conflict serializable | ✅ |

### Tricks

- **Build precedence graph:** scan operations; for each conflict between T_i (earlier) and T_j (later), add T_i → T_j.
- **Test cycle:** DFS for back edges.
- **Apply 2PL:** ensure no acquire after first release in any transaction.
- **For deadlock:** look for cyclic wait.
- **For schedule recovery:** check commit ordering.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
ACID properties:
**Solution.** Atomicity, Consistency, Isolation, Durability.

### Q2. (GATE CSE 2014)
Conflict serializable iff:
**Solution.** Precedence graph acyclic.

### Q3. (GATE CSE 2018)
2PL ensures:
**Solution.** Conflict serializability.

### Q4. (GATE CSE 2008)
Strict 2PL prevents:
**Solution.** Cascading aborts.

### Q5. (GATE CSE 2010)
Wait-die scheme:
**Solution.** Older waits; younger dies.

### Q6. (GATE CSE 2015)
WAL rule:
**Solution.** Log before data write.

### Q7. (GATE CSE 2013)
UNDO operation:
**Solution.** Rolls back uncommitted transactions.

### Q8. (GATE CSE 2007)
Read-Write conflict:
**Solution.** Read of A then Write of A by another transaction.

### Q9. (GATE CSE 2003)
Phantom read:
**Solution.** Re-read returns extra rows.

### Q10. (GATE CSE 2009)
View serializable ⊃ conflict serializable:
**Solution.** True.

### Q11. (GATE CSE 2019)
Lost update problem:
**Solution.** Two writes; later overwrites earlier.

### Q12. (GATE CSE 2020)
Isolation level for serializable:
**Solution.** Strictest; prevents all anomalies.

### Q13. (GATE CSE 2021)
Wound-wait:
**Solution.** Older wounds (aborts) younger.

### Q14. (GATE CSE 2016)
MVCC advantage:
**Solution.** Readers don't block writers.

### Q15. (GATE CSE 2011)
Checkpointing benefit:
**Solution.** Limits recovery time.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define transaction.

**P2.** ACID properties.

**P3.** Conflict between operations.

**P4.** Precedence graph.

**P5.** 2PL phases.

**P6.** Wait-die vs wound-wait.

**P7.** WAL.

**P8.** UNDO vs REDO.

**P9.** Lost update.

**P10.** Isolation levels (4).

### Medium

**P11.** Test conflict serializability of given schedule.

**P12.** Build precedence graph.

**P13.** Apply 2PL to schedule.

**P14.** Detect deadlock in wait-for graph.

**P15.** Apply timestamp ordering.

**P16.** Identify isolation level for given anomaly.

**P17.** Apply UNDO/REDO recovery.

**P18.** Checkpoint usage.

**P19.** MVCC scenario.

**P20.** Optimistic concurrency control phases.

### Hard

**P21.** Show conflict serializable but not view serializable example.

**P22.** Prove 2PL ⇒ conflict serializability.

**P23.** Apply ARIES recovery algorithm.

**P24.** Deadlock prevention with timestamps.

**P25.** Phantom read solution.

**P26.** Cascadeless schedule example.

**P27.** Strict 2PL implementation.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | logical unit of work | direct |
| P2 | ACID | direct |
| P3 | different transactions, same data, ≥1 write | direct |
| P4 | nodes = transactions | direct |
| P5 | growing + shrinking | direct |
| P6 | as in 1.14 | direct |
| P7 | log before data | direct |
| P8 | uncommitted vs committed | direct |
| P9 | overwrite | direct |
| P10 | uncomm / comm / repeat / serial | direct |
| P11 | precedence graph cycle | direct |
| P12 | trace conflicts | direct |
| P13 | partition phases | direct |
| P14 | cycle | direct |
| P15 | TS rules | direct |
| P16 | match anomaly | direct |
| P17 | per log record | direct |
| P18 | snapshot | direct |
| P19 | MVCC trace | direct |
| P20 | read, validate, write | direct |
| P21 | classic with blind writes | direct |
| P22 | precedence graph acyclic | direct |
| P23 | analysis + redo + undo | direct |
| P24 | wait-die / wound-wait | direct |
| P25 | range locks | direct |
| P26 | example | direct |
| P27 | hold X till commit | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | All conflict-equivalent serial = same | Different orderings possible. |
| 2 | 2PL deadlock-free | Can deadlock. |
| 3 | View ⊆ conflict | Other way: conflict ⊆ view. |
| 4 | UNDO and REDO same | Different. |
| 5 | WAL = REDO logging only | Includes both. |
| 6 | Isolation = Serializability | Levels vary. |
| 7 | Strict 2PL = Rigorous 2PL | Different. |
| 8 | MVCC slow | Often faster. |
| 9 | Recoverable = Cascadeless | Hierarchy. |
| 10 | Optimistic always good | Bad with high contention. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Conflict serializable" | Precedence graph acyclic. |
| "2PL" | Growing/shrinking phases. |
| "Isolation level" | 4 standard SQL levels. |
| "WAL" | Log before data. |
| "UNDO/REDO" | Uncommitted vs committed. |
| "Wait-die / wound-wait" | Timestamp deadlock prevention. |
| "MVCC" | Multiple versions. |
| "Schedule recoverability" | Commit ordering. |
| "Checkpoint" | Reduce recovery scope. |
| "Phantom read" | Range query anomaly. |

---

## 9. Quick Revision

```
TRANSACTION: READ, WRITE, COMMIT, ABORT
ACID
 atomicity, consistency, isolation, durability

CONFLICTS: diff txn + same data + ≥1 write
PRECEDENCE GRAPH
 conflict serializable ⇔ acyclic

VIEW SERIALIZABLE ⊋ CONFLICT SERIALIZABLE

RECOVERABLE ⊋ CASCADELESS ⊋ STRICT (in restrictiveness)

LOCKING: S compat S; X exclusive

2PL: growing + shrinking
 ⇒ conflict serializable
 strict 2PL: X till commit (no cascading abort)
 rigorous: all till commit
 conservative: at start

DEADLOCK
 wait-for graph cycle
 prevent: wait-die, wound-wait

TIMESTAMP ORDERING: rules per data item

MVCC: multiple versions; readers don't block

OPTIMISTIC: read → validate → write

RECOVERY
 log: <T, X, old, new>, START, COMMIT, ABORT
 UNDO uncommitted; REDO committed
 WAL: log before data
 deferred / immediate / shadow / ARIES

CHECKPOINTING limits recovery

ISOLATION LEVELS
 read uncommitted / committed / repeatable / serializable

ANOMALIES
 dirty read, non-repeatable, phantom, lost update
```
