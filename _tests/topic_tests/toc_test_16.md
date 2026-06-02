# Topic Test 16 — TOC (CFG/PDA/CFL · Turing Machines & Decidability)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] CFG and which automaton are equivalent?
(A) DFA  (B) NFA  (C) NPDA  (D) DPDA

**Q2.** [MCQ] DPDA accepts:
(A) Regular  (B) DCFL  (C) CFL  (D) CSL

**Q3.** [MCQ] {aⁿbⁿcⁿ : n ≥ 0} is:
(A) Regular  (B) CFL  (C) Not CFL  (D) Decidable but not recursive

**Q4.** [MCQ] CFL closed under intersection?
(A) Yes  (B) No  (C) Only with regular  (D) Only with CSL

**Q5.** [MCQ] CYK algorithm time:
(A) O(n)  (B) O(n²)  (C) O(n³)  (D) O(2ⁿ)

**Q6.** [MCQ] Equivalence of two CFGs:
(A) Decidable  (B) Undecidable  (C) Semi-decidable  (D) Polynomial-time

**Q7.** [MCQ] {ww : w ∈ {a,b}*} is:
(A) Regular  (B) CFL  (C) Not CFL  (D) Recursive only

**Q8.** [MCQ] CNF form of CFG:
(A) A → BC or A → a  (B) A → aα  (C) A → aBb  (D) A → ε only

**Q9.** [MCQ] PDA stack alphabet:
(A) Σ  (B) Γ  (C) Q  (D) F

**Q10.** [MCQ] Turing machine halting problem is:
(A) In P  (B) NP-complete  (C) Decidable  (D) Undecidable

**Q11.** [MCQ] Decidable ≡ ?
(A) RE only  (B) RE ∩ co-RE  (C) co-RE only  (D) NP

**Q12.** [MCQ] Rice's theorem says:
(A) All TM properties decidable  (B) Non-trivial language property of L(M) undecidable  (C) Universality decidable  (D) Halting decidable

**Q13.** [MCQ] LBA accepts:
(A) Regular  (B) CFL  (C) CSL  (D) RE

**Q14.** [MCQ] RE closed under complement?
(A) Yes  (B) No  (C) Only finite  (D) Only DCFL

**Q15.** [MCQ] NTM vs DTM in power:
(A) Same  (B) NTM stronger  (C) DTM stronger  (D) Incomparable

---

## Section B — 2 marks each

**Q16.** [MCQ] CFG for L = {aⁿbⁿ : n ≥ 0}:
(A) S → aSb | ε  (B) S → aaSbb | ε  (C) S → ab | ε  (D) S → aSb | aS | bS

**Q17.** [MCQ] Pumping lemma for CFL: w split into:
(A) 3 parts  (B) 4 parts  (C) 5 parts (uvxyz)  (D) 6 parts

**Q18.** [NAT] If L is RE and complement L̄ is RE, then L is `____`-decidable (write yes or no based on whether decidable is yes=1 or no=0). Answer: 1 = decidable.

**Q19.** [MCQ] Which is undecidable?
(A) DFA emptiness  (B) DFA equivalence  (C) Regular language emptiness  (D) "Is L(M) finite?"

**Q20.** [MCQ] Chomsky hierarchy: which is strict inclusion?
(A) Regular ⊊ CFL ⊊ CSL ⊊ Rec ⊊ RE  (B) RE ⊊ Rec ⊊ CSL  (C) CFL ⊊ Regular  (D) None

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (C) | NPDA |
| 2 | (B) | DCFL |
| 3 | (C) | not CFL |
| 4 | (B) | CFL not closed under ∩ |
| 5 | (C) | direct |
| 6 | (B) | undecidable |
| 7 | (C) | not CFL |
| 8 | (A) | CNF |
| 9 | (B) | direct |
| 10 | (D) | direct |
| 11 | (B) | direct |
| 12 | (B) | Rice |
| 13 | (C) | direct |
| 14 | (B) | direct |
| 15 | (A) | same power |
| 16 | (A) | classic |
| 17 | (C) | uvxyz |
| 18 | 1 | decidable = RE ∩ co-RE |
| 19 | (D) | Rice |
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
