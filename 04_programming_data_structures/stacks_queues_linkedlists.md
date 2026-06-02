# Stacks, Queues & Linked Lists

> Subject: Programming & Data Structures
> GATE weight: **2–4 marks** every year. Stack/queue operations, linked list manipulation, expression evaluation, applications.

---

## 1. Concept Explanation

### 1.1 Linear Data Structures

Linear DS organize data in a sequence:
- **Array:** contiguous memory, random access (O(1)), fixed size.
- **Linked list:** non-contiguous, sequential access (O(n)), dynamic size.
- **Stack & Queue:** restricted-access linear DS.

### 1.2 Stack (LIFO)

**Last In First Out** discipline. Operations:

| Operation | Description | Time |
|---|---|---|
| `push(x)` | Insert at top | O(1) |
| `pop()` | Remove from top | O(1) |
| `top()` / `peek()` | View top | O(1) |
| `isEmpty()` / `isFull()` | Check status | O(1) |

**Implementations:**
- Array: top index, fixed capacity, possible overflow.
- Linked list: head node, dynamic, no overflow (memory permitting).

### 1.3 Stack Applications

- **Function call stack** — recursion, return addresses.
- **Expression evaluation** — infix → postfix; postfix evaluation.
- **Balanced parenthesis check.**
- **Backtracking** — DFS, maze, undo.
- **Reverse a sequence.**

### 1.4 Postfix Evaluation Algorithm

```
For each token:
  If operand: push.
  If operator: pop two, apply, push result.
At end: top of stack is the result.
```

### 1.5 Infix → Postfix (Shunting-Yard)

```
For each token in infix:
  If operand: output.
  If '(': push.
  If ')': pop until '(' (discard '(').
  If operator:
    while stack top has higher/equal precedence: pop to output.
    push current operator.
At end: pop all remaining operators to output.
```

Operator precedence: `^` > `*, /` > `+, −`. Right-associative for `^`.

### 1.6 Queue (FIFO)

**First In First Out**. Operations:

| Operation | Description | Time |
|---|---|---|
| `enqueue(x)` | Insert at rear | O(1) |
| `dequeue()` | Remove from front | O(1) |
| `front()` | View front | O(1) |
| `isEmpty()` / `isFull()` | Check | O(1) |

### 1.7 Queue Implementations

**Array (linear):**
- Front and rear indices.
- Naive enqueue/dequeue → wasted space (front moves forward).
- **Circular queue** wraps indices to reuse space.

**Circular queue conditions:**
- Empty: `front == rear`
- Full: `(rear + 1) % size == front` (one slot wasted)
- Or use a `count` variable to differentiate.

**Linked list:** head + tail pointers; both ops O(1).

### 1.8 Variants of Queue

| Variant | Description |
|---|---|
| **Deque (Double-ended queue)** | Insert/delete at both ends |
| **Priority queue** | Dequeue based on priority (heap) |
| **Circular queue** | Wraps around |
| **Double-ended priority queue** | Min and max access |

### 1.9 Queue Applications

- BFS in graphs.
- CPU scheduling (round-robin).
- I/O buffering.
- Print spooler.

### 1.10 Linked List

A sequence of nodes; each node has data + pointer to next.

**Types:**
- **Singly linked:** node → next.
- **Doubly linked:** node ↔ prev/next.
- **Circular linked:** last node points back to first.
- **Doubly circular:** last → first; first → last.

### 1.11 Singly Linked List Operations

| Operation | Time |
|---|---|
| Access by index | O(n) |
| Insert at head | O(1) |
| Insert at tail (no tail ptr) | O(n) |
| Insert at tail (with tail ptr) | O(1) |
| Insert after given node | O(1) |
| Delete head | O(1) |
| Delete given node | O(1) (with prev pointer) |
| Search | O(n) |

### 1.12 Doubly Linked List

Each node has prev + next pointers.

**Pros:** bidirectional traversal, O(1) deletion of any node (given pointer).
**Cons:** extra pointer storage.

### 1.13 Circular Linked List

Last node's `next` points to first node.
- Useful for round-robin scheduling.
- Can have only `tail` pointer; head = tail->next.

### 1.14 Common Operations: Traversal & Reversal

**Reverse singly linked list (iterative):**
```c
prev = NULL;
curr = head;
while (curr) {
    next = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
}
head = prev;
```

**Reverse recursive:**
```c
Node* reverse(Node* h) {
    if (!h || !h->next) return h;
    Node* p = reverse(h->next);
    h->next->next = h;
    h->next = NULL;
    return p;
}
```

### 1.15 Detect Cycle (Floyd's Tortoise & Hare)

```c
slow = fast = head;
while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
    if (slow == fast) return true;  // cycle
}
return false;
```

### 1.16 Stack via Linked List

`push`: insert at head; `pop`: remove from head. Both O(1).

### 1.17 Queue via Two Stacks

Use stack S1 for enqueue, S2 for dequeue.
- Enqueue: push onto S1.
- Dequeue: if S2 empty, pop all from S1 to S2; then pop from S2.

Amortized O(1) per operation.

### 1.18 Stack via Two Queues

Possible but each push (or pop) is O(n).

### 1.19 Memory Considerations

Linked lists have **per-node overhead** (next pointer = 4–8 bytes). For 32-bit integers + 8-byte pointer, overhead is 100%.

Arrays are more cache-friendly (contiguous).

### 1.20 Skip Lists (preview)

Probabilistic linked lists with multiple levels — O(log n) average operations. Used in concurrent data structures.

> **Summary:** Stack = LIFO, Queue = FIFO. Master implementations (array vs LL), expression evaluation, circular queue full/empty conditions, linked list manipulations (insert/delete/reverse/cycle detection). Time complexities are key.

---

## 2. Important Points

- **Stack:** LIFO, push/pop both O(1) with array (top index) or LL (head).
- **Stack overflow** in array implementation if size exceeded.
- **Postfix evaluation:** push operands, on operator pop two, push result.
- **Infix to postfix:** uses operator stack with precedence rules.
- **Queue array implementation** wastes space without circularity.
- **Circular queue full:** (rear + 1) % N == front (with one slot wasted).
- **Circular queue empty:** front == rear.
- **Deque** allows both-ended ops; useful for sliding-window problems.
- **Priority queue** typically heap-based (binary heap, O(log n)).
- **Singly linked list:** insertion at known position O(1); search/access O(n).
- **Doubly linked list:** O(1) deletion given node pointer.
- **Circular linked list:** no NULL sentinel; last → first.
- **Floyd's cycle detection:** slow/fast pointers; meets if cycle exists.
- **Stack via two queues** has O(n) ops; **queue via two stacks** has amortized O(1).
- **In-order array of stack:** top is at end if stack grows up.

---

## 3. Short Notes

```
STACK (LIFO)
 push, pop, top, isEmpty
 O(1) all ops
 implementations: array (top idx) or LL (head)

QUEUE (FIFO)
 enqueue (rear), dequeue (front)
 O(1) all ops with proper impl
 array → circular for space reuse
 linked: head + tail pointers

CIRCULAR QUEUE
 empty: front == rear
 full: (rear+1) % N == front (1 slot wasted)
 or count variable

POSTFIX EVAL
 stack-based, push operands, op pops two

INFIX → POSTFIX (shunting-yard)
 op precedence: ^ > * / > + −
 right-assoc ^

LINKED LIST
 singly / doubly / circular / DC

LL OPERATIONS
 access[i]: O(n)
 insert head: O(1); tail: O(1) w/ tail ptr
 delete head: O(1); given node: O(1) w/ prev
 search: O(n)

DOUBLY LL
 prev + next pointers
 bidirectional, easy delete

REVERSE (iterative)
 prev=NULL; curr=head
 next = curr->next; curr->next=prev; prev=curr; curr=next

CYCLE DETECT (Floyd)
 slow = next, fast = next->next; meet ⇒ cycle

STACK from LL
 push/pop at head: O(1)

QUEUE from 2 STACKS
 enqueue → S1; dequeue → S2 (refill if empty)
 amortized O(1)

DEQUE: both ends; PQ: heap

APPLICATIONS
 stack: recursion, expr eval, parens
 queue: BFS, scheduling, buffer
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Stack ops O(1) | ✅✅ |
| 2 | Queue ops O(1) (proper impl) | ✅✅ |
| 3 | Circular queue full/empty conditions | ✅✅ |
| 4 | Postfix evaluation: stack-based | ✅✅ |
| 5 | Infix → postfix: shunting-yard | ✅✅ |
| 6 | Singly LL access O(n), insert head O(1) | ✅✅ |
| 7 | Doubly LL O(1) delete given ptr | ✅ |
| 8 | Floyd's cycle detection | ✅✅ |
| 9 | Stack from LL: head as top | ✅ |
| 10 | Queue from 2 stacks: amortized O(1) | ✅ |
| 11 | DLL has 2× pointer space of SLL | ✅ |
| 12 | Reverse SLL: iterative or recursive | ✅ |

### Tricks

- **Validating parens:** push opening; on closing, check top matches.
- **Min-stack:** maintain auxiliary stack of minimums.
- **Sliding window max:** deque-based, O(n) total.
- **Detect cycle start (Floyd):** after meeting, reset slow to head; advance both by 1.
- **Reverse DLL:** swap prev and next of each node.
- **Convert prefix → infix:** stack of strings, pop two on operator.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Postfix evaluation of `5 6 2 + * 12 4 / -`:
**Solution.**
- Push 5, 6, 2.
- `+`: 6+2=8; stack: 5, 8.
- `*`: 5·8 = 40; stack: 40.
- Push 12, 4.
- `/`: 12/4=3; stack: 40, 3.
- `-`: 40−3 = 37.
**Answer: 37.**

### Q2. (GATE CSE 2014)
A circular queue of capacity 6 with front=2, rear=4. # elements?
**Solution.** (rear − front + N) mod N = (4 − 2 + 6) mod 6 = 2.

### Q3. (GATE CSE 2018)
Singly LL with 1000 nodes; insert at head: time?
**Solution.** O(1).

### Q4. (GATE CSE 2008)
Convert infix `(A + B) * C - D` to postfix:
**Solution.** AB+C*D−.

### Q5. (GATE CSE 2010)
A queue is implemented using a circular array of size n. Maximum elements stored?
**Solution.** n − 1 (one slot wasted) or n (with separate count variable).

### Q6. (GATE CSE 2015)
Output of postfix `2 3 4 + *`:
**Solution.** 3+4=7; 2·7 = 14.

### Q7. (GATE CSE 2013)
Stack: push 1,2,3; pop; push 4; pop; pop. Final state of stack?
**Solution.** [1] (only 1 remains).

### Q8. (GATE CSE 2007)
Doubly linked list with n nodes: # of pointer fields?
**Solution.** 2n.

### Q9. (GATE CSE 2003)
Floyd's algorithm detects:
**Solution.** Cycle in linked list.

### Q10. (GATE CSE 2009)
Reverse a singly linked list of n nodes: time?
**Solution.** O(n).

### Q11. (GATE CSE 2019)
Implementing queue with two stacks: amortized cost?
**Solution.** O(1).

### Q12. (GATE CSE 2020)
Min-stack supports getMin in O(1) using:
**Solution.** Auxiliary stack tracking running minimum.

### Q13. (GATE CSE 2021)
Validating balanced parens uses:
**Solution.** Stack.

### Q14. (GATE CSE 2016)
A circular linked list has n nodes. To find the last node:
**Solution.** O(n).

### Q15. (GATE CSE 2011)
Operation that's slower in array-based stack vs LL-based stack:
**Solution.** Stack overflow handling — array has fixed size; LL grows dynamically.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Stack push/pop time complexity?

**P2.** What is FIFO?

**P3.** Postfix of `A + B`?

**P4.** Convert infix `(A − B) * C` to postfix.

**P5.** Evaluate postfix: `5 6 + 2 *`.

**P6.** Define deque.

**P7.** Singly LL search time?

**P8.** Doubly LL has how many pointers per node?

**P9.** Empty condition of circular queue?

**P10.** Detect cycle in LL: which algorithm?

### Medium

**P11.** Convert `A + B * C / (D - E)` to postfix.

**P12.** Implement reverse of LL iteratively.

**P13.** Circular queue capacity 5; sequence enqueue 5 elements then dequeue 2 then enqueue 2. Show front, rear, contents.

**P14.** Stack vs queue: which uses LIFO?

**P15.** Build min-stack supporting getMin O(1).

**P16.** Implement queue using 2 stacks; show enqueue/dequeue.

**P17.** Detect cycle in LL with Floyd's algorithm; show pointer movement.

**P18.** Reverse a doubly linked list.

**P19.** Sliding window max using deque.

**P20.** Convert prefix `+ * 2 3 4` to infix and postfix.

### Hard

**P21.** Implement a stack with O(1) push, pop, getMin, getMax.

**P22.** Find middle of LL in single pass.

**P23.** Merge two sorted linked lists.

**P24.** Detect intersection point of two linked lists.

**P25.** Implement deque using doubly linked list.

**P26.** Trace evaluation of postfix `7 8 + 3 * 1 -`.

**P27.** Find loop start node after Floyd detects cycle.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | O(1) | direct |
| P2 | First in first out | direct |
| P3 | AB+ | direct |
| P4 | AB-C* | direct |
| P5 | 22 | direct |
| P6 | both-ended queue | direct |
| P7 | O(n) | direct |
| P8 | 2 | direct |
| P9 | front == rear | direct |
| P10 | Floyd | direct |
| P11 | ABC*DE-/+ | direct |
| P12 | iterative reverse | direct |
| P13 | trace | direct |
| P14 | stack | direct |
| P15 | aux stack | direct |
| P16 | enqueue → S1; dequeue → S2 | direct |
| P17 | trace | direct |
| P18 | swap prev/next | direct |
| P19 | deque maintains decreasing | direct |
| P20 | infix: ((2*3)+4); postfix: 23*4+ | direct |
| P21 | track min/max in aux stacks | direct |
| P22 | slow/fast pointer | direct |
| P23 | classic merge | direct |
| P24 | length diff or two-pointer | direct |
| P25 | enq/dq O(1) at both ends | direct |
| P26 | 7+8=15; 15·3=45; 45−1=44 | direct |
| P27 | reset slow to head, advance both | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing stack and queue order | LIFO vs FIFO. |
| 2 | Off-by-one in circular queue | Track full/empty carefully. |
| 3 | Forgetting tail pointer for O(1) tail insert in LL | Use tail. |
| 4 | Reversing LL but losing head | Use prev/curr/next pattern. |
| 5 | Cycle detection wrong condition | fast && fast->next. |
| 6 | Stack overflow in recursion | Limit depth. |
| 7 | Mixing infix/postfix precedence | Memorize precedence. |
| 8 | Treating singly LL as bidirectional | No prev pointer. |
| 9 | Forgetting one slot wasted in circular queue | (rear+1) mod N == front. |
| 10 | Empty queue dequeue undefined | Check empty first. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Evaluate postfix" | Stack-based; push operands. |
| "Convert infix to postfix" | Shunting-yard. |
| "Reverse linked list" | iterative prev/curr/next or recursive. |
| "Detect cycle in LL" | Floyd's slow/fast pointers. |
| "Find middle of LL" | slow/fast pointers. |
| "Implement queue with stacks" | Two stacks, amortized O(1). |
| "Implement stack with queues" | Two queues. |
| "Min/Max in O(1)" | Auxiliary stack. |
| "Sliding window max" | Deque. |
| "Balanced parens" | Stack. |
| "Round-robin" | Circular queue. |

---

## 9. Quick Revision

```
STACK (LIFO): push/pop O(1)
 array (top idx) or LL (head)

QUEUE (FIFO): enq/dq O(1)
 circular array or LL (head+tail)

CIRCULAR QUEUE
 empty: front == rear
 full: (rear+1) % N == front

POSTFIX EVAL: push operand, op pops 2

INFIX→POSTFIX (shunting-yard)
 prec: ^ > * / > + −
 right-assoc ^

LINKED LIST
 singly / doubly / circular
 access O(n); insert head O(1)
 doubly: O(1) delete given pointer

REVERSE
 iterative: prev/curr/next swap
 recursive: reverse rest, fix pointers

CYCLE: Floyd's slow/fast

STACK from LL: head = top
QUEUE from 2 STACKS: amortized O(1)
DEQUE: both ends
PQ: heap

APPLICATIONS
 stack: recursion, parens, expr
 queue: BFS, scheduling
 deque: sliding window
```
