# Topic Test 10 — PDS (C Programming · Stacks/Queues/Linked Lists)

> **Format:** GATE-style.
> **Time limit:** 30 minutes.
> **Total marks:** 25 (Q1–Q15 × 1 mark, Q16–Q20 × 2 marks).
> **Marking:** MCQ wrong = −⅓ (1-mark), −⅔ (2-mark). NAT no negative.

Solve fully **before** scrolling to the answer key.

---

## Section A — 1 mark each

**Q1.** [MCQ] What does `int *p[10]` declare?
(A) Pointer to array of 10 ints  (B) Array of 10 pointers to int  (C) Function ptr  (D) Multidim array

**Q2.** [MCQ] Output:
```c
int x = 5;
printf("%d", x++);
```
(A) 5  (B) 6  (C) Garbage  (D) Error

**Q3.** [NAT] sizeof("hello") = `____`

**Q4.** [MCQ] Static local variable initialized to:
(A) Garbage  (B) 0  (C) NULL  (D) Random

**Q5.** [MCQ] C is:
(A) Pass-by-reference  (B) Pass-by-value  (C) Both  (D) Neither

**Q6.** [MCQ] Output of `printf("%d", 7/2)`:
(A) 3.5  (B) 3  (C) 4  (D) 2

**Q7.** [MCQ] Stack ADT discipline:
(A) FIFO  (B) LIFO  (C) Random  (D) Priority

**Q8.** [MCQ] Queue ADT discipline:
(A) FIFO  (B) LIFO  (C) Random  (D) Priority

**Q9.** [MCQ] Postfix `5 6 + 2 *` evaluates to:
(A) 11  (B) 16  (C) 22  (D) 17

**Q10.** [NAT] Convert infix `A + B * C` to postfix → answer = `____` (alphabetical only)

**Q11.** [MCQ] Insert at head of singly linked list:
(A) O(1)  (B) O(n)  (C) O(log n)  (D) O(n²)

**Q12.** [MCQ] Detect cycle in linked list:
(A) Linear scan  (B) Floyd's slow/fast pointers  (C) Hashing  (D) Both B and C

**Q13.** [MCQ] Doubly linked list per-node pointers:
(A) 1  (B) 2  (C) 3  (D) 4

**Q14.** [MCQ] Circular queue, capacity N. Empty condition:
(A) front == rear  (B) (rear+1) % N == front  (C) front == 0  (D) rear == N

**Q15.** [MCQ] Recursion depth of `f(n) = f(n-1)` until 0?
(A) 1  (B) n  (C) log n  (D) 2ⁿ

---

## Section B — 2 marks each

**Q16.** [MCQ] Output:
```c
int a[] = {1,2,3,4,5};
int *p = a + 2;
printf("%d %d", *p, p[1]);
```
(A) 3 4  (B) 2 3  (C) 1 2  (D) 4 5

**Q17.** [MCQ] Convert `(A + B) * (C - D)` to postfix:
(A) AB+CD-*  (B) +AB-CD*  (C) AB+*CD-  (D) ABCD+-*

**Q18.** [NAT] Stack: push 1, push 2, push 3, pop, push 4, pop, pop. Top of stack now = `____`

**Q19.** [MCQ] Two-stack queue: # of pops/pushes per dequeue (amortized)?
(A) O(1)  (B) O(2)  (C) O(n)  (D) O(log n)

**Q20.** [MCQ] Reverse a singly linked list with n nodes; time and space?
(A) O(n) time, O(1) space  (B) O(n²) time, O(1)  (C) O(n) time, O(n) space  (D) O(log n) time

---

# 🔒 Answer Key & Solutions

> Stop the timer first.

| Q | Ans | Solution |
|---|---|---|
| 1 | (B) | array of pointers |
| 2 | (A) 5 | postfix |
| 3 | 6 | 5 chars + '\0' |
| 4 | (B) 0 | static default |
| 5 | (B) | direct |
| 6 | (B) 3 | int division |
| 7 | (B) LIFO | direct |
| 8 | (A) FIFO | direct |
| 9 | (C) 22 | (5+6)·2 |
| 10 | ABC*+ | precedence |
| 11 | (A) O(1) | head insert |
| 12 | (D) Both | Floyd or hash |
| 13 | (B) 2 | prev + next |
| 14 | (A) | empty |
| 15 | (B) n | linear |
| 16 | (A) 3 4 | a[2]=3, a[3]=4 |
| 17 | (A) AB+CD-* | direct |
| 18 | 1 | trace |
| 19 | (A) O(1) | amortized |
| 20 | (A) | iterative |

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
