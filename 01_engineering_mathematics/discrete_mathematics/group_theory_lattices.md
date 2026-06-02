# Group Theory & Lattices

> Subject: Engineering Mathematics → Discrete Mathematics
> GATE weight: **1–3 marks** every year. Algebra structure questions + lattice/Boolean algebra.

---

## 1. Concept Explanation

### 1.1 Algebraic Structures Hierarchy

Given a set S and a binary operation `*`:

| Structure | Properties |
|---|---|
| Magma / Groupoid | closed under * |
| Semigroup | closed + associative |
| Monoid | semigroup + identity element |
| Group | monoid + every element has inverse |
| Abelian group | group + commutative |
| Ring | (R, +) abelian group, (R, ·) semigroup, distributive |
| Commutative ring | ring + · commutative |
| Integral domain | comm. ring + no zero divisors |
| Field | comm. ring + every non-zero has multiplicative inverse |

**Order of group |G|** = number of elements.

### 1.2 Group Properties

A group `(G, *)` satisfies:
1. **Closure:** ∀a,b ∈ G, a*b ∈ G
2. **Associativity:** (a*b)*c = a*(b*c)
3. **Identity:** ∃e ∈ G, e*a = a*e = a
4. **Inverse:** ∀a ∈ G, ∃a⁻¹ with a*a⁻¹ = a⁻¹*a = e

If also **commutative** (a*b = b*a) → **abelian** group.

**Order of an element a:** smallest positive integer n with `aⁿ = e`. Denoted `o(a)`. If no such n exists, infinite order.

### 1.3 Subgroups

`H ⊆ G` is a **subgroup** iff H is closed, contains identity, and contains inverses (one-step test: `∀a, b ∈ H, a*b⁻¹ ∈ H`).

**Lagrange's Theorem:** for finite group G, |H| divides |G|.

Corollary: order of any element divides |G|.

### 1.4 Cyclic Groups

A group G is **cyclic** if ∃g ∈ G such that every element is gᵏ for some k ∈ ℤ. Notation: `G = ⟨g⟩`.

- Every cyclic group is abelian.
- Every subgroup of a cyclic group is cyclic.
- A cyclic group of order n is isomorphic to **ℤₙ** (integers mod n under addition).
- # generators of ℤₙ = `φ(n)` (Euler's totient).
- Number of subgroups of ℤₙ = number of divisors of n.

### 1.5 Common Groups

| Group | Description | |G| | Abelian? |
|---|---|---|---|
| ℤₙ (under +) | integers mod n | n | ✅ |
| ℤₙ* (under ·) | units mod n | φ(n) | ✅ |
| Sₙ | permutations of n | n! | ✅ iff n ≤ 2 |
| Aₙ | even permutations | n!/2 | ✅ iff n ≤ 3 |
| Dₙ | dihedral (symmetries of n-gon) | 2n | ✅ iff n ≤ 2 |
| GL(n, ℝ) | invertible n×n matrices | infinite | ❌ |
| SL(n, ℝ) | det = 1 matrices | infinite | ❌ |

### 1.6 Permutation Groups & Cycle Notation

A permutation σ ∈ Sₙ can be written as product of disjoint cycles. **Order of σ** = LCM of cycle lengths.

**Sign:** σ is even (sgn = +1) iff product of an even number of transpositions; odd (sgn = −1) otherwise.

Aₙ (even perms) is a subgroup of index 2.

### 1.7 Cosets, Normal Subgroups, Quotients

- **Left coset:** `aH = {a*h : h ∈ H}`. Cosets partition G.
- **# cosets** = `|G|/|H|` (Lagrange).
- **Normal subgroup N:** `gNg⁻¹ ⊆ N` for all g (left = right cosets).
- **Quotient group G/N:** cosets form a group.

### 1.8 Homomorphism, Isomorphism

- **Homomorphism** `f: G → H`: `f(a*b) = f(a)·f(b)`.
- **Kernel:** `ker(f) = {g ∈ G : f(g) = e_H}`. Always a normal subgroup.
- **Isomorphism:** bijective homomorphism. G ≅ H.
- **First Isomorphism Theorem:** `G/ker(f) ≅ image(f)`.

### 1.9 Rings & Fields (basics)

- Ring `(R, +, ·)`: addition is abelian group; multiplication is associative; distributive.
- A **field** has multiplicative inverses for all non-zero elements.
- **ℤ, ℚ, ℝ, ℂ** are rings; ℚ, ℝ, ℂ are fields; ℤ is not.
- Finite field of order pⁿ is GF(pⁿ) — exists iff p is prime.

### 1.10 Lattices (Order-theoretic)

A **lattice** is a poset (L, ≤) where every pair {a, b} has:
- **Join (LUB)**: `a ∨ b` (least upper bound).
- **Meet (GLB)**: `a ∧ b` (greatest lower bound).

**Equivalent algebraic definition:** lattice = set with two operations ∨, ∧ both commutative, associative, with absorption: `a ∨ (a ∧ b) = a` and `a ∧ (a ∨ b) = a`.

### 1.11 Special Lattices

| Type | Property |
|---|---|
| Bounded | has 0 (least) and 1 (greatest) |
| Distributive | a ∧ (b ∨ c) = (a ∧ b) ∨ (a ∧ c) |
| Complemented | every element has a complement (a ∨ a' = 1, a ∧ a' = 0) |
| Boolean | distributive + complemented + bounded |
| Modular | a ≤ c ⇒ a ∨ (b ∧ c) = (a ∨ b) ∧ c |

**Boolean algebra** ≅ Boolean lattice. Examples: power set under ⊆; truth values under {0,1} with AND, OR.

### 1.12 Hasse Diagram → LUB/GLB

In a Hasse diagram:
- a ∨ b = "first common ancestor" reachable upward
- a ∧ b = "first common descendant" reachable downward

Not every poset is a lattice — pair may have multiple maximal lower bounds (no GLB).

### 1.13 Distributive Lattice Test

A lattice is distributive iff it does **not** contain N₅ (pentagon) or M₃ (diamond) as a sublattice.

> **Summary:** Group axioms (closure, assoc, identity, inverse). Lagrange. Cyclic ↔ ℤₙ. Lattices = posets with ∨/∧. Boolean = distributive + complemented. Memorize the structure ladder and the lattice tests.

---

## 2. Important Points

- **Group axioms:** Closure, Associativity, Identity, Inverse (CAII).
- **Identity & inverse are unique** in any group.
- **Cancellation:** `a*b = a*c ⇒ b = c`.
- **(ab)⁻¹ = b⁻¹ a⁻¹** (reverse order).
- |G| prime ⇒ G is cyclic and only subgroups are {e} and G.
- Order of element divides order of group (corollary of Lagrange).
- # generators of ℤₙ = φ(n).
- Sₙ has order n!; Aₙ has order n!/2.
- Sₙ is **non-abelian** for n ≥ 3.
- A cyclic group of order n has exactly **one** subgroup of each divisor order.
- Every group of order ≤ 5 is abelian.
- Two cyclic groups of the same order are isomorphic.
- Lattice **always** has unique LUB/GLB for any pair (by definition).
- Boolean lattice on n elements ≅ subsets of n-set (P(n)) ⇒ size 2ⁿ.
- A finite distributive lattice is determined by its set of join-irreducibles.
- **Power set lattice (P(S), ⊆)** is Boolean.
- The divisibility poset on positive integers is a distributive lattice (LUB = lcm, GLB = gcd).
- **# elements in finite Boolean lattice = 2ᵏ for some k.**
- **Direct product** of two groups is a group; order multiplies.

---

## 3. Short Notes

```
STRUCTURE LADDER  (S, *)
 Magma     : closed
 Semigroup : + assoc
 Monoid    : + identity
 Group     : + inverses
 Abelian   : + commutative

GROUP COROLLARIES
 identity, inverse unique
 (ab)⁻¹ = b⁻¹a⁻¹
 cancellation: ab=ac ⇒ b=c
 Lagrange: |H| | |G|
 o(a) | |G|

CYCLIC GROUPS
 ⟨g⟩ generated by single element
 |⟨g⟩|= o(g)
 ℤₙ : cyclic of order n
 # generators of ℤₙ = φ(n)
 # subgroups of ℤₙ = #divisors(n)
 every cyclic is abelian

COMMON GROUPS
 ℤₙ: order n, abelian
 Sₙ: order n!, non-abelian for n≥3
 Aₙ: order n!/2 (even perms)
 Dₙ: dihedral, order 2n
 GL(n,ℝ): invertible matrices, non-abelian

PERMUTATION
 σ = disjoint cycles
 o(σ) = lcm(cycle lengths)
 sgn(σ): even / odd

NORMAL & QUOTIENT
 N ⊴ G ⇔ gNg⁻¹ = N
 G/N is a group
 1st Iso: G/ker f ≅ im f

RINGS, FIELDS
 Ring: (+) abelian group, (·) semigroup, distrib
 Field: ring + non-zero has multiplicative inverse
 GF(pⁿ): finite field iff p prime

LATTICE
 poset where ∀a,b ∃ a∨b, a∧b
 absorption: a∨(a∧b)=a, a∧(a∨b)=a
 distributive: a∧(b∨c)=(a∧b)∨(a∧c)
 complemented: ∀a ∃a': a∨a'=1, a∧a'=0
 Boolean = distrib + comp + bounded
 |Boolean lattice| = 2ᵏ

DISTRIB ⇔ no N₅, no M₃ sublattice
DIVISIBILITY POSET on ℕ⁺ is distributive lattice
 lub = lcm; glb = gcd
```

---

## 4. Formulas / Tricks

| # | Fact | Memorize Cold? |
|---|---|---|
| 1 | Lagrange: \|H\| divides \|G\| | ✅✅ |
| 2 | o(a) divides \|G\| | ✅✅ |
| 3 | (ab)⁻¹ = b⁻¹ a⁻¹ | ✅ |
| 4 | # generators of ℤₙ = φ(n) | ✅ |
| 5 | # subgroups of ℤₙ = τ(n) (divisor count) | ✅ |
| 6 | \|Sₙ\| = n!; \|Aₙ\| = n!/2 | ✅ |
| 7 | \|Dₙ\| = 2n | ✅ |
| 8 | Order of permutation = lcm of cycle lengths | ✅ |
| 9 | Group of prime order is cyclic | ✅ |
| 10 | Cancellation law in group | ✅ |
| 11 | Lattice absorption: a∨(a∧b)=a | ✅ |
| 12 | Boolean lattice has 2ᵏ elements | ✅ |
| 13 | Divisibility lattice: lub=lcm, glb=gcd | ✅ |
| 14 | Distributive ⇔ no N₅/M₃ sublattice | ✅ |
| 15 | Power set (P(S), ⊆) is Boolean | ✅ |

### Tricks

- **Quickly testing structure:** verify in order — closure first, then associativity, then identity, then inverses. Stop at the first failure.
- **Order of element in ℤₙ** = `n / gcd(n, k)` for element k.
- **In Sₙ, order of cycle** of length k is k. For product of disjoint cycles, take lcm.
- **A finite group of even order has an element of order 2** (Cauchy / counting argument).
- **GCD-LCM trick:** `lcm(a,b) · gcd(a,b) = a·b`.
- **Distributive lattice check shortcut:** count complements — in a Boolean lattice each element has unique complement; if any element has more than one complement, **not distributive**.
- **Subgroups of ℤₙ** are exactly `dℤₙ` for each d|n.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2014)
Consider the set S = {1, ω, ω²}, where ω is a cube root of unity. Under multiplication, S is:
(A) semigroup (B) monoid (C) group (D) abelian group

**Solution.** Closed (cube roots multiply to cube roots), associative, identity 1, inverses (ω·ω² = 1), commutative. ⇒ abelian group.
**Answer: (D).**

### Q2. (GATE CSE 2017)
Consider the set ℤ₆ = {0,1,2,3,4,5} under multiplication modulo 6. The set is:
(A) group (B) semigroup but not monoid (C) monoid but not group (D) commutative monoid but not group

**Solution.** Closed, associative, identity 1. But 2, 3, 4 lack inverses (zero divisors). Commutative.
**Answer: (D).**

### Q3. (GATE CSE 2015)
The number of elements in the set {1, 2, 3, …, 30} that are coprime to 30 is:
**Solution.** φ(30) = 30·(1−1/2)(1−1/3)(1−1/5) = 30·1/2·2/3·4/5 = 8.
**Answer: 8.**

### Q4. (GATE CSE 2010)
Let G be a group of order 6. Which of the following is true?
(A) G is necessarily abelian
(B) G is necessarily cyclic
(C) G has subgroup of order 2 and 3
(D) G has only trivial subgroups

**Solution.** Lagrange: subgroups have order 1, 2, 3, or 6. By Cauchy, G has elements of order 2 and 3 ⇒ subgroups of those orders.
**Answer: (C).**

### Q5. (GATE CSE 2008)
Let G = (ℤ, +). The subgroup generated by {3, 5} is:
**Solution.** ⟨3, 5⟩ = ℤ (since gcd(3,5)=1). *(Pattern: subgroup-generated by gcd.)*

### Q6. (GATE CSE 2005)
The number of subgroups of ℤ₂₄:
**Solution.** Number of divisors of 24 = (3+1)(1+1) = 8.
**Answer: 8.**

### Q7. (GATE CSE 2007)
Let H be a Hasse diagram of a poset on {a,b,c,d,e,f} with cover relations forming a "diamond" with extra elements. Determine LUB and GLB of subset.
*(Pattern: Hasse → LUB/GLB.)*

### Q8. (GATE CSE 2014)
A lattice (L, ≤) is given. Each element has a unique complement and ∨/∧ distribute. Which lattice is this?
**Answer:** Boolean lattice.

### Q9. (GATE CSE 2012)
The number of generators of the cyclic group ℤ₁₂:
**Solution.** φ(12) = 12·(1−1/2)(1−1/3) = 4. Generators are 1, 5, 7, 11.
**Answer: 4.**

### Q10. (GATE CSE 2018)
Permutation σ = (1 2 3 4)(5 6) ∈ S₆. Order of σ is:
**Solution.** lcm(4, 2) = 4.
**Answer: 4.**

### Q11. (GATE CSE 2009)
Let (L, ≤) be a poset where every pair has GLB and LUB. Then it is a:
**Answer:** Lattice.

### Q12. (GATE CSE 2003)
On the set ℤ⁺ with relation `a ≤ b ⇔ a divides b`, find LUB(4, 6) and GLB(4, 6):
**Solution.** lub = lcm(4,6) = 12. glb = gcd(4,6) = 2.

### Q13. (GATE CSE 2016)
A group G has 8 elements. The maximum possible order of any element is:
**Solution.** Lagrange: divides 8. Max = 8 (cyclic case).
**Answer: 8.**

### Q14. (GATE CSE 2011)
Let (L, ∨, ∧) be a complemented distributive lattice. The lattice is:
**Answer:** Boolean.

### Q15. (GATE CSE 2019)
The set ℤ₅* = {1,2,3,4} under multiplication mod 5 is:
**Solution.** Closed, associative, identity 1, inverses (2·3≡1, 4·4≡1). Commutative. ⇒ abelian group.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Is (ℕ, +) a group? Why?

**P2.** Is (ℤ, ·) a group? Why?

**P3.** Order of ℤ₁₀.

**P4.** # generators of ℤ₇.

**P5.** Order of element 3 in (ℤ₁₂, +).

**P6.** Order of (1 2 3) in S₃.

**P7.** Identity element of (ℤ, +).

**P8.** Find inverse of 3 in (ℤ₇*, ·).

**P9.** Is S₃ abelian?

**P10.** Find LUB and GLB of {2, 5} in divisibility lattice.

### Medium

**P11.** Is the set of 2×2 invertible matrices a group under multiplication?

**P12.** Find all subgroups of ℤ₁₂.

**P13.** Show that S₃ has 6 elements and list them.

**P14.** Compute lcm and gcd in divisibility lattice for 36 and 90.

**P15.** Decide if {1, −1, i, −i} under multiplication is a group.

**P16.** Find the number of subgroups of (ℤ, +).

**P17.** Compute order of (1 2 3)(4 5 6 7) in S₇.

**P18.** Determine if the lattice {0, a, b, c, 1} with a, b, c all between 0 and 1 (each pair joins to 1, meets to 0) is distributive.

**P19.** Show: every group of order 4 is abelian.

**P20.** Show: in any group, a² = e ∀a ⇒ G abelian.

### Hard

**P21.** Find the number of distinct group structures (up to isomorphism) on 4 elements.

**P22.** Show that the divisibility lattice on positive divisors of n is distributive.

**P23.** Prove that the kernel of a homomorphism is a normal subgroup.

**P24.** Number of elements of order 6 in ℤ₁₂.

**P25.** Show: the lattice (P(S), ⊆) is distributive.

**P26.** A lattice on 6 elements is shown by a Hasse diagram. Determine if it is Boolean.

**P27.** Prove that a finite group of order p (prime) is cyclic.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | No | 0 has no inverse in ℕ for + |
| P2 | No | 2 has no multiplicative inverse |
| P3 | 10 | order = n |
| P4 | 6 | φ(7) = 6 |
| P5 | 4 | 12/gcd(12,3)=4 |
| P6 | 3 | 3-cycle |
| P7 | 0 | for + |
| P8 | 5 | 3·5=15≡1 (mod 7) |
| P9 | No | (1 2)(2 3) ≠ (2 3)(1 2) |
| P10 | lub=10, glb=1 | gcd/lcm |
| P11 | Yes — GL(2,ℝ) | non-abelian group |
| P12 | {0}, ⟨6⟩, ⟨4⟩, ⟨3⟩, ⟨2⟩, ℤ₁₂ | divisors of 12 |
| P13 | e, (12), (13), (23), (123), (132) | direct |
| P14 | gcd=18, lcm=180 | factorize |
| P15 | Yes — cyclic of order 4 (gen by i) | abelian |
| P16 | Infinite — every nℤ for n ≥ 0 | mℤ subgroups |
| P17 | lcm(3,4)=12 | cycle orders |
| P18 | Not distributive — diamond M₃ | M₃ test |
| P19 | Order 4: cyclic ℤ₄ or Klein V₄, both abelian | classify |
| P20 | a² = e ⇒ a = a⁻¹; (ab)² = e ⇒ ab = (ab)⁻¹ = b⁻¹a⁻¹ = ba | involution |
| P21 | 2 (ℤ₄ and Klein V₄) | classification |
| P22 | divisor lattice ≅ ⊓ Cₚᵢ over prime factorization, each chain is distributive, product is distributive | product of chains |
| P23 | f(n)=e; f(gng⁻¹) = f(g)f(n)f(g⁻¹) = e | direct |
| P24 | 2 elements of order 6: 2 and 10 | gcd=2 cases |
| P25 | (A∩(B∪C))=(A∩B)∪(A∩C) | set distributivity |
| P26 | Check if size 2ᵏ and complement uniqueness | pow-of-2 sufficient with structure |
| P27 | Take any non-identity a; ⟨a⟩ subgroup; |⟨a⟩| divides p; not 1 ⇒ p ⇒ G | Lagrange |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Calling a monoid a group | Check inverses for **every** element. |
| 2 | Forgetting non-zero in ℤₙ for multiplicative group | Use ℤₙ* (units only). |
| 3 | Using Lagrange in reverse | |H| divides |G|, but not every divisor of |G| corresponds to a subgroup (for non-abelian); for cyclic, **every divisor does**. |
| 4 | Thinking every group of order n is cyclic | Only when n is prime, or n = pq with specific conditions. |
| 5 | Sₙ assumed abelian | Non-abelian for n ≥ 3. |
| 6 | Confusing meet/join with min/max in arbitrary posets | They're defined via LUB/GLB, not numeric min/max. |
| 7 | Thinking complement is unique in any lattice | Only in distributive lattices. |
| 8 | Forgetting absorption when checking lattice | a∨(a∧b)=a is required. |
| 9 | Treating divisibility as total order | It's a partial order on ℕ⁺. |
| 10 | Overlooking identity in monoid | Semigroup ≠ monoid. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Is (S,*) a group/monoid/...?" | Test ladder: closure → assoc → identity → inverses → commutativity. |
| "Order of element a" | Find smallest n with aⁿ = e; for ℤₙ use n/gcd(n,k). |
| "# generators of cyclic group" | φ(n). |
| "# subgroups of cyclic group" | τ(n) — divisor count. |
| "Order of permutation" | lcm of cycle lengths. |
| "Subgroup of group of order p (prime)" | Only {e} and G. |
| "Set with ∨, ∧ — type of lattice?" | Test distributive (M₃/N₅), complemented, bounded → Boolean if all. |
| "Divisibility poset" | Distributive lattice; lub=lcm, glb=gcd. |
| "Power set" | Boolean lattice; size 2ⁿ. |
| "# elements of given order" | use cyclic structure / Cauchy. |
| "Finite group of even order" | Has an element of order 2. |

---

## 9. Quick Revision

```
GROUP = closed + assoc + identity + inverse
ABELIAN: + commutative
Lagrange: |H| | |G|
o(a) | |G|
(ab)⁻¹ = b⁻¹ a⁻¹
prime |G| ⇒ cyclic ⇒ abelian

|Sₙ|=n!  |Aₙ|=n!/2  |Dₙ|=2n
Sₙ non-abelian for n≥3
o(perm) = lcm(cycle lengths)

ℤₙ : cyclic of order n
# generators ℤₙ = φ(n)
# subgroups ℤₙ = τ(n) (divisors)
o(k in ℤₙ) = n/gcd(n,k)

φ(n) = n·∏(1−1/p)
gcd · lcm = a·b

LATTICE: poset, ∀ pair has ∨, ∧
absorption: a∨(a∧b)=a, a∧(a∨b)=a
distributive: a∧(b∨c)=(a∧b)∨(a∧c)
complemented: ∀a ∃ a' (a∨a'=1, a∧a'=0)
Boolean: distrib + comp + bounded
|Boolean| = 2ᵏ

distrib ⇔ no N₅, no M₃ sublattice
divisibility lattice: lub=lcm, glb=gcd, distributive
power set (P(S), ⊆): Boolean

Ring = (+) abel grp, (·) semigroup, distrib
Field = ring + non-zero invertible
GF(pⁿ): finite field
```
