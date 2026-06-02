# Topic Test 15 — TOC (Regular Languages, DFA/NFA · Pumping Lemma & Closure)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] DFA, NFA, ε-NFA, regex equivalent in power?
(A) Yes  (B) No  (C) Only DFA & NFA  (D) Only DFA & regex

**Q2.** [MCQ] NFA with n states converted to DFA — max DFA states:
(A) n  (B) 2n  (C) n²  (D) 2ⁿ

**Q3.** [NAT] # states in min DFA accepting strings divisible by 4 in binary = `____`

**Q4.** [MCQ] Is {aⁿbⁿ : n ≥ 0} regular?
(A) Yes  (B) No  (C) Only when n bounded  (D) Cannot decide

**Q5.** [MCQ] Min DFA recognizing strings ending in "01":
(A) 2  (B) 3  (C) 4  (D) 5

**Q6.** [MCQ] Pumping lemma proves:
(A) Regularity  (B) Non-regularity  (C) Decidability  (D) Equivalence

**Q7.** [MCQ] In pumping lemma, who chooses w?
(A) Adversary  (B) You  (C) Random  (D) DFA

**Q8.** [MCQ] In pumping lemma, who chooses split xyz?
(A) Adversary  (B) You  (C) Random  (D) DFA

**Q9.** [MCQ] Regular languages closed under intersection?
(A) Yes  (B) No  (C) Only DFA-recognizable  (D) Only finite

**Q10.** [MCQ] Regular closed under complement?
(A) Yes  (B) No  (C) Only finite  (D) Only DFA

**Q11.** [MCQ] Right-linear grammar generates:
(A) Regular  (B) CFL  (C) CSL  (D) RE

**Q12.** [MCQ] Membership in regular language:
(A) O(|w|)  (B) O(2^|w|)  (C) O(n)  (D) Undecidable

**Q13.** [MCQ] Emptiness of regular language:
(A) Decidable  (B) Undecidable  (C) Semi-decidable  (D) Polynomial only

**Q14.** [MCQ] Regex (a + b)\* represents:
(A) ∅  (B) {ε}  (C) {a, b}\*  (D) Σ\*

**Q15.** [NAT] # states in NFA equivalent to regex `(a+b)*ab` (minimal) = `____`

---

## Section B — 2 marks each

**Q16.** [MCQ] Min DFA for "binary strings divisible by 5":
(A) 3 states  (B) 5 states  (C) 10 states  (D) 6 states

**Q17.** [NAT] # min DFA states for "strings containing substring 110" = `____`

**Q18.** [MCQ] CFL closed under intersection?
(A) Yes  (B) No  (C) Only with regular  (D) Only finite

**Q19.** [MCQ] {ww : w ∈ {a,b}\*} regular?
(A) Yes  (B) No  (C) Only when |w| bounded  (D) Cannot decide

**Q20.** [MCQ] Equivalence of two DFAs:
(A) Decidable  (B) Undecidable  (C) Semi-decidable only  (D) NP-complete

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (A) | direct |
| 2 | (D) | direct |
| 3 | 4 | states for mod 4 |
| 4 | (B) | direct |
| 5 | (B) 3 | states tracking last 2 chars |
| 6 | (B) | direct |
| 7 | (B) | direct |
| 8 | (A) | direct |
| 9 | (A) | direct |
| 10 | (A) | direct |
| 11 | (A) | direct |
| 12 | (A) | direct |
| 13 | (A) | direct |
| 14 | (D) Σ* | direct |
| 15 | 3 | start, after a, after ab |
| 16 | (B) 5 | mod 5 |
| 17 | 4 | states (no, 1, 11, 110) |
| 18 | (B) | direct |
| 19 | (B) | direct |
| 20 | (A) | direct |

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
