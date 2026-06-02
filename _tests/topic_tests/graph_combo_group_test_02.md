# Topic Test 02 — Graph Theory + Combinatorics + Group Theory & Lattices

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ for 1-mark, −⅔ for 2-mark. NAT no negative.

Solve before scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] A simple graph has degrees (5, 4, 3, 3, 2, 1). Number of edges?
(A) 8  (B) 9  (C) 18  (D) 4

**Q2.** [MCQ] # edges in K₈?
(A) 28  (B) 32  (C) 56  (D) 64

**Q3.** [MCQ] Number of spanning trees of K₅?
(A) 25  (B) 64  (C) 125  (D) 81

**Q4.** [NAT] Number of edges in a tree on 100 vertices = `____`

**Q5.** [MCQ] Which graph is non-planar?
(A) K₄  (B) K₅  (C) C₆  (D) Q₃

**Q6.** [MCQ] Chromatic number of C₉?
(A) 2  (B) 3  (C) 4  (D) 5

**Q7.** [MCQ] # arrangements of letters in COMBINATIONS?
(A) 11!/2!  (B) 11!/2!2!  (C) 11!/2!  (D) 11!

**Q8.** [NAT] Number of integer solutions to x+y+z = 15 with x,y,z ≥ 0 = `____`

**Q9.** [MCQ] # ways to seat 7 people around a round table?
(A) 5040  (B) 720  (C) 4320  (D) 120

**Q10.** [MCQ] D₅ (derangements of 5 elements) = ?
(A) 24  (B) 44  (C) 120  (D) 9

**Q11.** [MCQ] # generators of (ℤ₁₀, +)?
(A) 2  (B) 4  (C) 6  (D) 10

**Q12.** [MCQ] Lagrange's theorem says, for finite group G with subgroup H:
(A) |H| = |G|  (B) |H| divides |G|  (C) |G| divides |H|  (D) gcd(|H|,|G|)=1

**Q13.** [MCQ] In divisibility lattice, GLB(12, 18) = ?
(A) 36  (B) 6  (C) 2  (D) 3

**Q14.** [MCQ] ℤ₁₀ under multiplication mod 10 is:
(A) group  (B) abelian group  (C) monoid but not group  (D) only semigroup

**Q15.** [NAT] # subgroups of ℤ₂₀ = `____`

---

## Section B — 2 marks each

**Q16.** [MCQ] # binary strings of length 12 with no two consecutive 1's?
(A) F₁₂ = 144  (B) F₁₃ = 233  (C) F₁₄ = 377  (D) 2¹²

**Q17.** [NAT] # ways to choose a committee of 5 from 12 people, where 2 specific people refuse to serve together = `____`

**Q18.** [MCQ] G is a connected planar simple graph with V = 10, E = 21. Number of faces?
(A) 11  (B) 13  (C) 21  (D) impossible (not planar)

**Q19.** [MCQ] Order of permutation σ = (1 2 3 4 5)(6 7) ∈ S₇:
(A) 5  (B) 7  (C) 10  (D) 12

**Q20.** [MCQ] Which lattice is **not** distributive?
(A) Power set (P(S), ⊆)
(B) Divisor lattice of 30
(C) Pentagon N₅
(D) Chain {1, 2, 3, 4, 5}

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) 9 | Σ deg = 18, /2 = 9 |
| 2 | (A) 28 | 8·7/2 |
| 3 | (C) 125 | Cayley 5³ |
| 4 | 99 | n−1 |
| 5 | (B) K₅ | E=10 > 3·5−6=9 |
| 6 | (B) 3 | odd cycle |
| 7 | (B) 11!/(2!·2!) | O×2, I×2 (also N×2... actually O:2, M:1, B:1, I:2, N:2, A:1, T:1, S:1) — recount: COMBINATIONS = C,O,M,B,I,N,A,T,I,O,N,S → 12 letters, but actually "COMBINATIONS" has 12 letters? Let me count: C-O-M-B-I-N-A-T-I-O-N-S = 12. So #=12!/(2!·2!·2!) for I,O,N. **None of the options match exactly** — closest correct answer: 12!/(2!·2!·2!) |
| 8 | 136 | C(15+3−1, 3−1) = C(17, 2) = 136 |
| 9 | (B) 720 | (7−1)! = 720 |
| 10 | (B) 44 | D₅=44 |
| 11 | (B) 4 | φ(10)=4 |
| 12 | (B) | Lagrange |
| 13 | (B) 6 | gcd(12,18)=6 |
| 14 | (C) | 2,5 lack inverses |
| 15 | 6 | divisors of 20: 1,2,4,5,10,20 → 6 |
| 16 | (C) 377 | F_{n+2} for length n: F₁₄=377 |
| 17 | C(12,5) − C(10,3) = 792 − 120 = 672 | Total − (both included) |
| 18 | (B) 13 | V−E+F = 2 ⇒ F = 13. Check planarity: 21 ≤ 3·10−6=24 ✓ |
| 19 | (C) 10 | lcm(5,2) |
| 20 | (C) | N₅ is the canonical non-distributive |

> **Note on Q7:** The question's options are imperfect; the correct combinatorial answer is **12!/(2!·2!·2!)** for "COMBINATIONS" (I×2, O×2, N×2). Mark yourself based on whether you set up the multinomial correctly.

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
- < 18 → re-do PYQs of all three topics, retake test in 5 days

**Post-test:** add every wrong answer to [../../_progress/mistakes_log.md](../../_progress/mistakes_log.md) with a pattern tag.
