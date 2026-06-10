# Topic Test 17 — Compilers (Lexical & Parsing · SDT & IR)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] Lexer is implemented using:
(A) NFA  (B) DFA  (C) PDA  (D) TM

**Q2.** [MCQ] LL(1) requires:
(A) Left recursion allowed  (B) Common prefixes  (C) No left recursion + left-factored  (D) Ambiguity allowed

**Q3.** [MCQ] LR(1) handles left recursion?
(A) No  (B) Yes  (C) Only with augmentation  (D) Same as LL(1)

**Q4.** [MCQ] LR power ranking (subset):
(A) LR(0) ⊊ SLR(1) ⊊ LALR(1) ⊊ LR(1)  (B) LR(1) ⊊ LALR(1) ⊊ SLR(1) ⊊ LR(0)  (C) Equal  (D) None

**Q5.** [MCQ] Recursive descent without backtracking requires:
(A) LL(1)  (B) LR(0)  (C) LALR  (D) Operator precedence

**Q6.** [MCQ] FIRST(ε) = ?
(A) ∅  (B) {ε}  (C) {$}  (D) Σ

**Q7.** [MCQ] FOLLOW(S) for start symbol S:
(A) ∅  (B) {ε}  (C) ⊇ {$}  (D) Σ

**Q8.** [MCQ] Conflict in LL(1) parse table = ?
(A) Two productions in same cell  (B) Empty cell  (C) Wrong FIRST  (D) Wrong FOLLOW

**Q9.** [MCQ] LALR(1) state count vs SLR:
(A) Same as LR(0)  (B) Always more than LR(1)  (C) Half  (D) Twice

**Q10.** [MCQ] S-attributed grammar uses:
(A) Synthesized only  (B) Inherited only  (C) Both equally  (D) Neither

**Q11.** [MCQ] L-attributed evaluable in:
(A) Bottom-up only  (B) Top-down only  (C) Single L-to-R pass  (D) Multiple passes

**Q12.** [MCQ] 3-address code form:
(A) x = y op z  (B) x = y op z op w  (C) Single var  (D) Indirect only

**Q13.** [MCQ] Quadruples vs triples:
(A) Quadruples easier to optimize  (B) Triples easier  (C) Equal  (D) Triples impossible

**Q14.** [MCQ] Backpatching is for:
(A) Lexer  (B) Parser  (C) Filling jump targets later  (D) Symbol table

**Q15.** [MCQ] Operator precedence parser handles:
(A) All CFGs  (B) Operator grammars only  (C) Regular only  (D) RE only

---

## Section B — 2 marks each

**Q16.** [MCQ] Eliminate left recursion: A → Aa | b. Result?
(A) A → bA'; A' → aA' | ε  (B) A → aA' | ε  (C) A → b | ε  (D) A → Ab | a

**Q17.** [MCQ] FIRST(S) for S → AB, A → a | ε, B → b:
(A) {a}  (B) {b}  (C) {a, b}  (D) {ε}

**Q18.** [MCQ] 3AC for `a = b * c + d`:
(A) `t1 = b*c; a = t1+d`  (B) `a = b*c+d`  (C) `t1 = b+c; t2 = t1*d; a = t2`  (D) None

**Q19.** [MCQ] Detect grammar S → S a | b — LL(1)?
(A) Yes  (B) No (left recursion)  (C) Only with backtracking  (D) Need more info

**Q20.** [MCQ] Inherited attribute example:
(A) Value of arithmetic expression  (B) Length of string  (C) Type info from declaration  (D) Token count

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | direct |
| 2 | (C) | direct |
| 3 | (B) | direct |
| 4 | (A) | direct |
| 5 | (A) | direct |
| 6 | (B) {ε} | direct |
| 7 | (C) ⊇ {$} | direct |
| 8 | (A) | direct |
| 9 | (A) Same | direct |
| 10 | (A) | direct |
| 11 | (C) | direct |
| 12 | (A) | direct |
| 13 | (A) | direct |
| 14 | (C) | direct |
| 15 | (B) | direct |
| 16 | (A) | direct |
| 17 | (C) {a, b} | A produces a or ε so FIRST(B)=b included |
| 18 | (A) | direct |
| 19 | (B) | left recursion |
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
- < 18 → re-do PYQs of both topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
