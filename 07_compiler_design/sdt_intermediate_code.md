# Syntax-Directed Translation & Intermediate Code

> Subject: Compiler Design
> GATE weight: **2–3 marks** every year. Attribute grammars, S/L-attributed, three-address code, type systems.

---

## 1. Concept Explanation

### 1.1 Syntax-Directed Definition (SDD)

A **CFG augmented with attributes** for non-terminals + rules to compute them.

Two attribute types:

| Type | Computed |
|---|---|
| **Synthesized** | From children's attributes |
| **Inherited** | From parent and/or sibling attributes |

### 1.2 Synthesized Attributes

Computed by **bottom-up** evaluation. All values flow upward.

A grammar where every attribute is synthesized = **S-attributed**.

S-attributed SDDs work cleanly with **bottom-up parsers (LR)**.

**Example:** `E → E + T { E.val = E.val + T.val }`.

### 1.3 Inherited Attributes

Computed using parent/sibling values. Flow downward or sideways.

**Example:** type information propagated from declaration to identifier.

### 1.4 L-Attributed Definition

Each inherited attribute on RHS of A → X₁ X₂ … Xₙ depends only on:
- Inherited attributes of A (parent).
- Synthesized **or** inherited attributes of X₁, …, Xⱼ₋₁ (siblings to the left).
- Attributes of Xⱼ itself.

L-attributed = computable in **single left-to-right pass**.

S-attributed ⊆ L-attributed.

### 1.5 SDT (Syntax-Directed Translation Scheme)

CFG with **embedded actions** in productions. Actions are code fragments executed during parsing.

### 1.6 SDT for LR

If actions are at end of rules (post-reduce) → SDT is S-attributed.

For inherited attributes in LR: insert markers (auxiliary non-terminals).

### 1.7 SDT for LL

LL parsers process left-to-right. L-attributed schemes work directly.

### 1.8 Annotated Parse Tree

Parse tree with attribute values evaluated. Useful for visualization.

### 1.9 Symbol Table

Maps identifier → attributes (type, scope, address).

**Operations:** insert, lookup, delete, scope management.

**Scope handling:** stack of tables (one per scope level).

### 1.10 Type Checking

**Type system** assigns types to expressions / functions.

**Static typing:** types determined at compile time (C, Java).
**Dynamic typing:** at runtime (Python, JS).

**Type equivalence:**
- **Structural:** same shape.
- **Name:** same declared name.

**Type inference:** deduce types automatically.

### 1.11 Intermediate Representation (IR)

| IR | Description |
|---|---|
| **Three-address code (3AC)** | Instructions of form `x = y op z` |
| **Quadruples** | (op, arg1, arg2, result) |
| **Triples** | Reference operands by their position |
| **Indirect triples** | List of pointers to triples |
| **Postfix notation** | Operator after operands |
| **Abstract Syntax Tree (AST)** | Tree-based |
| **Control Flow Graph (CFG)** | Basic blocks + edges |

### 1.12 Three-Address Code

Each statement has at most three addresses (locations).

**Example:** `a = b + c * d` becomes:
```
t1 = c * d
t2 = b + t1
a = t2
```

### 1.13 Common 3-Address Instructions

| Form | Meaning |
|---|---|
| `x = y op z` | binary op |
| `x = op y` | unary |
| `x = y` | copy |
| `goto L` | unconditional jump |
| `if x relop y goto L` | conditional |
| `param x` | actual parameter |
| `call p, n` | call with n args |
| `return y` | return |
| `x = y[i]` | indexed access |
| `x[i] = y` | indexed assignment |
| `*p = y` | indirect store |
| `x = *p` | indirect load |

### 1.14 Quadruples vs Triples

**Quadruples:**
```
(op, arg1, arg2, result)
(*, c, d, t1)
(+, b, t1, t2)
(=, t2, _, a)
```

**Triples:**
```
(0) (*, c, d)
(1) (+, b, (0))
(2) (=, a, (1))
```

Triples reference earlier triples by index — saves memory but harder to optimize.

**Indirect triples:** array of pointers to triples.

### 1.15 Boolean Expressions

Two methods:
1. **Numerical:** evaluate to 0/1.
2. **Short-circuit (jumping code):** generate jumps directly.

For control flow (if, while, for), generate labels and conditional gotos.

### 1.16 Control Flow Translation

**if E then S₁ else S₂:**
- Generate code for E (sets a flag or short-circuits).
- Conditional jump to S₂.
- Code for S₁; jump to end.
- Label S₂; code for S₂.
- End label.

**while E do S:**
- Begin label.
- Code for E; conditional jump to end.
- Code for S.
- Jump to begin.
- End label.

### 1.17 Backpatching

For one-pass code generation: when generating code for boolean expressions and control flow, addresses of jumps may not yet be known. Use **lists of jumps** to be filled in later.

Common operation: `backpatch(L, target)` writes target into all instructions in list L.

### 1.18 Translation of Arrays

For `A[i]`, address = base + i · size.

### 1.19 Procedure Calls

**Activation record / stack frame:** holds parameters, local variables, return address, saved registers.

Translation generates:
- `param` instructions per argument.
- `call p, n` for n parameters.
- Callee returns via `return`.

### 1.20 Type Synthesis Example

```
E → E + T  { E.type = if E.type == int and T.type == int then int else error }
```

### 1.21 SDT Implementation

For LR parser:
- Place actions at end of productions (S-attributed).
- For inherited, insert markers.

For top-down LL: process actions in left-to-right order.

> **Summary:** SDD = grammar + attributes. S-attributed (synthesized only) works with LR; L-attributed includes left-only inherited. IR forms include 3AC, quadruples, triples. Use backpatching for one-pass code generation.

---

## 2. Important Points

- **Synthesized attributes** flow up; **inherited** flow down/across.
- **S-attributed** = synthesized only.
- **L-attributed** = synthesized + restricted inherited.
- S-attributed ⊊ L-attributed.
- S-attributed evaluable bottom-up (with LR).
- L-attributed evaluable in single L-to-R pass (with LL or augmented LR).
- **Three-address code** has ≤ 3 addresses per instruction.
- **Quadruples** are easier to optimize than triples.
- **Backpatching** allows single-pass codegen for boolean / control flow.
- **Annotated parse tree** has attribute values at each node.
- **Symbol table** is essential for semantic analysis.
- **Static typing** vs **dynamic typing** affects runtime checks.
- **Type checking** verifies type rules; can be static or dynamic.
- **AST** is more compact than parse tree, dropping unnecessary structure.

---

## 3. Short Notes

```
SDD = CFG + attributes + rules
ATTRIBUTES
 synthesized: from children
 inherited: from parent/siblings

S-attributed: synthesized only
 evaluable with LR

L-attributed: + restricted inherited
 evaluable in single L-to-R pass

SDT: CFG with embedded actions

ANNOTATED PARSE TREE: tree with attribute values

SYMBOL TABLE
 maps identifier → attributes
 scope: stack of tables

TYPE CHECKING
 static (compile time) / dynamic (runtime)
 structural / name equivalence
 type inference

INTERMEDIATE CODE
 3AC: x = y op z
 quadruples: (op, a1, a2, result)
 triples: position-referenced
 indirect triples: array of triple pointers
 AST: parse tree pruned
 CFG: basic blocks + edges

3AC INSTRUCTIONS
 x = y op z; x = op y; x = y
 goto L; if x relop y goto L
 param x; call p, n; return y
 x = y[i]; x[i] = y
 *p = y; x = *p

BOOLEAN EVAL
 numerical (0/1)
 short-circuit (jumping)

BACKPATCHING
 lists of pending jumps
 fill targets later

CONTROL FLOW TRANSLATION
 if-else: jumps + labels
 while: begin label, conditional jump to end
 for: similar

ARRAYS: address = base + i · size
PROCEDURE CALL: param + call + return
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Synthesized = from children | ✅✅ |
| 2 | Inherited = from parent/siblings | ✅✅ |
| 3 | S-attributed evaluable bottom-up (LR) | ✅✅ |
| 4 | L-attributed evaluable L-to-R | ✅ |
| 5 | 3AC: x = y op z (max 3 addresses) | ✅✅ |
| 6 | Quadruples: (op, a1, a2, result) | ✅ |
| 7 | Triples: (op, arg1, arg2) referenced by index | ✅ |
| 8 | Backpatching for one-pass codegen | ✅ |
| 9 | Static vs dynamic typing | ✅ |
| 10 | Type equivalence: structural vs name | ✅ |
| 11 | AST vs parse tree | ✅ |

### Tricks

- **Identify S-attributed** by checking only synthesized attributes.
- **L-attributed allows** inherited from previously-processed siblings.
- **Convert SDD to SDT:** place actions to ensure correct evaluation order.
- **For 3AC:** introduce temporary variables for intermediate results.
- **Quadruples preferred** for optimization.
- **Triples save memory** but complicate optimization (renaming changes indices).

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
S-attributed grammar uses:
**Solution.** Only synthesized attributes.

### Q2. (GATE CSE 2014)
L-attributed allows:
**Solution.** Inherited from left siblings.

### Q3. (GATE CSE 2018)
3-address code form:
**Solution.** x = y op z.

### Q4. (GATE CSE 2008)
Quadruples vs triples:
**Solution.** Quadruples easier to optimize.

### Q5. (GATE CSE 2010)
Backpatching is for:
**Solution.** Filling jump targets later in one-pass codegen.

### Q6. (GATE CSE 2015)
S-attributed evaluable with:
**Solution.** Bottom-up parsing (LR).

### Q7. (GATE CSE 2013)
Symbol table operations:
**Solution.** Insert, lookup, delete, scope management.

### Q8. (GATE CSE 2007)
Static typing vs dynamic:
**Solution.** Compile-time vs runtime type checking.

### Q9. (GATE CSE 2003)
AST vs parse tree:
**Solution.** AST drops syntactic detail; more compact.

### Q10. (GATE CSE 2009)
Triples reference operands via:
**Solution.** Their position (index).

### Q11. (GATE CSE 2019)
For while-do, IR uses:
**Solution.** Begin label, conditional jump, body, jump back.

### Q12. (GATE CSE 2020)
Synthesized attribute example:
**Solution.** value of expression in arithmetic grammar.

### Q13. (GATE CSE 2021)
Inherited attribute example:
**Solution.** Type info passed from declaration to identifiers.

### Q14. (GATE CSE 2016)
Annotated parse tree:
**Solution.** Parse tree with attribute values evaluated.

### Q15. (GATE CSE 2011)
SDT for LR:
**Solution.** Actions at end of productions (S-attributed); markers for inherited.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define SDD.

**P2.** Synthesized vs inherited?

**P3.** S-attributed grammar example.

**P4.** L-attributed allows what?

**P5.** Three-address code form?

**P6.** Quadruples format?

**P7.** What is backpatching?

**P8.** What's an AST?

**P9.** Static vs dynamic typing?

**P10.** Define annotated parse tree.

### Medium

**P11.** Compute 3AC for `a = b + c * d - e / f`.

**P12.** Convert SDT for `E → E + T` to action form.

**P13.** Backpatch example for `if E then S₁`.

**P14.** Translate `while x < n do x = x + 1` to 3AC.

**P15.** Compute address of `A[i][j]` (row-major, m cols).

**P16.** Quadruples vs triples for `a = b + c * d`.

**P17.** Type checking rule for `E → E + T`.

**P18.** Show why some inherited attributes can't be evaluated bottom-up.

**P19.** Symbol table entry for variable.

**P20.** Generate 3AC for `if (x < y) then a = 1 else a = 0`.

### Hard

**P21.** Build annotated parse tree for arithmetic expression.

**P22.** Implement S-attributed SDT for desk calculator.

**P23.** Implement L-attributed SDT for type declaration.

**P24.** Backpatching for short-circuit boolean expressions.

**P25.** Compare 3AC, quadruples, triples for same expression.

**P26.** Type inference for polymorphic functions.

**P27.** Translate function call with parameter passing.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | grammar + attributes + rules | direct |
| P2 | from children vs parent/siblings | direct |
| P3 | E → E + T : E.val = E.val + T.val | direct |
| P4 | L-to-R inherited from siblings | direct |
| P5 | x = y op z | direct |
| P6 | (op, a1, a2, result) | direct |
| P7 | fill jump targets later | direct |
| P8 | abstract syntax tree | direct |
| P9 | compile-time vs runtime | direct |
| P10 | parse tree with attribute values | direct |
| P11 | t1 = c*d; t2 = e/f; t3 = b+t1; t4 = t3-t2; a = t4 | direct |
| P12 | { E.val = E1.val + T.val } at end | direct |
| P13 | jump to true label, code for S₁, label end | direct |
| P14 | trace control flow | direct |
| P15 | base + (i·m + j) · size | direct |
| P16 | trace both | direct |
| P17 | E.type = if both int then int else error | direct |
| P18 | bottom-up doesn't have parent info | direct |
| P19 | name, type, scope, offset | direct |
| P20 | conditional + branches + labels | direct |
| P21 | trace tree + attr | direct |
| P22 | classic | direct |
| P23 | inherited type passed to identifiers | direct |
| P24 | jumping code with backpatch | direct |
| P25 | trace each form | direct |
| P26 | unification (Hindley-Milner) | direct |
| P27 | param + call sequence | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confuse synthesized and inherited | Bottom-up vs top-down. |
| 2 | Treat L-attributed = bottom-up | L-attributed needs L-to-R order. |
| 3 | Use triples for optimization | Quadruples better. |
| 4 | 3AC with > 3 addresses | Decompose. |
| 5 | Forget backpatching for jumps | Necessary for one-pass. |
| 6 | Static vs dynamic typing confusion | Compile-time vs runtime. |
| 7 | Mix structural and name equivalence | Different. |
| 8 | AST = parse tree | AST is pruned. |
| 9 | Forget symbol table scope | Stack-based. |
| 10 | LR cannot evaluate L-attributed | Possible with markers. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Generate 3AC" | Decompose into temporaries. |
| "S-attributed" | Synthesized only. |
| "L-attributed" | + restricted inherited. |
| "Backpatching" | Boolean / control flow one-pass. |
| "Type checking" | Apply type rules. |
| "Quadruples vs triples" | Memory vs ease of optimization. |
| "Activation record" | Procedure call. |
| "Symbol table" | Scope management. |
| "AST" | Compact tree representation. |
| "Inherited attribute example" | Type passed from declaration. |

---

## 9. Quick Revision

```
SDD = CFG + attributes + rules
SYNTHESIZED: from children
INHERITED: from parent/siblings

S-ATTRIBUTED: synthesized only; LR-compatible
L-ATTRIBUTED: + restricted inherited; L-to-R pass
S ⊊ L

SDT: CFG + actions

INTERMEDIATE CODE
 3AC: x = y op z
 quadruples: (op, a1, a2, result)
 triples: indexed
 AST: pruned parse tree
 CFG: basic blocks

CONTROL FLOW
 if-else: jumps + labels
 while: begin + cond + body + jump

BACKPATCHING: fill jumps later

SYMBOL TABLE: identifier → attributes; scope stack

TYPE
 static / dynamic
 structural / name equiv
 inference (HM)

ARRAYS: base + i·size
PROCEDURE CALL: param + call + return
```
