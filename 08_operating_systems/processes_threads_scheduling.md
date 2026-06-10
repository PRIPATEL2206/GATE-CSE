# Processes, Threads & CPU Scheduling

> Subject: Operating Systems
> GATE weight: **3–6 marks** every year. Process states, scheduling algorithms, Gantt charts, waiting/turnaround time.

---

## 1. Concept Explanation

### 1.1 Process vs Program

| Term | Definition |
|---|---|
| **Program** | Static code on disk |
| **Process** | Program in execution + state (memory, CPU registers, etc.) |

A process is the **active** entity.

### 1.2 Process States

```
NEW → READY ⇄ RUNNING → TERMINATED
              ↕
            WAITING (I/O / event)
```

| State | Description |
|---|---|
| **New** | Being created |
| **Ready** | Waiting for CPU |
| **Running** | Executing on CPU |
| **Waiting/Blocked** | Waiting for I/O or event |
| **Terminated** | Finished |

**Transitions:** Ready → Running (dispatch); Running → Waiting (I/O); Waiting → Ready (I/O complete); Running → Ready (preemption / time slice).

### 1.3 Process Control Block (PCB)

OS data structure containing process info:
- PID, state.
- Program counter (PC), registers.
- Memory limits, page table.
- Open files, I/O status.
- Accounting info (CPU usage).

### 1.4 Context Switching

OS saves current process state (in PCB) + loads next process's state.

**Cost:** non-trivial; affects overhead.

### 1.5 Process vs Thread

| Aspect | Process | Thread |
|---|---|---|
| Memory | Separate address space | Shared with peers |
| Communication | IPC required | Shared memory |
| Creation cost | High | Low |
| Switching cost | High | Low |
| Failure isolation | One can't crash another | One thread crash may bring down all |

Threads = "lightweight processes" within a process.

### 1.6 Thread Models

| Model | Description |
|---|---|
| **User-level (1:N)** | Many user threads → 1 kernel; fast but no parallelism per process |
| **Kernel-level (1:1)** | 1 user thread per kernel thread |
| **Hybrid (M:N)** | M user → N kernel |

### 1.7 IPC (Inter-Process Communication)

| Mechanism | Description |
|---|---|
| **Pipes** | Unidirectional byte stream |
| **Named pipes (FIFOs)** | Persist beyond creator |
| **Message queues** | Discrete messages with type |
| **Shared memory** | Fastest; explicit sync needed |
| **Sockets** | Network-capable |
| **Signals** | Async notifications |
| **Semaphores** | Synchronization, sometimes IPC |

### 1.8 CPU Scheduling Goals

- **Maximize:** CPU utilization, throughput, fairness.
- **Minimize:** waiting time, turnaround time, response time.

### 1.9 Performance Metrics

| Metric | Definition |
|---|---|
| **CPU utilization** | % CPU busy |
| **Throughput** | # processes completed / time |
| **Turnaround time (TAT)** | Completion − Arrival |
| **Waiting time (WT)** | Time in ready queue (TAT − Burst) |
| **Response time** | First scheduled − Arrival (interactive) |

For non-preemptive: WT = TAT − Burst.
For preemptive: WT = total time in ready queue.

### 1.10 Scheduling Algorithms

| Algorithm | Preemptive? | Type |
|---|---|---|
| **FCFS** (First-Come First-Served) | No | Simple |
| **SJF** (Shortest Job First) | Optionally | Optimal avg WT |
| **SRTF** (Shortest Remaining Time First) | Yes | Preemptive SJF |
| **Priority** | Optionally | By priority value |
| **Round Robin (RR)** | Yes | Time slice |
| **Multilevel Queue** | Either | Multiple queues |
| **Multilevel Feedback Queue** | Yes | Adaptive movement |

### 1.11 FCFS

Run in arrival order. Simple but suffers **convoy effect** (long process delays short ones).

**Average WT:** Σ WTᵢ / n.

### 1.12 SJF (Non-preemptive)

Pick smallest burst time among arrived processes.

**Optimal:** minimum average waiting time among non-preemptive algorithms.

**Issue:** burst time generally not known in advance; predicted via exponential averaging:
`τₙ₊₁ = α · tₙ + (1 − α) · τₙ`.

### 1.13 SRTF (Preemptive SJF)

Whenever new process arrives, compare its burst with remaining time of running process; preempt if shorter.

**Optimal** for avg waiting time among all algorithms (with full info).

### 1.14 Priority Scheduling

Each process has priority. Run highest priority first.

**Issue:** **starvation** of low-priority. Solution: **aging** (priority increases over time).

### 1.15 Round Robin

Each process gets a time slice (quantum). After quantum, preempted to back of queue.

**Quantum trade-offs:**
- Small: more switching overhead, higher response.
- Large: degenerates to FCFS.

### 1.16 Multilevel Queue

Multiple queues for different process types (system, interactive, batch). Each may have its own scheduling.

**Inter-queue scheduling:** strict priority or time-slicing.

### 1.17 Multilevel Feedback Queue

Processes move between queues based on behavior:
- New process → highest priority queue.
- Use full quantum → demoted.
- Yield CPU early → promoted.

### 1.18 Gantt Chart

Time diagram showing which process runs when.

```
| P1 | P2 | P1 | P3 | P2 | P3 |
0    4    7    9   12  15   17
```

### 1.19 Scheduling Calculations Walkthrough

| Process | Arrival | Burst |
|---|---|---|
| P1 | 0 | 5 |
| P2 | 1 | 3 |
| P3 | 2 | 8 |

**FCFS** order: P1, P2, P3. Completion: 5, 8, 16.
TAT: 5, 7, 14. WT: 0, 4, 6. Avg WT: 10/3 ≈ 3.33.

**SJF (preemptive = SRTF):**
- t=0: P1 (5).
- t=1: arrive P2 (3). Compare. P2 smaller → preempt. Run P2.
- t=4: P2 done. Resume P1 (4 left), P3 (8) waiting.
- t=8: P1 done. Run P3.
- t=16: P3 done.

Computation: Compl P1=8, P2=4, P3=16. TAT: 8, 3, 14. WT: 3, 0, 6. Avg WT: 3.

### 1.20 Convoy Effect

In FCFS, long process at front delays many short ones → poor avg WT.

### 1.21 Real-Time Scheduling

| Type | Description |
|---|---|
| **Hard real-time** | Deadlines must be met (avionics) |
| **Soft real-time** | Best effort (multimedia) |

**Algorithms:**
- **Rate Monotonic (RM):** static priority; shorter period → higher priority. Schedulable if Σ Cᵢ/Tᵢ ≤ n(2^(1/n) − 1).
- **Earliest Deadline First (EDF):** dynamic; closest deadline first. Optimal for single-CPU. Schedulable if Σ Cᵢ/Tᵢ ≤ 1.

### 1.22 Multi-core / SMP Scheduling

- **Load balancing:** spread work.
- **Processor affinity:** keep process on same CPU.
- **Push/pull migration.**

> **Summary:** Process = active program. PCB stores state. Threads share memory. Scheduling: FCFS / SJF / SRTF / Priority / RR. Compute Gantt chart, WT, TAT for given input. SJF optimal for avg WT (non-preemptive); SRTF optimal preemptive.

---

## 2. Important Points

- **Process has its own memory**; **threads share** within process.
- **Context switch** is expensive; thread switch is cheaper than process.
- **PCB** contains process state.
- **CPU scheduling** decides among ready processes.
- **TAT = Completion − Arrival.**
- **WT = TAT − Burst** (non-preemptive); else cumulative wait time.
- **SJF** = optimal avg WT (non-preemptive).
- **SRTF** = optimal avg WT (preemptive).
- **RR** trade-off depends on quantum.
- **Priority scheduling** suffers from **starvation**; fix with **aging**.
- **Convoy effect** in FCFS.
- **Multilevel feedback** is most flexible.
- **EDF** optimal for real-time on uniprocessor.
- **Rate Monotonic** is a static-priority real-time scheduler.

---

## 3. Short Notes

```
PROCESS STATES
 NEW → READY ⇄ RUNNING → TERMINATED
                ↕
              WAITING

PCB: PID, state, PC, regs, memory, files

THREAD vs PROCESS
 thread: shared memory, lightweight
 process: separate, heavy

THREAD MODELS: 1:N, 1:1, M:N

IPC
 pipes, named pipes, message queues,
 shared memory, sockets, signals, semaphores

SCHEDULING METRICS
 TAT = Completion − Arrival
 WT = TAT − Burst (non-preemp)
 throughput, CPU util, response

ALGORITHMS
 FCFS: no preempt, convoy effect
 SJF: shortest burst, optimal avg WT
 SRTF: preemptive SJF
 Priority: starvation; aging
 RR: time slice; quantum critical
 Multilevel queue / feedback

GANTT CHART: time diagram

REAL-TIME
 RM: static priority by period
 EDF: dynamic by deadline; optimal uni-CPU

MULTICORE: load balance, affinity, migration

CONVOY EFFECT: FCFS long process

PRIORITY ISSUES
 starvation → aging
```

---

## 4. Formulas / Tricks

| # | Formula | Memorize Cold? |
|---|---|---|
| 1 | TAT = Completion − Arrival | ✅✅ |
| 2 | WT = TAT − Burst | ✅✅ |
| 3 | Avg WT = ΣWTᵢ / n | ✅ |
| 4 | SJF optimal avg WT (non-preemptive) | ✅✅ |
| 5 | SRTF optimal avg WT (preemptive) | ✅✅ |
| 6 | RM schedulable: Σ Cᵢ/Tᵢ ≤ n(2^(1/n) − 1) | ✅ |
| 7 | EDF schedulable: Σ Cᵢ/Tᵢ ≤ 1 | ✅ |
| 8 | RR with quantum q: each process waits ≤ (n−1)q before next slice | ✅ |
| 9 | Throughput = # complete / time | ✅ |
| 10 | CPU util = busy time / total | ✅ |
| 11 | Aging combats starvation | ✅ |
| 12 | Context switch cost is real | ✅ |

### Tricks

- **Build Gantt chart** from arrival + burst times.
- **For SRTF:** at each event (arrival/completion), pick min remaining burst.
- **For RR:** use circular queue, time slice processes in turn.
- **TAT/WT computation:** use Gantt chart + per-process completion times.
- **For real-time:** check schedulability bound first.
- **Priority inversion:** low priority holds resource needed by high priority. Fix: priority inheritance.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Optimal avg WT scheduling algorithm:
**Solution.** SJF (non-preempt) or SRTF (preempt).

### Q2. (GATE CSE 2014)
Round Robin quantum effect:
**Solution.** Small → high overhead; large → ≈ FCFS.

### Q3. (GATE CSE 2018)
Convoy effect occurs in:
**Solution.** FCFS.

### Q4. (GATE CSE 2008)
Process state when waiting for I/O:
**Solution.** Waiting / Blocked.

### Q5. (GATE CSE 2010)
PCB stores:
**Solution.** Process metadata: PID, state, PC, registers, memory, files.

### Q6. (GATE CSE 2015)
Thread vs process: which has lower context switch cost?
**Solution.** Thread.

### Q7. (GATE CSE 2013)
Priority scheduling problem:
**Solution.** Starvation; fixed by aging.

### Q8. (GATE CSE 2007)
SRTF preempts when:
**Solution.** New process has shorter remaining burst.

### Q9. (GATE CSE 2003)
TAT formula:
**Solution.** Completion − Arrival.

### Q10. (GATE CSE 2009)
WT formula (non-preemptive):
**Solution.** TAT − Burst.

### Q11. (GATE CSE 2019)
Avg WT for FCFS with bursts 5, 3, 8 (arriving in order):
**Solution.** WT: 0, 5, 8 → avg = 13/3 ≈ 4.33.

### Q12. (GATE CSE 2020)
Scheduling using EDF:
**Solution.** Earliest deadline highest priority.

### Q13. (GATE CSE 2021)
Multilevel feedback queue:
**Solution.** Adaptive priorities; processes move based on behavior.

### Q14. (GATE CSE 2016)
RM schedulability bound for n=3:
**Solution.** 3(2^(1/3) − 1) ≈ 0.7797.

### Q15. (GATE CSE 2011)
Difference: program vs process.
**Solution.** Program is static; process is active.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define process.

**P2.** Process states list.

**P3.** PCB contents.

**P4.** Thread vs process key difference.

**P5.** TAT formula.

**P6.** WT formula (non-preemptive).

**P7.** SJF stands for?

**P8.** SRTF stands for?

**P9.** Round Robin requires?

**P10.** Aging fixes what?

### Medium

**P11.** Compute Gantt chart for FCFS: P1(0,5), P2(1,3), P3(2,8).

**P12.** Compute SJF (non-preemptive) for above.

**P13.** Compute SRTF for above.

**P14.** Compute Round Robin quantum 2 for above.

**P15.** Avg WT for FCFS in P11.

**P16.** Detect convoy effect example.

**P17.** Difference between hard and soft real-time.

**P18.** What is priority inversion?

**P19.** Multilevel queue vs multilevel feedback queue.

**P20.** Predicting next CPU burst (exponential averaging).

### Hard

**P21.** Compute average TAT and WT for SRTF on 4-process schedule.

**P22.** Show RM unschedulable example.

**P23.** EDF schedulability check.

**P24.** Multiprocessor scheduling: affinity vs load balance.

**P25.** Implement RR using a queue.

**P26.** Compare scheduling for I/O-bound vs CPU-bound processes.

**P27.** Solve real-time scheduling with periodic tasks.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | program in execution | direct |
| P2 | new, ready, running, waiting, terminated | direct |
| P3 | PID, state, PC, regs, memory, files | direct |
| P4 | shared memory | direct |
| P5 | Compl − Arrival | direct |
| P6 | TAT − Burst | direct |
| P7 | Shortest Job First | direct |
| P8 | Shortest Remaining Time First | direct |
| P9 | time quantum | direct |
| P10 | starvation | direct |
| P11 | trace | direct |
| P12 | trace | direct |
| P13 | trace | direct |
| P14 | trace circular | direct |
| P15 | (0+4+6)/3 = 3.33 | direct |
| P16 | long process at front delays short | direct |
| P17 | hard: must meet; soft: try | direct |
| P18 | low holds resource needed by high | direct |
| P19 | feedback allows movement | direct |
| P20 | τₙ₊₁ = α·tₙ + (1−α)τₙ | direct |
| P21 | trace SRTF | direct |
| P22 | sum > bound | direct |
| P23 | sum ≤ 1 | direct |
| P24 | trade-off | direct |
| P25 | round-robin queue | direct |
| P26 | I/O-bound interactive; CPU-bound batch | direct |
| P27 | use RM or EDF | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing TAT and WT | TAT = WT + Burst. |
| 2 | RR quantum too small ⇒ no overhead (myth) | Causes high overhead. |
| 3 | SJF preempts (myth) | Non-preemptive SJF; preempt = SRTF. |
| 4 | Priority scheduling fair (myth) | Causes starvation. |
| 5 | Forgetting context switch cost | Real impact. |
| 6 | Multilevel queue = feedback (myth) | Different. |
| 7 | EDF schedulable always (myth) | Only if Σ Cᵢ/Tᵢ ≤ 1. |
| 8 | RM ≥ EDF (myth) | EDF is more flexible. |
| 9 | Process and thread state independent | Threads share. |
| 10 | All schedulers preemptive | FCFS is not. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Compute Gantt chart" | Trace algorithm step-by-step. |
| "Find avg WT/TAT" | Compute per process; average. |
| "Optimal avg WT" | SJF / SRTF. |
| "Convoy effect" | FCFS. |
| "Starvation" | Priority; fix with aging. |
| "Priority inversion" | Low holds; fix with priority inheritance. |
| "Real-time periodic tasks" | RM (static) or EDF (dynamic). |
| "Quantum trade-off" | RR quantum sizing. |
| "Process vs thread" | Memory sharing. |
| "Predicting burst" | Exponential averaging. |

---

## 9. Quick Revision

```
PROCESS STATES
 NEW → READY ⇄ RUNNING → TERMINATED
                ↕ WAITING

PCB stores: PID, state, PC, regs, memory, files

THREADS share memory; lighter context switch

IPC: pipes, FIFOs, queues, shared mem,
      sockets, signals, semaphores

METRICS
 TAT = Completion − Arrival
 WT = TAT − Burst
 Throughput, CPU util, Response

ALGORITHMS
 FCFS: convoy effect
 SJF: optimal avg WT (non-preempt)
 SRTF: optimal avg WT (preempt)
 Priority: starvation → aging
 RR: quantum critical
 Multilevel queue / feedback

REAL-TIME
 RM: static, period priority
   bound: Σ C/T ≤ n(2^(1/n) − 1)
 EDF: dynamic, deadline
   bound: Σ C/T ≤ 1

MULTICORE
 load balancing, affinity, migration

PRIORITY INVERSION → priority inheritance
```
