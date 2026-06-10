# I/O Systems & Protection

> Subject: Operating Systems
> GATE weight: **1–2 marks** every year. I/O subsystem, protection mechanisms, security basics.

---

## 1. Concept Explanation

### 1.1 I/O Hardware

CPU communicates with I/O devices via **device controllers** + **buses**.

| Component | Description |
|---|---|
| Device controller | Hardware that manages a device |
| Device driver | OS module that interfaces with controller |
| Bus | Communication channel (PCIe, USB, etc.) |

### 1.2 I/O Methods

(See [io_interface_dma.md](../03_computer_organization_architecture/io_interface_dma.md) for full COA-level treatment.)

| Method | CPU role |
|---|---|
| Polling | Busy-wait |
| Interrupt-driven | Notified when ready |
| DMA | Bulk transfer without CPU |

### 1.3 OS I/O Layers

```
Application
    │
System call interface
    │
Kernel I/O subsystem (buffering, caching, scheduling, error handling)
    │
Device drivers
    │
Device controllers
    │
Devices
```

### 1.4 Kernel I/O Services

| Service | Purpose |
|---|---|
| **Buffering** | Hold data between transfers |
| **Caching** | Speed access via memory |
| **Spooling** | Hold output until device ready (e.g., printers) |
| **Scheduling** | Order I/O requests |
| **Error handling** | Retry, log, notify |
| **Protection** | Restrict access |

### 1.5 Buffering Strategies

| Type | Description |
|---|---|
| **Single buffer** | One buffer between user and device |
| **Double buffer** | Two — overlap read/write |
| **Circular buffer** | Multiple, reused |

### 1.6 Spooling vs Buffering

- **Buffering:** synchronization within a single I/O.
- **Spooling:** queueing for later processing (printing).

### 1.7 Protection Goals

- Prevent unauthorized access.
- Isolate processes.
- Enforce access policies.

### 1.8 Mechanism vs Policy

- **Mechanism:** how protection is enforced.
- **Policy:** what is allowed.

Separation enables flexibility.

### 1.9 Domain of Protection

Set of <object, rights> pairs available to a process.

**Domain switching** = process changes its rights (e.g., setuid in Unix).

### 1.10 Access Matrix

Rows: domains (or subjects).
Columns: objects.
Cells: access rights (read, write, execute, etc.).

**Sparse matrix** → typically stored as:
- **Access Control List (ACL):** per object.
- **Capability list:** per subject.

### 1.11 Unix Permissions

`rwx rwx rwx` for owner / group / others.
- r: read.
- w: write.
- x: execute.

Plus special bits: setuid, setgid, sticky.

### 1.12 Capability vs ACL

| Capability | ACL |
|---|---|
| Per-subject | Per-object |
| Easy revocation per subject | Easy per-object check |
| Capabilities can be passed | ACL is centrally managed |

### 1.13 Hardware Protection

| Mode | Description |
|---|---|
| **User mode** | Restricted access |
| **Kernel mode** | Full access |
| **Mode bit** | CPU flag |

System calls switch modes.

### 1.14 Memory Protection

- **Base + limit registers:** check each address.
- **Paging:** access bits in PTE.
- **Segmentation:** segment-level rights.

### 1.15 Security Threats

| Threat | Description |
|---|---|
| **Trojan horse** | Hidden malicious code |
| **Trap door** | Backdoor in legitimate program |
| **Logic bomb** | Triggered by condition |
| **Virus** | Replicates, attaches to programs |
| **Worm** | Self-propagating |
| **DoS** | Denies service |
| **Buffer overflow** | Overwrite memory boundaries |
| **SQL injection** | Inject malicious SQL |

### 1.16 Authentication

| Type | Example |
|---|---|
| **Something you know** | Password, PIN |
| **Something you have** | Token, smart card |
| **Something you are** | Biometric |
| **Two-factor** | Combine 2+ of above |

### 1.17 Cryptography Basics

| Concept | Description |
|---|---|
| **Symmetric** | Same key (AES, DES) |
| **Asymmetric** | Public/private key (RSA, ECC) |
| **Hash** | One-way (SHA-256) |
| **MAC** | Message authentication |
| **Digital signature** | Asymmetric + hash |

### 1.18 Common Attacks

| Attack | Description |
|---|---|
| **Brute force** | Try all keys/passwords |
| **Dictionary** | Common passwords |
| **Replay** | Resend captured message |
| **Man-in-the-middle** | Intercept and modify |
| **Spoofing** | Pretend to be someone else |
| **Phishing** | Fake authentication |

### 1.19 Process Isolation

OS uses:
- Memory protection (paging, base+limit).
- User vs kernel mode.
- System call interface.
- Capability/ACL checks.

### 1.20 Privilege Separation

Run with minimum privileges (principle of least privilege).

E.g., web server starts as root (to bind port 80) then drops privileges.

### 1.21 Sandboxing

Restrict process to limited resources (modern OS, browser tabs).

### 1.22 Common GATE Topics

- Mode bit and system calls.
- ACL vs capability.
- Unix permissions.
- I/O methods (cross-link with COA).
- Buffer overflow basic.

> **Summary:** OS I/O subsystem provides buffering, caching, spooling, scheduling, error handling. Protection via access matrix (ACL or capability), user/kernel mode, memory protection. Security: cryptography, authentication, common attacks.

---

## 2. Important Points

- **Device driver** abstracts device specifics.
- **Buffering** decouples I/O speeds; **spooling** queues for shared device.
- **DMA** is for bulk transfers without CPU.
- **Mode bit** distinguishes user vs kernel.
- **System calls** switch modes; trap into kernel.
- **Access matrix** can be ACL (per-object) or capability (per-subject).
- **Unix permissions:** rwx for owner/group/other.
- **Setuid bit** runs program as owner.
- **Buffer overflow** is a common vulnerability.
- **Symmetric crypto** is faster; **asymmetric** for key exchange / signatures.
- **Hash functions** are one-way.
- **2FA** combines factors.
- **Sandboxing** limits damage.
- **Principle of least privilege** is fundamental.

---

## 3. Short Notes

```
I/O HARDWARE
 controller, driver, bus

I/O METHODS
 polling, interrupt, DMA

OS I/O LAYERS
 system call → kernel I/O → driver → controller → device

KERNEL I/O SERVICES
 buffering, caching, spooling, scheduling, error handling, protection

BUFFERING
 single, double, circular

SPOOLING vs BUFFERING

PROTECTION
 mechanism vs policy
 domains, access matrix
 ACL (per-object) vs capability (per-subject)

UNIX PERMISSIONS
 rwx rwx rwx
 setuid, setgid, sticky

HARDWARE PROTECTION
 user vs kernel mode
 mode bit
 base + limit
 PTE bits

SECURITY THREATS
 trojan, trapdoor, logic bomb,
 virus, worm, DoS, buffer overflow, SQL injection

AUTHENTICATION
 know / have / are
 2FA

CRYPTO
 symmetric (AES, DES)
 asymmetric (RSA, ECC)
 hash (SHA-256)
 MAC, signature

ATTACKS
 brute, dictionary, replay,
 MITM, spoofing, phishing

PROCESS ISOLATION
 memory protection, mode, syscall, ACL/capability

LEAST PRIVILEGE
SANDBOXING
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | I/O methods: polling / interrupt / DMA | ✅✅ |
| 2 | Kernel I/O services list | ✅ |
| 3 | ACL vs capability | ✅✅ |
| 4 | Mode bit: user vs kernel | ✅✅ |
| 5 | Unix rwx permissions | ✅✅ |
| 6 | Symmetric (AES) vs asymmetric (RSA) | ✅ |
| 7 | Hash one-way | ✅ |
| 8 | 2FA combines factors | ✅ |
| 9 | Buffer overflow bypasses memory | ✅ |
| 10 | Least privilege | ✅ |

### Tricks

- **For ACL vs capability:** ACL = per-object; capability = per-subject.
- **For Unix permission:** owner / group / others, each rwx.
- **For mode bit:** trap into kernel via system call.
- **For symmetric crypto:** fast but key distribution problem.
- **For asymmetric:** slower but solves key distribution.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
DMA is for:
**Solution.** Bulk I/O without CPU.

### Q2. (GATE CSE 2014)
Mode bit:
**Solution.** Distinguishes user and kernel mode.

### Q3. (GATE CSE 2018)
ACL vs capability:
**Solution.** ACL: per-object; capability: per-subject.

### Q4. (GATE CSE 2008)
Spooling example:
**Solution.** Print queue.

### Q5. (GATE CSE 2010)
Unix setuid:
**Solution.** Run program as file owner.

### Q6. (GATE CSE 2015)
Symmetric crypto example:
**Solution.** AES, DES.

### Q7. (GATE CSE 2013)
Asymmetric crypto example:
**Solution.** RSA.

### Q8. (GATE CSE 2007)
Hash function property:
**Solution.** One-way; collision-resistant.

### Q9. (GATE CSE 2003)
Trojan horse:
**Solution.** Program with hidden malicious payload.

### Q10. (GATE CSE 2009)
Two-factor authentication:
**Solution.** Combines 2 different factor types.

### Q11. (GATE CSE 2019)
Buffer overflow:
**Solution.** Overwrites adjacent memory.

### Q12. (GATE CSE 2020)
Principle of least privilege:
**Solution.** Process should have minimum needed privileges.

### Q13. (GATE CSE 2021)
Sandboxing purpose:
**Solution.** Limit access; isolate.

### Q14. (GATE CSE 2016)
System call:
**Solution.** Mode switch from user to kernel.

### Q15. (GATE CSE 2011)
Domain of protection:
**Solution.** Set of <object, rights>.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define device driver.

**P2.** I/O methods (3).

**P3.** Buffering vs spooling.

**P4.** Mode bit role.

**P5.** ACL vs capability.

**P6.** Unix rwx.

**P7.** Symmetric crypto example.

**P8.** Asymmetric crypto example.

**P9.** Hash function property.

**P10.** 2FA.

### Medium

**P11.** Detect race condition in I/O.

**P12.** ACL example.

**P13.** Capability example.

**P14.** Setuid use case.

**P15.** Buffer overflow defense.

**P16.** Compare AES vs RSA.

**P17.** Digital signature workflow.

**P18.** Least privilege example.

**P19.** Sandbox example.

**P20.** MITM attack.

### Hard

**P21.** Implement secure password storage.

**P22.** Privilege escalation prevention.

**P23.** Compare Unix permissions vs ACL.

**P24.** RSA signing scheme.

**P25.** Capability revocation strategy.

**P26.** OS sandbox implementation.

**P27.** Side-channel attack examples.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | OS module managing device | direct |
| P2 | polling, interrupt, DMA | direct |
| P3 | sync vs queue | direct |
| P4 | user/kernel | direct |
| P5 | per-object vs per-subject | direct |
| P6 | owner/group/other | direct |
| P7 | AES | direct |
| P8 | RSA | direct |
| P9 | one-way + collision-resistant | direct |
| P10 | combine factors | direct |
| P11 | unsynchronized buffer access | direct |
| P12 | rwx in NTFS | direct |
| P13 | object handle in capability list | direct |
| P14 | passwd command | direct |
| P15 | stack canaries, ASLR, NX bit | direct |
| P16 | speed vs key distribution | direct |
| P17 | hash + sign with private | direct |
| P18 | drop privileges | direct |
| P19 | browser tab | direct |
| P20 | intercept | direct |
| P21 | salted hash | direct |
| P22 | careful syscall design | direct |
| P23 | Unix limited; ACL flexible | direct |
| P24 | hash + RSA private key | direct |
| P25 | revoke per object via timestamp | direct |
| P26 | seccomp / namespaces | direct |
| P27 | timing, cache, power | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Polling = interrupt | Different. |
| 2 | DMA always faster | Setup overhead matters. |
| 3 | Kernel mode = user mode | Different privileges. |
| 4 | ACL = capability | Different perspectives. |
| 5 | Symmetric crypto for signatures | Use asymmetric. |
| 6 | Hash reversible | One-way only. |
| 7 | Setuid harmless | Security risk. |
| 8 | Buffer overflow benign | Major vulnerability. |
| 9 | 2FA = 2 passwords | Different factors. |
| 10 | Sandbox unbreakable | Has limits. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "I/O bulk transfer" | DMA. |
| "Device-OS interface" | Driver. |
| "Spooling example" | Print spooler. |
| "Mode bit" | User/kernel. |
| "ACL vs capability" | Object vs subject focus. |
| "Symmetric crypto" | AES/DES. |
| "Asymmetric crypto" | RSA/ECC. |
| "Hash" | SHA-256, one-way. |
| "Unix permissions" | rwx. |
| "Least privilege" | Minimum needed. |

---

## 9. Quick Revision

```
I/O METHODS
 polling / interrupt / DMA

OS I/O LAYERS
 syscall → kernel → driver → controller → device

KERNEL I/O SERVICES
 buffering, caching, spooling, scheduling, error, protection

ACCESS CONTROL
 access matrix
 ACL (per-object)
 capability (per-subject)

UNIX PERMISSIONS rwx (owner/group/other)
SETUID, SETGID, sticky

MODE BIT: user vs kernel
SYSCALL switches mode

CRYPTO
 symmetric (AES, DES)
 asymmetric (RSA, ECC)
 hash (SHA-256)
 MAC, signature

THREATS
 virus, worm, DoS, buffer overflow,
 SQL injection, MITM, phishing

AUTHENTICATION
 know / have / are
 2FA combines

LEAST PRIVILEGE; SANDBOXING

PROCESS ISOLATION
 memory + mode + syscall + ACL
```
