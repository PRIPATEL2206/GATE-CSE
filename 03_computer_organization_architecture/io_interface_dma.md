# I/O Interface & DMA

> Subject: Computer Organization & Architecture (COA)
> GATE weight: **1–3 marks** every year. I/O techniques (programmed, interrupt, DMA), interrupt handling, bus arbitration.

---

## 1. Concept Explanation

### 1.1 I/O Devices

External devices vary widely: keyboards (slow human-input), disks (block-oriented), networks (packetized), GPUs (high-throughput).

CPU communicates with I/O via **interfaces** (controllers).

### 1.2 I/O Addressing

- **Memory-mapped I/O:** I/O registers occupy memory addresses; same load/store instructions used.
- **I/O-mapped (port-mapped) I/O:** separate I/O address space with special instructions (IN, OUT in x86).

### 1.3 I/O Techniques

Three principal methods for CPU-I/O data transfer:

| Method | CPU involvement | Speed |
|---|---|---|
| **Programmed I/O (polling)** | CPU polls device status; waits | Slow, simple |
| **Interrupt-driven I/O** | CPU notified when device ready | Faster than polling |
| **DMA (Direct Memory Access)** | DMA controller transfers data without CPU | Fastest for bulk |

### 1.4 Programmed I/O (Polling)

CPU repeatedly checks status register until device is ready, then transfers data.

**Pros:** simple, no extra hardware.
**Cons:** CPU busy-waits → wastes cycles.

Loop:
```
while (status_reg != READY) ;     // poll
data_reg = ... or read data_reg
```

### 1.5 Interrupt-Driven I/O

Device signals CPU via **interrupt** when ready. CPU executes ISR (interrupt service routine).

**Steps:**
1. Device asserts interrupt request (IRQ).
2. CPU finishes current instruction.
3. Saves PC and registers (context save).
4. Looks up interrupt vector.
5. Jumps to ISR.
6. ISR transfers data.
7. RTI (return from interrupt) restores context.

**Pros:** CPU productive between events.
**Cons:** still CPU-bound transfers; overhead per interrupt.

### 1.6 Interrupt Types

| Type | Triggered by |
|---|---|
| **Maskable** | Disabled via interrupt mask register |
| **Non-maskable (NMI)** | Cannot be disabled (e.g., hardware error) |
| **Software (trap)** | INT instruction |
| **Exception** | Synchronous (divide-by-0, page fault) |
| **External** | Hardware device |

### 1.7 Interrupt Handling Mechanisms

| Mechanism | Description |
|---|---|
| **Polled** | CPU polls interrupt sources |
| **Vectored** | Each device has unique vector → directly indexes ISR table |
| **Daisy-chain** | Devices share IRQ; priority via chain |
| **PIC (Programmable Interrupt Controller)** | 8259-style; manages multiple IRQs |

### 1.8 Direct Memory Access (DMA)

DMA controller transfers data **directly** between memory and device without CPU intervention (for the bulk of the transfer).

**DMA setup phase (CPU does):**
1. Source address.
2. Destination address.
3. Byte count.
4. Direction (read/write).
5. Start signal.

**Transfer phase (DMA does):**
- DMA fetches/writes data.
- Increments addresses.
- Decrements count.
- Asserts interrupt when count = 0.

### 1.9 DMA Modes

| Mode | Description |
|---|---|
| **Burst** | DMA holds bus until entire transfer complete (fast; CPU idle) |
| **Cycle-stealing** | DMA grabs bus one cycle per transfer; CPU runs in between |
| **Transparent** | DMA only when CPU doesn't need bus; lowest priority |

### 1.10 Bus Arbitration

When multiple masters want bus:

| Method | Description |
|---|---|
| **Daisy-chain** | Requests propagate; first device grants bus |
| **Centralized** | Bus controller arbitrates |
| **Distributed** | Devices arbitrate themselves |
| **Polling** | Controller polls one at a time |

### 1.11 Bus Types

- **Synchronous bus:** all transfers on clock edges; simpler, faster.
- **Asynchronous bus:** handshake-based; flexible but slower.

### 1.12 I/O Performance

For programmed I/O:
- CPU dedicated to I/O during transfer → wasted on long ops.

For DMA:
- CPU can perform other work during DMA transfer.
- Overhead = DMA setup + interrupt at end.

### 1.13 Bus Bandwidth

`Bandwidth = bus_width × clock_freq` (or × transfers_per_sec).

For 32-bit bus at 100 MHz: 4 B × 100 M = 400 MB/s.

### 1.14 Interrupt Latency

Total time from device asserting IRQ to ISR start.

- Interrupt response time = pipeline flush + context save + vector lookup + ISR jump.

### 1.15 Disk I/O Basics (preview)

| Term | Definition |
|---|---|
| Seek time | Move head to correct track |
| Rotational latency | Wait for sector to rotate under head |
| Transfer time | Read/write data |
| Total disk access | Seek + Rotational + Transfer |

> **Summary:** Three I/O methods (polling, interrupt, DMA). DMA has setup + transfer + completion phases. Memory-mapped vs port-mapped addressing. Interrupts have priority and vectoring schemes.

---

## 2. Important Points

- **Polling** is simplest but wastes CPU cycles.
- **Interrupt** lets CPU run other work between events.
- **DMA** is essential for high-bandwidth devices (disks, NICs).
- **DMA** requires bus arbitration with CPU.
- **DMA controller has its own state** — count, address, direction.
- **Memory-mapped I/O** uses standard load/store; **port-mapped** uses special IN/OUT.
- **NMI** cannot be disabled — used for fatal errors.
- **Vectored interrupts** are faster than polled (no scanning).
- **Daisy-chain** has fixed priority (chain order).
- **Cycle stealing** balances CPU and DMA throughput.
- **Page fault** is a synchronous exception (resolved by OS).
- **Bus contention** limits throughput when multiple masters compete.
- **DMA reduces CPU load** but doesn't speed up the transfer itself (data still goes through bus).

---

## 3. Short Notes

```
I/O ADDRESSING
 memory-mapped: load/store
 port-mapped: special IN/OUT

I/O METHODS
 programmed (polling): CPU loops on status
 interrupt-driven: device signals CPU
 DMA: controller transfers directly

INTERRUPTS
 maskable / NMI / software / exception / external
 vectored (table) / polled / daisy-chain / PIC

INTERRUPT HANDLING
 1. assert IRQ
 2. finish current instr
 3. save context (PC, regs)
 4. vector → ISR
 5. ISR runs
 6. RTI

DMA
 setup: src, dst, count, dir
 transfer: DMA does data
 modes:
   burst: hold bus
   cycle-steal: 1 cycle at a time
   transparent: when CPU idle

BUS ARBITRATION
 daisy-chain (priority by chain)
 centralized (controller)
 distributed
 polling

BUS BANDWIDTH = width × frequency

DISK ACCESS (preview)
 seek + rotational + transfer
```

---

## 4. Formulas / Tricks

| # | Formula / Rule | Memorize Cold? |
|---|---|---|
| 1 | Programmed I/O loop time = polling overhead | ✅ |
| 2 | Interrupt time = save + vector + ISR + restore | ✅ |
| 3 | DMA = setup + transfer (parallel with CPU) + interrupt | ✅ |
| 4 | DMA modes: burst, cycle-stealing, transparent | ✅ |
| 5 | Memory-mapped vs port-mapped I/O | ✅ |
| 6 | Vectored interrupts faster than polled | ✅ |
| 7 | NMI cannot be masked | ✅ |
| 8 | Bus bandwidth = width × frequency | ✅✅ |
| 9 | Daisy chain priority by chain order | ✅ |
| 10 | Disk access = seek + rotation + transfer | ✅ |

### Tricks

- **DMA vs CPU transfer:** DMA frees CPU but doesn't reduce bus traffic.
- **For mixed workload:** burst DMA stalls CPU; cycle-stealing balances.
- **Interrupt latency:** count cycles for save+ISR+restore.
- **Bus contention:** if both DMA and CPU need bus, throughput halves under cycle-stealing.
- **Memory-mapped I/O simplicity:** uses standard cache and addressing — no extra instructions.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Which I/O method is fastest for bulk data?
**Solution.** DMA.

### Q2. (GATE CSE 2014)
In cycle-stealing DMA, what happens?
**Solution.** DMA grabs one bus cycle, then yields to CPU.

### Q3. (GATE CSE 2018)
Memory-mapped I/O:
**Solution.** Uses memory addresses for I/O registers; standard load/store work.

### Q4. (GATE CSE 2008)
Vectored interrupts use:
**Solution.** Vector table indexed by interrupt number to find ISR address.

### Q5. (GATE CSE 2010)
Bus bandwidth = 32 bits × 100 MHz = ?
**Solution.** 4 B × 100 M = 400 MB/s.

### Q6. (GATE CSE 2015)
NMI is:
**Solution.** Non-maskable interrupt; used for critical events.

### Q7. (GATE CSE 2013)
DMA setup phase requires:
**Solution.** Source, destination, count, direction.

### Q8. (GATE CSE 2007)
Daisy-chained interrupt priority:
**Solution.** First device in chain has highest priority.

### Q9. (GATE CSE 2003)
Disk access time:
**Solution.** Seek + rotational + transfer.

### Q10. (GATE CSE 2009)
Polling vs interrupt: when is polling preferred?
**Solution.** When device almost always ready (overhead of interrupt > polling).

### Q11. (GATE CSE 2019)
DMA controller transfers 100 MB at 50 MB/s. Time?
**Solution.** 2 s.

### Q12. (GATE CSE 2020)
Burst-mode DMA effect on CPU:
**Solution.** CPU is held off bus until transfer completes (high latency).

### Q13. (GATE CSE 2021)
Interrupt latency depends on:
**Solution.** Pipeline state, save/restore overhead, ISR length.

### Q14. (GATE CSE 2016)
Bus arbitration: distributed scheme:
**Solution.** Devices arbitrate among themselves without central controller.

### Q15. (GATE CSE 2011)
For 1 MB transfer at 400 MB/s + 10 µs setup, total time?
**Solution.** 1/400 + 10 µs = 2.5 ms + 10 µs ≈ 2.51 ms.

---

## 6. Practice Questions (20+)

### Easy

**P1.** State 3 I/O methods.

**P2.** What is DMA?

**P3.** Memory-mapped vs port-mapped I/O.

**P4.** Define ISR.

**P5.** What is NMI?

**P6.** Bus bandwidth for 64-bit bus at 200 MHz?

**P7.** Vectored interrupts: advantage?

**P8.** DMA modes — name 3.

**P9.** Disk access time components?

**P10.** Cycle-stealing impact on CPU?

### Medium

**P11.** Interrupt overhead = 50 cycles, 100K interrupts/s, CPU at 1 GHz. % CPU time?

**P12.** Compute DMA transfer time for 1 GB at 200 MB/s.

**P13.** Polling overhead 10 cycles, 1000 polls/s, CPU 1 GHz. CPU usage?

**P14.** Memory-mapped I/O vs port-mapped: pros and cons?

**P15.** Compute interrupt latency for 200 cycles save + 1000 cycles ISR + 200 cycles restore at 1 GHz.

**P16.** DMA setup 100 cycles + transfer 1 ms. Total?

**P17.** Daisy-chain bus arbitration: maximum priority?

**P18.** Compute bus utilization for 80 MB/s DMA on 400 MB/s bus.

**P19.** Why use cycle-stealing over burst DMA?

**P20.** What's the difference between trap and interrupt?

### Hard

**P21.** Compute total time: CPU does 10ms work + DMA transfer 100 MB at 200 MB/s + ISR 10 µs.

**P22.** A computer has 4 I/O devices on shared IRQ. Vector mechanism cost?

**P23.** Calculate disk access time: 10ms seek + 5ms rotation + 1ms transfer.

**P24.** A burst DMA holds bus for 100 µs every 1 ms. CPU bandwidth lost?

**P25.** Why is DMA more efficient than CPU-driven for bulk transfers?

**P26.** A page fault is a synchronous interrupt — explain its handling.

**P27.** Compute memory bandwidth needed for 1 Gb/s network card.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | polling, interrupt, DMA | direct |
| P2 | direct memory access | direct |
| P3 | memory-mapped uses memory addresses | direct |
| P4 | interrupt service routine | direct |
| P5 | non-maskable | direct |
| P6 | 1.6 GB/s | width × freq |
| P7 | direct ISR address | direct |
| P8 | burst, cycle-stealing, transparent | direct |
| P9 | seek + rotation + transfer | direct |
| P10 | one cycle stolen at a time | direct |
| P11 | 50·100K = 5M cycles/s = 0.5% | direct |
| P12 | 5 s | direct |
| P13 | 10·1K = 10K cycles/s = 0.001% | direct |
| P14 | MMIO simple addressing; port-mapped separate space | direct |
| P15 | 1400 ns = 1.4 µs | direct |
| P16 | 1.0001 ms | direct |
| P17 | first device in chain | direct |
| P18 | 80/400 = 20% | direct |
| P19 | CPU still gets bus periodically | direct |
| P20 | trap is software, interrupt is hardware | direct |
| P21 | DMA dominates: 0.5 s + small overhead | direct |
| P22 | needs PIC or polling overhead | direct |
| P23 | 16 ms | direct |
| P24 | 10% (100µs / 1ms) | direct |
| P25 | CPU not in transfer loop | direct |
| P26 | save state, OS handles, restore | direct |
| P27 | 125 MB/s | conversion |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing polling and interrupt | Polling is CPU loop; interrupt is hardware signal. |
| 2 | Forgetting DMA setup time | Total = setup + transfer + completion. |
| 3 | Treating NMI as maskable | NMI can't be disabled. |
| 4 | Memory-mapped I/O needs special instructions | No — standard load/store. |
| 5 | DMA always faster (myth) | Setup overhead can dominate small transfers. |
| 6 | Burst-mode DMA causes no CPU stall | It does — CPU yields entire bus. |
| 7 | Vectored vs polled distinction | Vector → direct lookup; polled → scan. |
| 8 | Bus bandwidth ignoring overhead | Real bandwidth < theoretical. |
| 9 | Synchronous bus = always faster | Async bus has handshake reliability. |
| 10 | DMA without bus arbitration | DMA needs to arbitrate with CPU. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Best I/O method for bulk data" | DMA. |
| "Best I/O method for slow human input" | Interrupt. |
| "Best I/O method for very fast device always ready" | Polling. |
| "DMA mode minimizing CPU stall" | Cycle-stealing or transparent. |
| "DMA mode maximizing throughput" | Burst. |
| "Interrupt cannot be disabled" | NMI. |
| "Daisy-chain priority" | First device wins. |
| "Memory-mapped I/O instructions" | Standard load/store. |
| "Port-mapped I/O instructions" | IN, OUT (x86). |
| "Bus bandwidth calc" | width × freq. |

---

## 9. Quick Revision

```
I/O METHODS
 programmed (polling): CPU loops
 interrupt-driven: device signals
 DMA: controller bulk transfer

I/O ADDRESSING
 memory-mapped (load/store)
 port-mapped (IN/OUT)

INTERRUPT TYPES
 maskable / NMI / software / exception / external

INTERRUPT HANDLING
 vectored / polled / daisy-chain / PIC

DMA
 setup: src, dst, count, dir
 transfer: DMA owns bus
 modes:
  burst — CPU stalled
  cycle-stealing — alternate
  transparent — only when CPU idle

BUS
 sync vs async
 bandwidth = width × freq
 arbitration: daisy / centralized / distributed / polling

DISK = seek + rotation + transfer
```
