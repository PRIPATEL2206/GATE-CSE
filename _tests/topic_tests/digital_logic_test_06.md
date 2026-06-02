# Topic Test 06 — Digital Logic (Number Systems · Boolean Algebra & K-Maps)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] (1010 1101)₂ in hexadecimal:
(A) AC  (B) AD  (C) DA  (D) BD

**Q2.** [NAT] Decimal value of (101101)₂ = `____`

**Q3.** [MCQ] 8-bit 2's complement of −5:
(A) 11111011  (B) 10000101  (C) 11111010  (D) 00000101

**Q4.** [MCQ] Range of 8-bit 2's complement signed numbers:
(A) −127 to 128  (B) −128 to 127  (C) 0 to 255  (D) −255 to 255

**Q5.** [NAT] (3F)₁₆ in decimal = `____`

**Q6.** [MCQ] IEEE 754 single bias is:
(A) 64  (B) 127  (C) 128  (D) 1023

**Q7.** [MCQ] Number of distinct Boolean functions of 3 variables:
(A) 8  (B) 64  (C) 256  (D) 512

**Q8.** [MCQ] (AB)' = ?
(A) A'B'  (B) A' + B'  (C) AB'  (D) A'B

**Q9.** [MCQ] Simplify A + A'B:
(A) A  (B) A + B  (C) AB  (D) B

**Q10.** [MCQ] Universal gate set: pick from below:
(A) AND alone  (B) OR alone  (C) NAND alone  (D) XOR alone

**Q11.** [NAT] # rows in truth table of 5-variable function = `____`

**Q12.** [MCQ] A ⊕ A = ?
(A) 0  (B) 1  (C) A  (D) A'

**Q13.** [MCQ] Minimum K-map group size for 4-variable function is:
(A) 1  (B) 2  (C) 4  (D) 8

**Q14.** [MCQ] F = Σm(0, 2, 4, 6) on 3 variables minimizes to:
(A) C  (B) C'  (C) AB  (D) A + B

**Q15.** [MCQ] In an n-variable K-map, # of cells = ?
(A) n  (B) 2n  (C) n²  (D) 2ⁿ

---

## Section B — 2 marks each

**Q16.** [MCQ] Add the 5-bit 2's complement: 01100 + 01010. Is overflow detected?
(A) Yes, result is wrong  (B) No, result is 22  (C) No, result is 26  (D) Yes, result is −10

**Q17.** [MCQ] IEEE 754: 0 10000010 11000000000000000000000 represents:
(A) 7.0  (B) 12.0  (C) 14.0  (D) 28.0

**Q18.** [NAT] # essential prime implicants of F = Σm(0, 2, 5, 7, 8, 10, 13, 15) (4-var) = `____`

**Q19.** [MCQ] Implement F = AB + CD using minimum 2-input NAND gates:
(A) 3  (B) 4  (C) 5  (D) 6

**Q20.** [MCQ] Simplify (A + B)(A + C):
(A) A + BC  (B) A · BC  (C) AB + AC  (D) A + B + C

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) AD | 1010 1101 → A D |
| 2 | 45 | 32+8+4+1 |
| 3 | (A) 11111011 | flip 00000101 + 1 |
| 4 | (B) | 2's comp |
| 5 | 63 | 3·16+15 |
| 6 | (B) 127 | single |
| 7 | (C) 256 | 2^8 |
| 8 | (B) | DM |
| 9 | (B) A + B | identity |
| 10 | (C) NAND | universal |
| 11 | 32 | 2⁵ |
| 12 | (A) 0 | XOR |
| 13 | (A) 1 | minterms count as size 1 |
| 14 | (B) C' | minterms have C=0 |
| 15 | (D) 2ⁿ | rows |
| 16 | (A) Yes | 12+10=22 needs 5 bits but 5-bit signed max=15; 22 → 10110 = −10 in 2's comp |
| 17 | (C) 14.0 | 1.75 × 8 |
| 18 | 2 | B'D' and BD |
| 19 | (C) 5 | 2 NAND for AB + 2 for CD + 1 final NAND |
| 20 | (A) A + BC | distributive (Boolean OR over AND) |

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
