# Lexical Analysis & Parsing (LL, LR)

> Subject: Compiler Design
> GATE weight: **3–5 marks** every year. FIRST/FOLLOW, parse table construction, conflict detection.

---

## 1. Concept Explanation

### 1.1 Compiler Phases

```
Source code
    │
    ▼
Lexical Analysis (Lexer)         → tokens
    │
    ▼
Syntax Analysis (Parser)         → parse tree / AST
    │
    ▼
Semantic Analysis                → annotated AST
    │
    ▼
Intermediate Code Generation     → 3-address code, etc.
    │
    ▼
Code Optimization
    │
    ▼
Code Generation                  → target code
```

Plus: **symbol table** and **error handler** across all phases.

### 1.2 Lexical Analysis

**Tokens:** smallest meaningful units (identifier, keyword, number, operator, punctuation).

**Lexeme:** actual character sequence matched.
**Pattern:** rule (regex) defining valid lexemes for a token.

**Lexer = DFA** simulating union of regexes.

**Implementation:** tools like `lex` / `flex` automate.

### 1.3 Tokens vs Symbols

| Term | Example |
|---|---|
| Token | `<id, "x">`, `<num, "42">` |
| Lexeme | "x", "42", "while" |
| Pattern | `[a-zA-Z_][a-zA-Z0-9_]*` for identifier |

### 1.4 Parsing — Top-Down vs Bottom-Up

| Approach | Direction | Examples |
|---|---|---|
| **Top-down** | Start symbol → input | Recursive descent, LL(k), Predictive |
| **Bottom-up** | Input → start symbol | LR(0), SLR, LALR, LR(1), Operator precedence |

### 1.5 Recursive Descent Parsing

Each non-terminal becomes a function. Recursive calls match the grammar.

May require **backtracking** for ambiguous productions, unless grammar is LL(1).

### 1.6 LL(k) Parsing

**LL(k):** Left-to-right input, Leftmost derivation, k tokens lookahead.

**LL(1):** lookahead of 1 token. Most common for top-down.

**Conditions for LL(1) grammar:**
- No left recursion.
- No two productions share a common prefix (left-factored).
- For A → α | β: FIRST(α) ∩ FIRST(β) = ∅.
- If ε ∈ FIRST(α), then FIRST(β) ∩ FOLLOW(A) = ∅.

### 1.7 FIRST and FOLLOW Sets

**FIRST(α):** set of terminals that begin some string derivable from α.

```
FIRST(terminal a) = {a}
FIRST(ε) = {ε}
FIRST(X Y₁ Y₂ … Yₙ):
  add FIRST(Y_i) for first i where ε ∉ FIRST(Y_{i-1})
  if ε ∈ FIRST of all, add ε
```

**FOLLOW(A):** set of terminals that can immediately follow A in some sentential form.

```
FOLLOW(S) ⊇ {$}  (end-marker)
For A → αBβ: FOLLOW(B) ⊇ FIRST(β) − {ε}
For A → αB or A → αBβ with ε ∈ FIRST(β):
  FOLLOW(B) ⊇ FOLLOW(A)
```

### 1.8 LL(1) Parse Table

For each production A → α:
- For each terminal a ∈ FIRST(α): M[A, a] = A → α.
- If ε ∈ FIRST(α): for each b ∈ FOLLOW(A): M[A, b] = A → α.

**Conflict** in M[A, a] → grammar not LL(1).

### 1.9 Bottom-Up Parsing

Build parse tree from leaves. Use **stack** to track shifts/reduces.

| Action | Description |
|---|---|
| **Shift** | Move next input token onto stack |
| **Reduce** | Replace rhs of production on stack top with lhs |
| **Accept** | Start symbol on stack and input consumed |
| **Error** | Conflict |

### 1.10 LR(k) Parsing

**LR(k):** Left-to-right input, Rightmost derivation in **reverse**, k tokens lookahead.

LR family (in increasing power):
- **LR(0):** no lookahead.
- **SLR(1):** uses FOLLOW for lookahead.
- **LALR(1):** merged LR(1) states.
- **LR(1):** full lookahead.

**Power:** LR(0) ⊆ SLR(1) ⊆ LALR(1) ⊆ LR(1) ⊆ LR(k).

### 1.11 LR Items

**LR(0) item:** A → α • β (dot indicates parsing position).

**LR(1) item:** A → α • β, a (with lookahead a).

### 1.12 Building LR Parse Tables

1. Compute closure / goto for items.
2. Construct DFA of items (canonical collection).
3. Fill ACTION + GOTO tables.

**Conflicts:**
- **Shift-reduce conflict:** can shift or reduce.
- **Reduce-reduce conflict:** two reductions possible.

### 1.13 Comparison Table

| Parser | States (typical) | Power | Comments |
|---|---|---|---|
| LR(0) | smallest | weakest | reduce always, no lookahead |
| SLR(1) | same as LR(0) | medium | uses FOLLOW |
| LALR(1) | same as LR(0) | strong | merges LR(1) states |
| LR(1) | largest | strongest | full lookahead |

LALR(1) is most practical (yacc, bison).

### 1.14 Operator Precedence Parsing

For operator grammars (no ε, no two adjacent non-terminals).

Use precedence relations <·, =·, ·>.

### 1.15 Ambiguous Grammars

Often handled in parser via precedence/associativity rules instead of grammar rewriting.

### 1.16 Eliminating Left Recursion

Left recursion: A → Aα | β.
Rewrite as:
```
A → β A'
A' → α A' | ε
```

### 1.17 Left Factoring

Common prefix factoring:
```
A → αβ | αγ
becomes:
A → α A'
A' → β | γ
```

### 1.18 Properties of LL vs LR

| Property | LL(1) | LR(1) |
|---|---|---|
| Direction | top-down | bottom-up |
| Derivation | leftmost | rightmost (reverse) |
| Left recursion | ❌ | ✅ |
| Left factoring | required | may not be |
| Power | smaller | larger |

LR(1) accepts ⊃ LL(1).

### 1.19 Common LL(1) Failures

- Left recursion.
- Common prefix.
- Ambiguity.

Not all CFGs are LL(1) or LR(k). Some CFLs are not even DCFL (need nondeterminism).

### 1.20 Error Recovery

**Panic mode:** skip until known synchronizing token.
**Phrase level:** local correction.
**Error productions:** grammar augmented with error rules.
**Global correction:** find minimum-cost correction.

> **Summary:** Lexer = DFA over regex. Parsers split into top-down (LL(1) needs FIRST/FOLLOW) vs bottom-up (LR family by power). Master FIRST/FOLLOW computation, LL(1) parse table, LR(0)/SLR/LALR conflict detection.

---

## 2. Important Points

- **Lexer = DFA** for regex of token patterns.
- **LL(1)** = top-down, 1 lookahead.
- **LR(1)** = bottom-up, 1 lookahead.
- **LL(k) grammars cannot have left recursion.**
- **LL grammars must be left-factored.**
- LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ LR(1).
- LALR(1) is **most practical**; same states as LR(0)/SLR.
- **FIRST and FOLLOW** are key for LL(1).
- **LL(1) conflict** = same cell has two productions.
- **Shift-reduce / Reduce-reduce conflicts** indicate non-LR.
- **Operator precedence** parsers don't handle all CFLs.
- Ambiguous grammars typically not LL or LR; resolve via precedence rules.
- **Recursive descent = LL(1)** without backtracking.
- LR can handle **left-recursive** grammars; LL cannot.
- Some CFLs are **not** LR(k) for any k.

---

## 3. Short Notes

```
COMPILER PHASES
 lex → parse → semantic → IR → opt → codegen
 + symbol table + error handling

LEXER = DFA

TOKEN: <type, value>; LEXEME: text; PATTERN: regex

PARSING
 top-down: LL(k), recursive descent
 bottom-up: LR(0), SLR, LALR, LR(1)

LL(1) CONDITIONS
 no left recursion
 left-factored
 FIRST(α) ∩ FIRST(β) = ∅
 ε in FIRST(α) ⇒ FIRST(β) ∩ FOLLOW(A) = ∅

FIRST AND FOLLOW
 FIRST(terminal) = self
 FIRST(X Y₁ … Yₙ): cumulate, ε if all
 FOLLOW(S) ⊇ {$}
 A → αBβ: FOLLOW(B) ⊇ FIRST(β) − {ε}
 A → αB: FOLLOW(B) ⊇ FOLLOW(A)

LL(1) PARSE TABLE
 cell M[A, a] = A → α
 conflict ⇒ not LL(1)

BOTTOM-UP
 stack + shift/reduce/accept/error
 LR(0): no lookahead
 SLR(1): uses FOLLOW
 LALR(1): merged LR(1) states
 LR(1): full lookahead
 LR(0) ⊊ SLR(1) ⊊ LALR(1) ⊊ LR(1)

LR ITEMS: A → α • β (LR(0)) ; with lookahead (LR(1))

CONFLICTS
 shift-reduce: ambiguous
 reduce-reduce: two reductions

ELIMINATE LEFT RECURSION
 A → Aα | β  →  A → β A', A' → α A' | ε

LEFT FACTOR
 A → αβ | αγ  →  A → α A', A' → β | γ

LL vs LR
 LL: leftmost; LR: rightmost-reverse
 LR handles left recursion; LL doesn't
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | LL(1) conflict-free check | ✅✅ |
| 2 | Left recursion elimination procedure | ✅✅ |
| 3 | Left factoring procedure | ✅✅ |
| 4 | FIRST and FOLLOW algorithms | ✅✅✅ |
| 5 | LR power: LR(0) ⊊ SLR ⊊ LALR ⊊ LR(1) | ✅✅ |
| 6 | LL(1) ⊆ LR(1); LR strictly stronger | ✅✅ |
| 7 | LR can handle left recursion | ✅✅ |
| 8 | Conflict in LL(1) table → not LL(1) | ✅✅ |
| 9 | Shift-reduce conflict in LR | ✅ |
| 10 | LALR same # states as LR(0) | ✅ |
| 11 | Operator precedence: limited grammar form | ✅ |

### Tricks

- **For LL(1) test:** check if grammar passes 4 conditions (no left rec, factored, FIRST disjoint, FOLLOW check).
- **Build FIRST/FOLLOW iteratively:** repeat until stable.
- **Use parse table to detect LL(1) failures.**
- **LR(0) reduce-conflicts often resolved by SLR's FOLLOW.**
- **Identify LALR conflicts:** check merging of LR(1) states.
- **Eliminate ambiguity** for if-else: associate else with nearest if.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Lexer is implemented using:
**Solution.** DFA.

### Q2. (GATE CSE 2014)
LL(1) grammar excludes:
**Solution.** Left recursion and unfactored prefixes.

### Q3. (GATE CSE 2018)
LR power ranking:
**Solution.** LR(0) ⊊ SLR(1) ⊊ LALR(1) ⊊ LR(1).

### Q4. (GATE CSE 2008)
Recursive descent without backtracking requires:
**Solution.** LL(1) grammar.

### Q5. (GATE CSE 2010)
FIRST(S) for S → AB | a, A → ε | b:
**Solution.** First of AB: FIRST(A) − {ε} ∪ (FIRST(B) if ε ∈ FIRST(A)) — assume B has terminal c → FIRST(S) = {b, c, a}.

### Q6. (GATE CSE 2015)
LR(1) grammar handles left recursion:
**Solution.** Yes.

### Q7. (GATE CSE 2013)
Shift-reduce conflict in LR(0):
**Solution.** Both shift and reduce applicable on same input.

### Q8. (GATE CSE 2007)
LALR(1) compared to LR(1):
**Solution.** Same states as LR(0)/SLR; less powerful than LR(1).

### Q9. (GATE CSE 2003)
Operator precedence parser handles:
**Solution.** Operator grammars.

### Q10. (GATE CSE 2009)
FOLLOW(A) for A → ε in S → AB:
**Solution.** FIRST(B) − {ε} (and FOLLOW(S) if ε ∈ FIRST(B)).

### Q11. (GATE CSE 2019)
LR parser uses:
**Solution.** Stack + parsing table (ACTION + GOTO).

### Q12. (GATE CSE 2020)
Eliminate left recursion: A → Aα | β:
**Solution.** A → β A'; A' → α A' | ε.

### Q13. (GATE CSE 2021)
LL(1) parse table conflict:
**Solution.** Two productions in same cell.

### Q14. (GATE CSE 2016)
Lexical analysis tool:
**Solution.** lex / flex.

### Q15. (GATE CSE 2011)
LR(0) item:
**Solution.** A production with a dot indicating parsing position.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define lexer.

**P2.** What's a token?

**P3.** Top-down vs bottom-up parsing?

**P4.** LL stands for?

**P5.** LR stands for?

**P6.** LL(1) requires what conditions?

**P7.** Eliminate left recursion: A → Aa | b.

**P8.** Left factor: A → ab | ac.

**P9.** LR(1) vs LALR(1) — which more powerful?

**P10.** Operator precedence parser limitation?

### Medium

**P11.** Compute FIRST and FOLLOW for S → AB, A → a | ε, B → b.

**P12.** Build LL(1) parse table for above grammar.

**P13.** Test LL(1) for S → S a | b.

**P14.** Eliminate left recursion in S → S a | S b | c.

**P15.** Left-factor S → if E then S | if E then S else S.

**P16.** Apply LR(0) to grammar S → A B, A → a, B → b.

**P17.** Detect shift-reduce conflict in S → S + S | id.

**P18.** Compare LL(1) and LR(1) on left-recursive grammar.

**P19.** LALR vs LR(1) state count.

**P20.** Recursive descent for arithmetic expressions.

### Hard

**P21.** Build SLR(1) table for E → E + T | T, T → T * F | F, F → (E) | id.

**P22.** Build LALR(1) parse table for above.

**P23.** Find LR(0) items + canonical collection.

**P24.** Identify reduce-reduce conflict.

**P25.** Convert ambiguous if-else grammar to unambiguous.

**P26.** Compute FIRST and FOLLOW with ε-productions.

**P27.** Handle right-recursion in LL grammar (often acceptable).

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | DFA over token regex | direct |
| P2 | <type, value> | direct |
| P3 | start to leaves vs leaves to start | direct |
| P4 | left-to-right, leftmost | direct |
| P5 | left-to-right, rightmost (reverse) | direct |
| P6 | as in 1.6 | direct |
| P7 | A → bA'; A' → aA' | ε | direct |
| P8 | A → aA'; A' → b | c | direct |
| P9 | LR(1) > LALR(1) | direct |
| P10 | only operator grammars | direct |
| P11 | FIRST(S) = {a, b}; FOLLOW(S) = {$}; FOLLOW(A) = {b}; FOLLOW(B) = {$} | trace |
| P12 | trace | direct |
| P13 | left recursion → not LL(1) | direct |
| P14 | S → c S'; S' → a S' | b S' | ε | direct |
| P15 | left-factor common prefix | direct |
| P16 | trace LR(0) | direct |
| P17 | shift-reduce | direct |
| P18 | LR succeeds; LL fails | direct |
| P19 | same states, LR(1) more | direct |
| P20 | function per non-terminal | direct |
| P21 | trace closure / goto | direct |
| P22 | trace LALR | direct |
| P23 | trace items | direct |
| P24 | two productions reduce on same input | direct |
| P25 | match else with nearest if | direct |
| P26 | iterative algorithm | direct |
| P27 | usually fine for LL | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | LL(1) handles left recursion | It doesn't. |
| 2 | LR(1) and LALR(1) same power | LALR is weaker but practical. |
| 3 | Forgetting ε case in FIRST/FOLLOW | Crucial for LL(1) test. |
| 4 | Left recursion elimination wrong order | A' → α A' | ε. |
| 5 | Lexer can be NFA only | Yes, but typically determinized. |
| 6 | Treat all CFGs as LL(1) | Many aren't. |
| 7 | Shift-reduce always means non-LR | Often resolved by precedence rules. |
| 8 | LL(1) ⊆ LR(0) | Wrong: LL(1) ⊆ LR(1) but not LR(0). |
| 9 | LALR has more states than SLR | They have same number of states. |
| 10 | Recursive descent always works | Only for LL(1) without backtracking. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Compute FIRST/FOLLOW" | Iterate until stable. |
| "LL(1) check" | Build parse table; conflict ⇒ not LL(1). |
| "Build LR table" | Closure + goto + ACTION/GOTO. |
| "Eliminate left recursion" | Standard procedure. |
| "Left factor" | Common prefix removal. |
| "Conflict resolution" | Precedence/associativity rules. |
| "Recursive descent" | Top-down LL(1). |
| "Operator precedence" | Limited grammar. |
| "Lexer" | DFA / regex-based. |
| "LR power comparison" | LR(0) ⊊ SLR ⊊ LALR ⊊ LR(1). |

---

## 9. Quick Revision

```
LEXER = DFA over regex
TOKEN <type, value>; LEXEME text; PATTERN regex

PARSER
 top-down: LL(k), recursive descent
 bottom-up: LR(0), SLR, LALR, LR(1)

LL(1)
 no left recursion
 left-factored
 FIRST disjoint
 ε in FIRST(α) ⇒ FIRST(β) ∩ FOLLOW(A) = ∅

FIRST(X)
 terminal: self
 ε rules apply
 cumulate Y_i

FOLLOW(A)
 FOLLOW(S) ⊇ $
 A → αBβ: FOLLOW(B) ⊇ FIRST(β) − {ε}
 A → αB: FOLLOW(B) ⊇ FOLLOW(A)

LR
 LR(0): no lookahead
 SLR: uses FOLLOW
 LALR: merged LR(1) states
 LR(1): full lookahead
 power: LR(0) ⊊ SLR ⊊ LALR ⊊ LR(1)

CONFLICTS
 LL: same cell
 LR: shift-reduce, reduce-reduce

LEFT REC: A → Aα | β  →  A → βA', A' → αA' | ε
LEFT FACTOR: A → αβ | αγ  →  A → αA', A' → β | γ

LR handles left rec; LL doesn't
LL(1) ⊊ LR(1); LR(1) ⊋ LALR(1)

LALR most practical
```
