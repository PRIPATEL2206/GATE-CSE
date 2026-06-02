# C Programming (Pointers, Arrays, Recursion, Scope)

> Subject: Programming & Data Structures
> GATE weight: **3–6 marks** every year. Pointer arithmetic, output prediction, recursion tracing, storage classes.

---

## 1. Concept Explanation

### 1.1 Variables, Storage Classes & Scope

| Storage Class | Lifetime | Scope | Default Value |
|---|---|---|---|
| `auto` | Block | Block (default for local) | Garbage |
| `static` (local) | Whole program | Block | 0 |
| `static` (global) | Whole program | File | 0 |
| `extern` | Whole program | Global (cross-file) | 0 |
| `register` | Block | Block (hint to use register) | Garbage |

**Block scope:** variables declared inside `{ }` visible only inside.
**Function scope:** entire function body.
**File scope:** declared outside any function, no `static`.

### 1.2 Memory Layout of a C Program

```
| Stack (grows down)       |  Local variables, function frames
| ↓                        |
| ↑                        |
| Heap (grows up)          |  malloc/calloc allocations
| BSS (uninit. globals)    |  Initialized to 0
| Data (init. globals)     |  Initialized values
| Text (code)              |  Read-only program code
```

### 1.3 Pointers

A **pointer** stores a memory address.

```c
int x = 10;
int *p = &x;        // p holds address of x
int y = *p;         // y = 10 (dereference)
```

**Operations:**
- `&` — address-of
- `*` — dereference
- `++`, `--` — pointer increment/decrement (by sizeof type)

### 1.4 Pointer Arithmetic

For `int *p`:
- `p + 1` → `p + sizeof(int)` bytes (typically `p + 4`).
- `p[i]` ≡ `*(p + i)`.

### 1.5 Arrays vs Pointers

- An array name is a **pointer to its first element** (in most contexts).
- `arr[i]` ≡ `*(arr + i)` ≡ `*(i + arr)` ≡ `i[arr]` (legal but ugly).

Differences:
- `sizeof(arr)` = full array size (in bytes).
- `sizeof(ptr)` = pointer size (typically 4 or 8).
- Cannot reassign array name; can reassign pointers.

### 1.6 Multi-dimensional Arrays

```c
int a[3][4];        // 3 rows × 4 cols
a[i][j] = *(*(a+i) + j);
```

**Row-major storage:** `a[i][j]` at offset `(i * cols + j) * sizeof(elem)`.

### 1.7 Pointers to Pointers

```c
int x = 5;
int *p = &x;
int **pp = &p;
**pp == 5;
```

### 1.8 Functions and Pass-by-Value

C is **pass-by-value**.
- Modifying parameter inside function doesn't change caller's variable.
- To "modify" caller's data, pass a pointer to it.

### 1.9 Function Pointers

```c
int (*fp)(int, int);  // fp is a pointer to function (int, int) → int
fp = &add;
result = fp(2, 3);
```

### 1.10 Dynamic Memory

| Function | Purpose |
|---|---|
| `malloc(n)` | Allocates n bytes; returns void*. Uninitialized. |
| `calloc(n, sz)` | Allocates n·sz bytes; zeroed. |
| `realloc(p, n)` | Resize block at p. |
| `free(p)` | Releases memory. |

`malloc` returns `NULL` on failure.

### 1.11 Strings

A **C string** is an array of `char` terminated by `'\0'`.

```c
char s[] = "hello";   // 6 bytes (incl. '\0')
char *p = "hello";    // pointer to string literal (read-only)
```

**Common functions:** `strlen`, `strcpy`, `strcmp`, `strcat`, `strncpy`, etc.

### 1.12 Structures & Unions

```c
struct Point { int x, y; };
struct Point p = {1, 2};
p.x = 5;

struct Point *pp = &p;
pp->x = 10;            // == (*pp).x
```

**Union:** all members share the same memory.

### 1.13 Recursion

Function calls itself. Each call has its own stack frame with local variables.

**Examples:**
- Factorial: `f(n) = 1 if n=0; n·f(n−1) otherwise`
- Fibonacci: `f(n) = f(n−1) + f(n−2)` (with base cases)
- Tree traversal, GCD (Euclidean)

**Tail recursion:** recursive call is the last action — can be optimized to iteration.

### 1.14 Recursion Tree & Stack Depth

For `f(n)` with one recursive call: depth = O(n) frames. Each frame holds local vars.

For Fibonacci with two calls: stack depth = n; total calls ≈ φⁿ (exponential).

### 1.15 Operator Precedence (Common GATE Confusions)

| Operators | Associativity |
|---|---|
| `()`, `[]`, `->`, `.` | Left to right |
| `++`, `--` (postfix) | Left to right |
| `++`, `--`, `!`, `~`, unary `*`, `&`, `(type)`, `sizeof` | Right to left |
| `*`, `/`, `%` | Left to right |
| `+`, `−` | Left to right |
| `<<`, `>>` | Left to right |
| `<`, `<=`, `>`, `>=` | Left to right |
| `==`, `!=` | Left to right |
| `&` | Left to right |
| `^` | Left to right |
| `|` | Left to right |
| `&&` | Left to right |
| `||` | Left to right |
| `?:` | Right to left |
| `=`, `+=`, etc. | Right to left |

### 1.16 Pre/Post Increment

- `++a` (prefix): increment first, then use new value.
- `a++` (postfix): use current value, then increment.

```c
int a = 5;
int b = a++ + ++a;
// First: a++ uses 5, then a=6; ++a: a=7, value 7
// b = 5 + 7 = 12; final a = 7
```

(Be wary of unspecified evaluation order; this expression is implementation-defined in standard C.)

### 1.17 Sequence Points

- Comma operator, `&&`, `||`, `?:`, function call.
- Between sequence points, evaluation order is unspecified.
- `i = i++ + ++i;` is **undefined behavior**.

### 1.18 typedef

`typedef` creates an alias for a type.
```c
typedef unsigned long u64;
typedef struct Node { int data; struct Node *next; } Node;
```

### 1.19 Const, Volatile, Restrict

- `const`: cannot be modified after init.
- `volatile`: tells compiler value can change unexpectedly (e.g., hardware register).
- `restrict`: pointer is the only way to access the data.

### 1.20 Common GATE Pitfalls

- `printf("%d", x)` requires int; passing wrong type → UB.
- Pointer arithmetic uses element size, not byte size.
- Returning pointer to local stack variable → UB.
- Off-by-one on string lengths.
- Unintended type promotion (`char` → `int`).

> **Summary:** Master pointer arithmetic, arrays-vs-pointers, recursion stack/depth tracing, storage class lifetimes, and operator precedence. GATE C programs are short but trap-laden.

---

## 2. Important Points

- **Array name decays to pointer to first element** in most expressions.
- `sizeof(arr)` returns total size; `sizeof(ptr)` returns pointer size (4 or 8 bytes).
- Pointer arithmetic moves by **sizeof(type)**, not by 1 byte.
- `static` local variables persist across calls and initialize **once**.
- Variables declared without `static` inside functions are **automatic** (stack-allocated).
- `malloc` does not initialize memory; `calloc` zeroes.
- **String literals** are usually stored in read-only memory.
- C uses **pass-by-value**; pointers enable indirect modification.
- **Recursion uses stack space** proportional to recursion depth.
- **Tail recursion** can sometimes be optimized to iteration.
- `int x = 5, *p = &x; *p++` increments p, returns *p before increment.
- **Operator precedence trap:** `*p++` ≡ `*(p++)`, not `(*p)++`.
- `a[i]` ≡ `*(a + i)`; works for any pointer too.
- 2D array `a[m][n]` row-major: a[i][j] at offset `i*n + j`.
- `void *` can hold any pointer; cast back to use.
- **NULL pointer dereference** → segmentation fault.

---

## 3. Short Notes

```
STORAGE CLASSES
 auto: block lifetime + scope (default local)
 static (local): persists across calls, init once, default 0
 static (global): file scope only
 extern: cross-file global
 register: hint, block scope

MEMORY LAYOUT
 stack ↓ | heap ↑ | BSS | data | text

POINTERS
 & address-of, * dereference
 p+1 advances by sizeof(type)
 array[i] == *(array + i)
 sizeof(arr) ≠ sizeof(ptr)

DYNAMIC MEM
 malloc (uninit), calloc (zero), realloc, free
 returns void*; cast or implicit assign
 NULL on failure

RECURSION
 each call: own frame on stack
 depth ≈ recursive depth
 tail-recursive optimizable
 fib has exponential calls

OPERATOR PRECEDENCE
 () [] -> .  highest
 unary (++ -- ! ~ *p &x sizeof)
 * / %, + −
 << >>
 < <= > >=
 == !=
 & ^ |
 && ||
 ?:
 = (assignments)

PRE/POST INC
 ++a: increment then use
 a++: use then increment

UB EXAMPLES
 i = i++ + ++i  (no sequence point)
 returning local pointer
 dereferencing NULL/freed

STRINGS: char[] terminated by '\0'

FUNCTION POINTERS
 int (*fp)(int, int)
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | `arr[i] == *(arr + i)` | ✅✅ |
| 2 | `p + 1` advances by sizeof(type) | ✅✅ |
| 3 | `sizeof(arr)` vs `sizeof(ptr)` | ✅✅ |
| 4 | `static` local: init once, persists | ✅ |
| 5 | C is pass-by-value | ✅ |
| 6 | `*p++` ≡ `*(p++)` | ✅ |
| 7 | `i = i++ + ++i` is UB | ✅ |
| 8 | Recursion depth ≈ stack frames | ✅ |
| 9 | 2D row-major: a[i][j] = a + i·cols + j | ✅✅ |
| 10 | `malloc` uninitialized; `calloc` zeroed | ✅ |
| 11 | NULL dereference = crash | ✅ |
| 12 | String length in bytes = strlen + 1 (for '\0') | ✅ |

### Tricks

- **Tracing pointer arithmetic:** convert to byte offsets for clarity.
- **Recursion tracing:** unfold call tree on paper.
- **Output prediction:** evaluate left-to-right when sequence points exist; otherwise UB.
- **Sizeof shortcut:** for `int arr[10]`, sizeof = 40 (assuming 4-byte int).
- **Fibonacci recursion calls:** fib(n) makes ~φⁿ calls (exponential).
- **Postfix in expressions:** the increment happens after the value is taken.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
```c
int x = 10, y = 20;
int *p = &x, *q = &y;
*p = *q;
printf("%d %d", x, y);
```
**Solution.** `*p = *q` copies y's value to x. Output: `20 20`.

### Q2. (GATE CSE 2014)
What does this print?
```c
int a[] = {1, 2, 3, 4, 5};
int *p = a + 2;
printf("%d", *p);
```
**Solution.** p points to a[2] = 3. Output: `3`.

### Q3. (GATE CSE 2018)
```c
int f(int n) {
    if (n <= 1) return n;
    return f(n-1) + f(n-2);
}
```
What's f(5)? **Solution.** Fibonacci-like: 0,1,1,2,3,5 → f(5) = 5.

### Q4. (GATE CSE 2008)
```c
static int x = 0;
void f() { x++; printf("%d ", x); }
int main() { f(); f(); f(); }
```
**Solution.** static persists. Output: `1 2 3`.

### Q5. (GATE CSE 2010)
What is sizeof("hello")?
**Solution.** 6 (5 chars + '\0').

### Q6. (GATE CSE 2015)
```c
int a[] = {1, 2, 3};
int *p = a;
printf("%d", *(p + 1));
```
**Solution.** a[1] = 2.

### Q7. (GATE CSE 2013)
```c
int x = 5;
int y = x++ + ++x;
printf("%d %d", x, y);
```
**Solution.** Implementation-defined; common interpretation: x++ uses 5, x=6; ++x makes x=7, value 7. y = 5 + 7 = 12. Final x=7. Output: `7 12`.

### Q8. (GATE CSE 2007)
What does `int *p[10]` declare?
**Solution.** An array of 10 pointers to int.

### Q9. (GATE CSE 2003)
What does `int (*p)[10]` declare?
**Solution.** A pointer to an array of 10 ints.

### Q10. (GATE CSE 2009)
Output of:
```c
char s[] = "abc";
printf("%lu", sizeof(s));
```
**Solution.** 4 (3 chars + '\0').

### Q11. (GATE CSE 2019)
```c
int f(int n) {
    if (n == 0) return 1;
    return n * f(n-1);
}
```
What is f(5)? **Solution.** 120.

### Q12. (GATE CSE 2020)
Stack depth of f(n) above when called with n=10?
**Solution.** 11 frames (n = 10, 9, …, 0).

### Q13. (GATE CSE 2021)
```c
int main() {
    int *p;
    *p = 10;        // UB: p is uninitialized
    printf("%d", *p);
}
```
**Solution.** Undefined behavior — likely segfault.

### Q14. (GATE CSE 2016)
A function pointer type for `int max(int, int)`:
**Solution.** `int (*fp)(int, int);`

### Q15. (GATE CSE 2011)
Memory layout: where is heap?
**Solution.** Between BSS and stack.

---

## 6. Practice Questions (20+)

### Easy

**P1.** What does `&x` give?

**P2.** Output:
```c
int x = 10;
int *p = &x;
printf("%d", *p);
```

**P3.** sizeof of `int a[5]` (assume 4-byte int)?

**P4.** What's the output?
```c
int x = 5;
printf("%d", x++);
```

**P5.** What is a static local variable?

**P6.** Define dangling pointer.

**P7.** What's the value of NULL?

**P8.** What header for malloc?

**P9.** What is a string in C?

**P10.** Stack depth of recursion of fact(5)?

### Medium

**P11.** Output:
```c
int a[] = {1,2,3,4,5};
int *p = a+2;
printf("%d %d", p[1], *(p-1));
```

**P12.** Trace `f(4)`:
```c
int f(int n) { if (n<2) return n; return f(n-1)+f(n-2); }
```

**P13.** What does this print?
```c
int x = 5;
int *p = &x;
*p = *p + 1;
printf("%d", x);
```

**P14.** Trace recursion calls of fib(5).

**P15.** Output:
```c
int a[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
int *p = &a[1][1];
printf("%d", *p);
```

**P16.** Difference between `char *p = "hello"` and `char p[] = "hello"`.

**P17.** What's the output?
```c
void f(int x) { x = 10; }
int main() { int a = 5; f(a); printf("%d", a); }
```

**P18.** Same problem with `f(int *x)` instead?

**P19.** Output:
```c
int main() {
    int i = 1;
    while (i <= 3) printf("%d ", i++);
}
```

**P20.** Output of `printf("%d", 5/2)` and `printf("%f", 5.0/2)`.

### Hard

**P21.** Trace recursion depth and total calls of fib(10).

**P22.** Output:
```c
int *f() { int x = 5; return &x; }
int main() { int *p = f(); printf("%d", *p); }
```
*(UB — returning pointer to local.)*

**P23.** Implement linked list reverse using recursion (pseudocode).

**P24.** Predict output:
```c
int x = 10;
int *p = &x;
int **pp = &p;
**pp = 20;
printf("%d", x);
```

**P25.** Output of:
```c
char s[] = "hello";
char *p = s;
while (*p) p++;
printf("%ld", p - s);
```

**P26.** Function returning function pointer:
```c
int (*get_op(char c))(int, int);
```
Explain.

**P27.** Recursive function for binary search:
```c
int bsearch(int *a, int lo, int hi, int t);
```
Write pseudocode.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | address of x | direct |
| P2 | 10 | dereference |
| P3 | 20 | 5·4 |
| P4 | 5 | postfix |
| P5 | persistent local | direct |
| P6 | pointer to freed memory | direct |
| P7 | 0 (or (void*)0) | direct |
| P8 | stdlib.h | direct |
| P9 | char array with '\0' | direct |
| P10 | 6 | 5,4,3,2,1,0 |
| P11 | 4 2 | direct |
| P12 | f(4)=3 | Fibonacci |
| P13 | 6 | indirect modification |
| P14 | 15 calls | exponential |
| P15 | 5 | a[1][1] |
| P16 | first read-only literal; second mutable copy | direct |
| P17 | 5 | pass-by-value |
| P18 | 10 | pass pointer |
| P19 | 1 2 3 | postfix in loop |
| P20 | 2; 2.500000 | int vs float div |
| P21 | depth 11; calls 177 | Fib calls = 2·F(n+1) − 1 |
| P22 | UB; possibly 5 | direct |
| P23 | recurse on next, then point next->next to current | direct |
| P24 | 20 | double indirection |
| P25 | 5 | strlen |
| P26 | function returning function pointer with int(int,int) signature | direct |
| P27 | base case; midpoint compare; recurse | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Confusing `*p++` with `(*p)++` | `*p++` modifies p; `(*p)++` modifies *p. |
| 2 | Returning pointer to local variable | UB — local goes out of scope. |
| 3 | Forgetting '\0' in strings | Allocate strlen+1. |
| 4 | Treating arrays as fully equivalent to pointers | sizeof differs; can't reassign array name. |
| 5 | Not free'ing malloc'd memory | Memory leak. |
| 6 | Free-ing twice | UB; double-free. |
| 7 | Using uninitialized pointer | Segfault. |
| 8 | Recursion without base case | Stack overflow. |
| 9 | Confusing pass-by-value with pass-by-reference | C doesn't have C++ refs. |
| 10 | `i = i++` in single expression | UB (no sequence point). |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Output of program with pointers" | Trace memory and dereferences. |
| "Recursion: f(n)?" | Unfold base + recursive cases. |
| "static variable" | Persistent across calls, init once. |
| "sizeof of array" | Total bytes; count elements × element size. |
| "Pass to function modifies caller variable?" | Only via pointer. |
| "Function pointer declaration" | `T (*fp)(args)`. |
| "Array of pointers vs pointer to array" | `int *p[N]` vs `int (*p)[N]`. |
| "Pre vs post increment" | Trace carefully. |
| "Memory layout" | stack/heap/BSS/data/text. |
| "Recursion depth" | Number of nested calls. |

---

## 9. Quick Revision

```
STORAGE CLASSES
 auto, static (local & global), extern, register

MEMORY: stack ↓ | heap ↑ | BSS | data | text

POINTERS
 & address-of, * dereference
 p + 1 → +sizeof(type)
 arr[i] == *(arr + i)

DYNAMIC: malloc, calloc, realloc, free
 returns void*; NULL on failure

RECURSION
 each call: stack frame
 base case mandatory
 tail-recursive can be optimized
 fib(n) ≈ φⁿ calls

PRECEDENCE TOP TO BOTTOM
 () [] -> .
 unary (++ -- ! ~ * & sizeof)
 * / %, + −
 << >>
 < <= > >=  == !=
 & ^ |  && ||
 ?:
 = (assignments)

PRE-INC: change first, use new
POST-INC: use current, then change
*p++ ≡ *(p++)

PASS-BY-VALUE in C; use pointers for indirect mutation

STRINGS: char[] + '\0'
FUNCTION POINTER: int (*fp)(int, int);

UB
 returning local addr
 NULL deref
 i = i++ + ++i
 free twice
 use after free
```
