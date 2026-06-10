# Topic Test 21 — DBMS (ER & Relational Model · SQL & Relational Algebra)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] M:N relationship in relational schema needs:
(A) FK only  (B) Single relation  (C) Separate relation with composite PK  (D) None

**Q2.** [MCQ] FK in 1:N relationship resides on:
(A) 1 side  (B) N side  (C) Either  (D) Neither

**Q3.** [MCQ] Weak entity has:
(A) Own PK  (B) Owner's PK + discriminator  (C) No PK ever  (D) Foreign key only

**Q4.** [MCQ] Total participation indicator:
(A) Single line  (B) Double line  (C) Dashed line  (D) Triple line

**Q5.** [MCQ] Multi-valued attribute mapping:
(A) Same relation  (B) Separate relation  (C) Drop  (D) Compute

**Q6.** [MCQ] Selection in relational algebra:
(A) σ  (B) π  (C) ⋈  (D) ÷

**Q7.** [MCQ] Projection symbol:
(A) σ  (B) π  (C) ⋈  (D) ρ

**Q8.** [MCQ] Natural join requires:
(A) Common attribute names  (B) Same arity  (C) Same domain  (D) None

**Q9.** [MCQ] NULL = NULL evaluates to:
(A) TRUE  (B) FALSE  (C) NULL  (D) Error

**Q10.** [MCQ] COUNT(*) vs COUNT(col):
(A) Same  (B) COUNT(col) skips NULL  (C) COUNT(*) skips NULL  (D) Both skip

**Q11.** [MCQ] HAVING vs WHERE:
(A) HAVING before GROUP BY  (B) HAVING after GROUP BY  (C) Same  (D) None

**Q12.** [NAT] # of tables for ER with 4 strong entities + 2 M:N relationships + 1 multi-valued attribute = `____`

**Q13.** [MCQ] DDL command:
(A) SELECT  (B) INSERT  (C) CREATE  (D) UPDATE

**Q14.** [MCQ] DCL command:
(A) GRANT  (B) DELETE  (C) UPDATE  (D) SELECT

**Q15.** [MCQ] Cartesian product symbol:
(A) ×  (B) ∪  (C) ∩  (D) −

---

## Section B — 2 marks each

**Q16.** [MCQ] UNION removes duplicates; UNION ALL:
(A) Removes too  (B) Keeps duplicates  (C) Throws error  (D) Skips NULLs

**Q17.** [MCQ] Outer join preserves:
(A) No unmatched rows  (B) Unmatched from one or both sides  (C) Only matched  (D) Random rows

**Q18.** [MCQ] Find departments with > 5 employees:
(A) `SELECT dept FROM Emp WHERE COUNT(*) > 5`
(B) `SELECT dept FROM Emp GROUP BY dept HAVING COUNT(*) > 5`
(C) `SELECT dept FROM Emp HAVING COUNT(*) > 5`
(D) None

**Q19.** [MCQ] Self-join purpose:
(A) Combine 2 tables  (B) Join table to itself  (C) Cross product  (D) Filter rows

**Q20.** [MCQ] Division operation example:
(A) Find employees in some dept  (B) Find students who took ALL courses in S  (C) Cross product  (D) Filter

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (C) | direct |
| 2 | (B) | direct |
| 3 | (B) | direct |
| 4 | (B) | direct |
| 5 | (B) | direct |
| 6 | (A) | direct |
| 7 | (B) | direct |
| 8 | (A) | direct |
| 9 | (C) | direct |
| 10 | (B) | direct |
| 11 | (B) | direct |
| 12 | 7 | 4 + 2 + 1 |
| 13 | (C) | direct |
| 14 | (A) | direct |
| 15 | (A) | direct |
| 16 | (B) | direct |
| 17 | (B) | direct |
| 18 | (B) | direct |
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
