# Machine Instructions & Addressing Modes

> Subject: Computer Organization & Architecture (COA)
> GATE weight: **2–3 marks** every year. Instruction formats, addressing modes, ISA design.

---

## 1. Concept Explanation

### 1.1 Instruction & ISA

An **instruction** = operation code (opcode) + operand specifications (registers, memory, immediate).
The **Instruction Set Architecture (ISA)** is the visible interface between hardware and software.

### 1.2 Instruction Format

```
| Opcode | Operand 1 | Operand 2 | Operand 3 |
```

Different ISAs use different organizations:

| Type | Form | Example |
|---|---|---|
| **3-address** | OP A, B, C → A ← B op C | RISC (MIPS, ARM) |
| **2-address** | OP A, B → A ← A op B | x86 |
| **1-address** | OP B → ACC ← ACC op B | accumulator-based |
| **0-address** | OP → top of stack op | stack machines (JVM bytecode) |

### 1.3 Number of Addresses Trade-off

More address bits ⇒ shorter programs but larger instructions.
Fewer address bits ⇒ longer programs (more loads/stores), shorter instructions.

| Format | Pros | Cons |
|---|---|---|
| 3-address | Compact code, fewer instructions | Wide instructions |
| 1-address (acc) | Simple hardware | More memory accesses |
| 0-address (stack) | Compact instructions | Longer programs |

### 1.4 Instruction Length

`Instruction length = Opcode bits + Σ (operand specifier bits)`

Operand specifiers may include addressing-mode bits.

**Example:** 16-bit instruction with 5-bit opcode and three 3-bit register operands needs 5 + 3·3 = 14 bits → 2 bits free (e.g., for addressing-mode flags).

### 1.5 Opcode Length

For k different operations: `⌈log₂ k⌉` opcode bits.
**Expanding opcode:** use shorter opcodes for instructions with more operands; longer for fewer (variable-length).

### 1.6 RISC vs CISC

| Feature | RISC | CISC |
|---|---|---|
| Instruction set | Small, simple | Large, complex |
| Format | Fixed-length | Variable-length |
| Addressing modes | Few | Many |
| Execution | One per cycle (mostly) | Multi-cycle |
| Registers | Many | Fewer |
| Examples | MIPS, ARM, RISC-V | x86, VAX |

### 1.7 Addressing Modes (the GATE workhorse)

How the CPU determines the location of an operand.

| Mode | Notation | EA = Effective Address | Use Case |
|---|---|---|---|
| **Immediate** | #X | n/a — operand is X | constants |
| **Register** | Rn | n/a — operand in register | fast access |
| **Direct (Absolute)** | [Addr] | EA = Addr | global variables |
| **Indirect** | [[Addr]] | EA = M[Addr] | pointer in memory |
| **Register Indirect** | [Rn] | EA = (Rn) | pointers |
| **Indexed** | X(Rn) | EA = X + (Rn) | arrays |
| **Base + Offset / Base-Indexed** | (Rn) + Rm | EA = (Rn) + (Rm) | array element |
| **Base + Index + Displacement** | X(Rn, Rm) | EA = X + (Rn) + (Rm) | mixed |
| **PC-relative** | X(PC) | EA = PC + X | branches |
| **Auto-increment** | (Rn)+ | EA = (Rn); Rn++ | sequential access |
| **Auto-decrement** | -(Rn) | Rn--; EA = (Rn) | stacks |
| **Stack** | implicit | top of stack | stack machines |

### 1.8 Execution of Each Mode

For each mode, the processor:
1. Decodes the addressing mode bits.
2. Fetches operand using the EA computation.
3. May increment/decrement registers (auto-modes).

**Cycle count:**
- Immediate: 0 memory accesses (operand in instruction).
- Register: 0 memory accesses.
- Direct: 1 memory access.
- Indirect: 2 memory accesses.
- Register-indirect / indexed / base+offset: 1 memory access.

### 1.9 Stack-Based vs Register-Based

**Stack machine:** zero-address instructions; operations work on top of stack.

```
PUSH A
PUSH B
ADD       ; A + B
PUSH C
MUL       ; (A+B) × C
```

**Register machine:** explicit operand registers.
```
LOAD R1, A
LOAD R2, B
ADD R3, R1, R2
LOAD R4, C
MUL R5, R3, R4
```

### 1.10 Conversion Between Notations

| Notation | Example for `(A+B)*C` |
|---|---|
| Infix | (A + B) * C |
| Prefix (Polish) | * + A B C |
| Postfix (Reverse Polish) | A B + C * |

**Postfix evaluation** uses a stack — LIFO.

### 1.11 Subroutine Call & Return

- **CALL/JSR**: pushes return address; jumps.
- **RET**: pops; jumps to stored address.
- **Stack frame** holds local variables, return address, saved registers.

### 1.12 Interrupts vs Branches

- **Branch:** programmatic, conditional/unconditional.
- **Interrupt:** asynchronous; current state saved; ISR runs.
- **Trap/Exception:** synchronous (e.g., divide by zero).

### 1.13 Common Instruction Types

| Type | Examples |
|---|---|
| Data transfer | LOAD, STORE, MOVE, PUSH, POP |
| Arithmetic | ADD, SUB, MUL, DIV |
| Logical | AND, OR, NOT, XOR |
| Shift / Rotate | SHL, SHR, ROL, ROR |
| Compare | CMP, TEST |
| Branch | BEQ, BNE, JMP, CALL, RET |
| Control | NOP, HALT |
| I/O | IN, OUT |

### 1.14 Endianness

- **Big-endian:** MSB at lowest address.
- **Little-endian:** LSB at lowest address.

For the 32-bit value `0x12345678` stored at address 100:

| Address | Big-endian | Little-endian |
|---|---|---|
| 100 | 12 | 78 |
| 101 | 34 | 56 |
| 102 | 56 | 34 |
| 103 | 78 | 12 |

> **Summary:** Master addressing modes (with EA formula and # of memory accesses), instruction format trade-offs, RISC vs CISC, postfix evaluation. Most PYQs are direct lookups + simple computations once you know the modes.

---

## 2. Important Points

- Number of operations = 2^(opcode bits).
- For variable-length opcodes, use **expanding opcode** technique.
- **Immediate addressing** is fastest (no memory access for operand).
- **Indirect** is slowest among standard modes (2 memory accesses).
- **PC-relative** is critical for **position-independent code**.
- **Stack machines** use postfix; convert any infix expression to postfix for stack evaluation.
- **Postfix evaluation:** read left-to-right; push operands; on operator, pop two and push result.
- Postfix conversion: shunting-yard algorithm or recursive descent.
- **MIPS** is a 3-address, fixed 32-bit, RISC ISA — common GATE reference.
- **Auto-increment / auto-decrement** simulate post-increment/pre-decrement in C pointers.
- **Effective Address (EA) formula** is the mode's defining identity.
- Indirect through a register doesn't access memory until use of the register's pointee.
- The number of memory accesses can be a tiebreaker when comparing addressing modes.
- Endianness affects byte-level reads/writes only — word-level is opaque.

---

## 3. Short Notes

```
INSTRUCTION FORMAT
 [opcode] [operand1] [operand2] [operand3]
 0/1/2/3 address forms

ADDRESS COUNT TRADE-OFF
 more addresses → fewer instructions, wider format
 fewer addresses → more instructions, narrow format

RISC vs CISC
 RISC: small, fixed, regular
 CISC: large, variable

ADDRESSING MODES (EA formula | # mem accesses)
 immediate: operand in instruction | 0
 register: in register | 0
 direct: EA = Addr | 1
 indirect: EA = M[Addr] | 2
 reg-indirect: EA = (Rn) | 1
 indexed: EA = X + (Rn) | 1
 base+offset: EA = (Rn) + (Rm) | 1
 base+index+disp: EA = X + (Rn) + (Rm) | 1
 PC-relative: EA = PC + X | 1
 auto-inc: EA = (Rn); Rn++ | 1
 auto-dec: Rn--; EA = (Rn) | 1

NOTATIONS
 infix:  (A+B)*C
 prefix: *+ABC
 postfix: AB+C*

POSTFIX EVAL via STACK
 push operands; op pops two

ENDIANNESS
 big: MSB at low addr
 little: LSB at low addr

INTERRUPTS / TRAPS / EXCEPTIONS
 async / sync events
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Instruction length = opcode + operands + mode bits | ✅ |
| 2 | k operations need ⌈log₂ k⌉ opcode bits | ✅ |
| 3 | n registers need ⌈log₂ n⌉ register bits | ✅ |
| 4 | Direct EA = Addr (1 access) | ✅✅ |
| 5 | Indirect EA = M[Addr] (2 accesses) | ✅✅ |
| 6 | Indexed EA = X + (Rn) (1 access) | ✅✅ |
| 7 | PC-relative EA = PC + X | ✅ |
| 8 | Auto-inc/dec for sequential / stack | ✅ |
| 9 | RISC fixed-length, CISC variable | ✅ |
| 10 | Postfix conversion + stack evaluation | ✅✅ |
| 11 | Endianness affects byte order | ✅ |

### Tricks

- **Infix → Postfix:** use a stack; on operand → output; on operator → pop higher/equal precedence ops then push.
- **Postfix evaluation count:** # operands = # operators + 1.
- **Counting instructions for an expression:** stack machine (postfix length) usually gives a lower bound.
- **Operand bits formula:** for instruction with addressing-mode bits, count: `opcode + n × (mode + register/address)`.
- **Memory access count:** sum across operands. Useful for cycle estimation.
- **Spotting RISC vs CISC trace:** fixed-length, simple, register-based ⇒ RISC.
- **Endianness pitfall:** mixing big/little can corrupt multi-byte values.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
A processor uses 32-bit instructions. The instruction format has a 6-bit opcode and 4 register operands. How many bits per register?
**Solution.** (32 − 6)/4 = 26/4 = 6.5 — must be integer; with 6 bits per register total = 30, leaving 2 bits unused (e.g., for mode).

### Q2. (GATE CSE 2014)
Postfix of (A + B) * (C − D) is:
**Solution.** AB+CD−*.

### Q3. (GATE CSE 2018)
A stack-based machine evaluates `A + B − C * D`. Number of stack operations?
**Solution.** Postfix: AB+CD*−. Operations: PUSH A, PUSH B, +, PUSH C, PUSH D, *, −. **7 ops** (4 pushes + 3 ops).

### Q4. (GATE CSE 2008)
With direct addressing, an instruction "LOAD A" requires:
**Solution.** 1 memory access for fetching operand at address A.

### Q5. (GATE CSE 2010)
Indirect addressing requires:
**Solution.** 2 memory accesses (read pointer, then read operand).

### Q6. (GATE CSE 2015)
A computer has 64 registers. # bits to specify a register?
**Solution.** log₂64 = 6.

### Q7. (GATE CSE 2013)
A processor has 32-bit address bus. Maximum addressable bytes?
**Solution.** 2³² = 4 GB.

### Q8. (GATE CSE 2007)
Convert prefix `+ A * B C` to infix:
**Solution.** A + (B * C).

### Q9. (GATE CSE 2003)
A 16-bit instruction has 5-bit opcode and 11 bits for two operands. With 64 registers, how many bits per memory address?
**Solution.** 6 register bits per operand (×2 = 12, exceeds 11) — so likely 1 register + 1 address; address bits = 11 − 6 = 5.

### Q10. (GATE CSE 2009)
RISC processors typically have:
**Solution.** Fixed-length instructions, large register file, simple addressing modes.

### Q11. (GATE CSE 2019)
A 4-byte integer 0x11223344 stored at address 100 in a little-endian machine. Byte at address 100?
**Solution.** 0x44 (LSB).

### Q12. (GATE CSE 2020)
Convert infix `A + B * C − D / E` to postfix:
**Solution.** ABC*+DE/−.

### Q13. (GATE CSE 2021)
PC-relative addressing is used because:
**Solution.** Position-independent code; branch targets relative to current PC.

### Q14. (GATE CSE 2016)
A CPU supports 50 distinct instructions. # opcode bits?
**Solution.** ⌈log₂ 50⌉ = 6.

### Q15. (GATE CSE 2011)
For autoincrement addressing, after fetch:
**Solution.** Register is incremented (typically by operand size).

---

## 6. Practice Questions (20+)

### Easy

**P1.** What's the EA in immediate addressing?

**P2.** # memory accesses in register addressing?

**P3.** Convert `A + B * C` to postfix.

**P4.** # opcode bits to support 32 operations.

**P5.** RISC has fixed or variable instruction length?

**P6.** A computer has 16 registers. # register bits?

**P7.** What does indirect addressing access?

**P8.** Maximum addressable memory with 24-bit address?

**P9.** Notation: `+AB` is which form?

**P10.** Stack machine uses how many operand addresses per instruction?

### Medium

**P11.** A 32-bit instruction has 8-bit opcode and 3 operands (each register). # bits per register if 64 registers?

**P12.** Infix `(A + B) * C / D − E` to postfix.

**P13.** Postfix `AB+C*D/E−` to infix.

**P14.** Compute # mem accesses for `MOV [R1], [R2]` (both indirect).

**P15.** A 3-address instruction has 24 total bits, opcode 6, register 5. # bits per register operand × 3 = 15. # remaining bits = 24 − 6 − 15 = 3 (mode).

**P16.** With 64 KB memory and 16-bit address, byte-addressable. # of words (16-bit) addressable?

**P17.** Infix to prefix: `A − B + C * D`.

**P18.** A computer's instructions have 16-bit length: 4-bit opcode + two 6-bit register operands. How many registers are addressable?

**P19.** Show stack content during evaluation of `AB+C*D−`.

**P20.** A program has 1000 instructions. Each takes 1.5 cycles average. CPU at 1 GHz. Execution time?

### Hard

**P21.** Design an instruction format for an ISA with 100 instructions, 32 registers, and an immediate-mode constant up to 16 bits. Total instruction length?

**P22.** Compute clock cycles for a stack-machine evaluation of `((A + B) * (C − D)) + E`.

**P23.** Translate `WHILE x < 10 DO x = x + 1` to RISC pseudo-assembly.

**P24.** Compute # of PC-relative branches if PC and target differ by ≤ ±2¹⁵.

**P25.** A CPU has 8-bit opcode. Some instructions have 0 operands, others have 1. How can opcode be expanded?

**P26.** Show that 0-address instructions correspond to postfix expression length.

**P27.** A processor uses 5-stage pipeline. How does instruction length affect fetch?

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | none — operand in instruction | direct |
| P2 | 0 | direct |
| P3 | ABC*+ | precedence |
| P4 | 5 | 2⁵ |
| P5 | fixed | RISC |
| P6 | 4 | log₂16 |
| P7 | pointer in memory | direct |
| P8 | 16 MB | 2²⁴ |
| P9 | prefix | direct |
| P10 | 0 | stack machine |
| P11 | 6 each, total 18; 32-8-18=6 mode bits | direct |
| P12 | AB+C*D/E− | precedence |
| P13 | (((A+B)*C)/D)−E | direct |
| P14 | 2 indirect = 4 mem accesses (2 each) + 1 store = depends on src/dest | direct |
| P15 | 3 mode bits | direct |
| P16 | 32K words (each = 2 bytes) | direct |
| P17 | +−AB*CD | prefix |
| P18 | 64 (2⁶) | direct |
| P19 | trace stack | direct |
| P20 | 1500 ns = 1.5 µs | direct |
| P21 | 7 (opcode) + 5×3 (registers, if 3-addr with reg) + 16 (imm) — varies; design choice | direct |
| P22 | postfix length: AB+CD−*E+ → 4 ops | direct |
| P23 | LOOP: CMP x,10; BGE END; ADD x,1; JMP LOOP; END: | RISC pseudo |
| P24 | 2¹⁶ = 65536 | direct |
| P25 | use longer opcodes for fewer-operand instructions | expanding opcode |
| P26 | each operator pops 2 pushes 1; expression of length k operators ⇒ k+1 operands | direct |
| P27 | fixed → simple fetch; variable → harder | RISC vs CISC |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting indirect uses 2 memory accesses | Count carefully. |
| 2 | Confusing prefix and postfix | Prefix: op first; postfix: op last. |
| 3 | Mixing endianness | Track byte order explicitly. |
| 4 | Treating PC-relative as absolute | EA = PC + X, not just X. |
| 5 | Forgetting auto-increment side effect | Register changes after access. |
| 6 | RISC = better always (myth) | Trade-offs depending on use. |
| 7 | Counting opcode bits without considering all instructions | ⌈log₂ k⌉. |
| 8 | Variable-length opcodes overlooked | Expanding opcode. |
| 9 | Big/little endian confusion in array indexing | Same value shows different bytes. |
| 10 | Operand count vs operand size | Two different things. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "# bits for opcode / register / address" | ⌈log₂ N⌉. |
| "Convert to postfix / prefix" | Use precedence + stack. |
| "Effective address calculation" | Look up addressing mode formula. |
| "Number of memory accesses" | Sum per operand by mode. |
| "RISC vs CISC characteristics" | Fixed-length / regular / many registers vs variable / complex / fewer. |
| "Stack machine evaluation" | Postfix order, pop two on operator. |
| "Indirect vs direct vs immediate" | 2 / 1 / 0 mem accesses. |
| "Instruction length design" | Opcode + operand bits + mode flags. |
| "PC-relative addressing" | Position independent. |
| "Endianness byte order" | Big = MSB first; little = LSB first. |

---

## 9. Quick Revision

```
INSTRUCTION = opcode + operand specs

ADDRESSING MODES (EA | # mem)
 immediate: in instr | 0
 register: in reg | 0
 direct: EA = Addr | 1
 indirect: EA = M[Addr] | 2
 reg-indirect: EA = (Rn) | 1
 indexed: EA = X + (Rn) | 1
 base+offset: (Rn) + (Rm) | 1
 PC-rel: EA = PC + X | 1
 auto-inc/dec: with side effect | 1

#OPS = ⌈log₂ k⌉

NOTATIONS
 infix → prefix → postfix
 stack-eval postfix:
   operands push, op pops 2 push 1

RISC vs CISC
 RISC: fixed, simple, regs
 CISC: variable, complex

ENDIAN
 big: MSB at low addr
 little: LSB at low addr

INTERRUPTS / TRAPS / EXCEPTIONS
 async / sync, ISR, return
```
