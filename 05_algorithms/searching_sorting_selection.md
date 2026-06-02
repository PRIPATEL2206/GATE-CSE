# Searching, Sorting & Selection

> Subject: Algorithms
> GATE weight: **3–5 marks** every year. All sorting algorithms, complexity tables, in-place/stable, selection.

---

## 1. Concept Explanation

### 1.1 Searching

| Algorithm | Best | Avg | Worst | Space | Notes |
|---|---|---|---|---|---|
| Linear search | O(1) | O(n) | O(n) | O(1) | works on unsorted |
| Binary search | O(1) | O(log n) | O(log n) | O(1) iterative, O(log n) recursive | sorted array required |
| Ternary search | O(1) | O(log₃ n) | O(log₃ n) | O(1) | uses 2 comparisons/round |
| Jump search | O(1) | O(√n) | O(√n) | O(1) | sorted array |
| Interpolation search | O(1) | O(log log n) | O(n) | O(1) | uniform distribution best |

### 1.2 Binary Search

```c
int bsearch(int *a, int lo, int hi, int t) {
    while (lo <= hi) {
        int m = lo + (hi - lo) / 2;     // avoid overflow
        if (a[m] == t) return m;
        if (a[m] < t) lo = m + 1;
        else hi = m - 1;
    }
    return -1;
}
```

`T(n) = T(n/2) + O(1) → O(log n)`.

### 1.3 Sorting Overview Table

| Algorithm | Best | Average | Worst | Space | Stable | In-place |
|---|---|---|---|---|---|---|
| **Bubble sort** | O(n) | O(n²) | O(n²) | O(1) | ✅ | ✅ |
| **Selection sort** | O(n²) | O(n²) | O(n²) | O(1) | ❌ | ✅ |
| **Insertion sort** | O(n) | O(n²) | O(n²) | O(1) | ✅ | ✅ |
| **Merge sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ | ❌ |
| **Quick sort** | O(n log n) | O(n log n) | O(n²) | O(log n) avg | ❌ | ✅ |
| **Heap sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ | ✅ |
| **Counting sort** | O(n + k) | O(n + k) | O(n + k) | O(n + k) | ✅ | ❌ |
| **Radix sort** | O(d(n + k)) | O(d(n + k)) | O(d(n + k)) | O(n + k) | ✅ | ❌ |
| **Bucket sort** | O(n + k) | O(n) | O(n²) | O(n) | ✅ | ❌ |
| **Shell sort** | O(n log n) | O(n^1.25) | O(n²) | O(1) | ❌ | ✅ |
| **Tree sort** | O(n log n) | O(n log n) | O(n²) | O(n) | depends | ❌ |

(k = range of keys; d = # digits.)

### 1.4 Bubble Sort

Pass through array; swap adjacent if out of order. Largest "bubbles" to end.

```c
for (i = 0; i < n-1; i++)
  for (j = 0; j < n-1-i; j++)
    if (a[j] > a[j+1]) swap(a[j], a[j+1]);
```

Best case O(n) with early termination flag (no swaps in a pass).

### 1.5 Selection Sort

Find min, swap to position 0. Find next min, swap to position 1. Etc.

Always O(n²); minimum swaps among O(n²) algorithms.

### 1.6 Insertion Sort

Build sorted prefix one element at a time; shift others to make room.

Best case O(n) when already sorted. Good for small or nearly-sorted data.

### 1.7 Merge Sort

Divide-and-conquer:
1. Split into halves.
2. Recursively sort each.
3. Merge sorted halves.

`T(n) = 2T(n/2) + n → Θ(n log n)`.

**Stable, not in-place** (needs O(n) auxiliary space).

### 1.8 Merge Procedure

```c
merge(a, lo, mid, hi):
  copy a[lo..mid] to L; a[mid+1..hi] to R
  i=0, j=0, k=lo
  while i<|L| and j<|R|:
    if L[i] <= R[j]: a[k++] = L[i++];
    else: a[k++] = R[j++];
  copy remaining
```

### 1.9 Quick Sort

1. Choose **pivot**.
2. Partition: elements ≤ pivot to left, > to right.
3. Recursively sort both halves.

Average O(n log n); worst O(n²) when pivots are extreme.

**Lomuto partition (simple):**
```c
int partition(int *a, int lo, int hi) {
    int pivot = a[hi];
    int i = lo - 1;
    for (int j = lo; j < hi; j++)
      if (a[j] <= pivot) swap(a[++i], a[j]);
    swap(a[i+1], a[hi]);
    return i+1;
}
```

**Hoare partition (faster):** uses two pointers from ends.

### 1.10 Quick Sort Worst Case

Sorted array with last element as pivot → all elements go to one side.

**Fix:**
- Random pivot.
- Median-of-three.
- Median-of-medians (for guaranteed O(n log n)).

### 1.11 Heap Sort

1. Build max-heap from array: O(n).
2. Repeatedly swap root with last; reduce heap size; sift down: O(n log n).

In-place; not stable.

### 1.12 Counting Sort

For integers in range [0, k]:
1. Count occurrences.
2. Compute prefix sums.
3. Place each in correct position.

**Time: O(n + k); Space: O(n + k).** Linear when k = O(n).

Stable.

### 1.13 Radix Sort

Sort by least significant digit, then next, etc., using stable subroutine (counting sort).

Time: **O(d(n + k))** where d = # of digits.

For 32-bit integers and 256 buckets: 4 passes → O(n).

### 1.14 Bucket Sort

Distribute into buckets based on uniform key distribution; sort each bucket.

Average O(n) under uniformity; worst O(n²) if all in one bucket.

### 1.15 Lower Bound for Comparison Sort

Any comparison-based sort requires **Ω(n log n)** comparisons. Proved via decision tree:

`# leaves = n!` ; `height ≥ log₂(n!) = Ω(n log n)`.

### 1.16 Stability

A sort is **stable** if equal elements preserve their relative order.

| Stable | Not Stable |
|---|---|
| Bubble, Insertion, Merge, Counting, Radix | Selection, Quick, Heap, Shell |

### 1.17 In-Place

A sort is **in-place** if it uses O(1) or O(log n) extra space.

| In-place | Not in-place |
|---|---|
| Bubble, Selection, Insertion, Quick, Heap, Shell | Merge, Counting, Radix, Bucket |

### 1.18 Selection Problem (k-th smallest)

Find k-th smallest element in unsorted array.

**Approaches:**
- Sort + index: O(n log n).
- Min-heap of size n + k extracts: O(n + k log n).
- Max-heap of size k: O(n log k).
- **QuickSelect:** average O(n), worst O(n²).
- **Median-of-medians (BFPRT):** worst-case O(n).

### 1.19 QuickSelect

Like quicksort but recurse into only **one** partition.

```c
int quickselect(int *a, int lo, int hi, int k) {
    if (lo == hi) return a[lo];
    int p = partition(a, lo, hi);
    if (p == k) return a[p];
    if (k < p) return quickselect(a, lo, p-1, k);
    return quickselect(a, p+1, hi, k);
}
```

`T(n) = T(n/2) + n → O(n) average`.

### 1.20 Sorting Use-Cases

| Situation | Use |
|---|---|
| Small n (< 50) | Insertion sort |
| Large n, general | Quicksort or Mergesort |
| External (data > RAM) | External merge sort |
| Stability required | Merge sort |
| In-place required | Heap sort or quick sort |
| Integer keys, small range | Counting sort |
| Many small numbers | Radix sort |
| k smallest | Heap or QuickSelect |

> **Summary:** Memorize the complexity table cold. Master merge/quick/heap/insertion sort algorithms. Lower bound for comparison sort = Ω(n log n). QuickSelect is O(n) average for k-th order statistic.

---

## 2. Important Points

- **Linear search** works on unsorted arrays; binary search requires sorted.
- **Comparison sort lower bound:** Ω(n log n).
- **Counting/radix/bucket** beat the bound by exploiting key structure.
- **Quicksort worst case** O(n²) on already-sorted data with poor pivot.
- **Mergesort is stable**; quicksort and heapsort are not.
- **Heap sort** is in-place; merge sort is not.
- **Counting sort time** O(n + k); great when k = O(n).
- **Radix sort** uses d passes of stable subsort.
- **Insertion sort** great for small n or nearly sorted (best case O(n)).
- **QuickSelect** average O(n) for k-th element.
- **Median-of-medians** gives worst-case O(n) selection.
- **For best vs worst:** quicksort = O(n²) worst; merge = O(n log n) worst.
- **Adaptive sorts** (insertion, bubble) faster on partially sorted input.
- **Hybrid sorts** (Timsort, Introsort) used in standard libraries.

---

## 3. Short Notes

```
SEARCH
 linear: O(n)
 binary: O(log n) (sorted)
 jump: O(√n) (sorted)
 interpolation: O(log log n) avg, O(n) worst (uniform)

COMPARISON SORT LOWER BOUND: Ω(n log n)

SORTING TABLE
 bubble: best n, avg/worst n²; stable, in-place
 selection: n²; not stable, in-place
 insertion: best n, avg/worst n²; stable, in-place
 merge: n log n; stable, not in-place
 quick: avg n log n, worst n²; not stable, in-place
 heap: n log n; not stable, in-place
 counting: O(n+k); stable, not in-place
 radix: O(d(n+k)); stable, not in-place
 bucket: avg O(n); stable, not in-place

QUICKSORT
 partition (Lomuto/Hoare)
 random pivot or median-of-3 to avoid worst case

MERGESORT
 T(n) = 2T(n/2) + n
 stable, O(n) extra space

HEAPSORT
 build-heap O(n)
 n extracts × log n
 in-place, not stable

COUNTING SORT
 count occurrences, prefix sum, place
 O(n+k), stable

RADIX SORT
 LSD or MSD, stable subroutine
 O(d(n+k))

SELECTION (k-th smallest)
 sort + index: O(n log n)
 heap of k: O(n log k)
 quickselect: O(n) avg
 median-of-medians: O(n) worst

STABLE: bubble, insertion, merge, counting, radix
IN-PLACE: bubble, selection, insertion, quick, heap

USE
 small n: insertion
 stable: merge
 in-place general: heap or quick
 small key range: counting
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Comparison sort lower bound: Ω(n log n) | ✅✅ |
| 2 | Quicksort worst O(n²); average O(n log n) | ✅✅ |
| 3 | Mergesort O(n log n) all cases | ✅✅ |
| 4 | Heapsort O(n log n) all cases | ✅✅ |
| 5 | Counting sort O(n+k) | ✅✅ |
| 6 | Radix sort O(d(n+k)) | ✅ |
| 7 | Insertion best O(n), worst O(n²) | ✅✅ |
| 8 | Binary search O(log n) | ✅✅ |
| 9 | QuickSelect average O(n) | ✅✅ |
| 10 | Median-of-medians worst O(n) | ✅ |
| 11 | Stability table (merge/insertion stable) | ✅ |
| 12 | In-place table (heap/quick in-place) | ✅ |

### Tricks

- **For nearly sorted data:** insertion sort → O(n).
- **For small k in k-th smallest:** heap of size k → O(n log k).
- **For large arrays with integer keys:** counting/radix beats comparison.
- **For partial sort / select:** QuickSelect.
- **Partition correctness:** ensure pivot is at correct final index.
- **Counting sort stable:** iterate from end when placing.
- **Median-of-medians:** divides into groups of 5, finds medians, recurses.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Quicksort worst case:
**Solution.** O(n²) — sorted input with last as pivot.

### Q2. (GATE CSE 2014)
Merge sort time complexity:
**Solution.** O(n log n) all cases.

### Q3. (GATE CSE 2018)
Lower bound on comparison-based sort:
**Solution.** Ω(n log n).

### Q4. (GATE CSE 2008)
Insertion sort best case:
**Solution.** O(n) — already sorted.

### Q5. (GATE CSE 2010)
Binary search on n elements:
**Solution.** O(log n).

### Q6. (GATE CSE 2015)
QuickSelect average:
**Solution.** O(n).

### Q7. (GATE CSE 2013)
Counting sort space:
**Solution.** O(n + k).

### Q8. (GATE CSE 2007)
Heap sort in-place?
**Solution.** Yes.

### Q9. (GATE CSE 2003)
Stable sorts: bubble, insertion, merge, counting?
**Solution.** All yes.

### Q10. (GATE CSE 2009)
Radix sort time:
**Solution.** O(d(n + k)).

### Q11. (GATE CSE 2019)
Find median in O(n):
**Solution.** Median-of-medians.

### Q12. (GATE CSE 2020)
Quicksort with random pivot — expected time:
**Solution.** O(n log n).

### Q13. (GATE CSE 2021)
External sort algorithm:
**Solution.** External merge sort.

### Q14. (GATE CSE 2016)
Number of comparisons in worst-case binary search on 1024 elements:
**Solution.** ⌈log₂ 1024⌉ + 1 = 11.

### Q15. (GATE CSE 2011)
Insertion sort on reversed array:
**Solution.** O(n²) (worst case).

---

## 6. Practice Questions (20+)

### Easy

**P1.** Worst case of quicksort?

**P2.** Best case of insertion sort?

**P3.** Time of binary search on n elements?

**P4.** Is mergesort stable?

**P5.** Is heapsort in-place?

**P6.** Counting sort time?

**P7.** Lower bound for comparison sort?

**P8.** k-th smallest in O(n) average?

**P9.** Selection sort time?

**P10.** Adaptive sort: name one.

### Medium

**P11.** Bubble sort vs selection sort comparisons.

**P12.** Quicksort with random pivot expected time.

**P13.** Mergesort space complexity.

**P14.** Find min and max in n elements with min comparisons.

**P15.** Sort 5 integers in [0, 10] — best algorithm?

**P16.** Find k-th smallest using heap.

**P17.** External merge sort use case.

**P18.** Counting sort: stability.

**P19.** Radix sort: when fastest?

**P20.** Number of swaps in selection sort worst-case?

### Hard

**P21.** Median-of-medians algorithm steps.

**P22.** Why is quicksort worst-case O(n²)?

**P23.** Can quicksort be made O(n log n) worst case?

**P24.** Find pair of elements summing to k in sorted array O(n).

**P25.** Sorting linked list — best algorithm?

**P26.** Sort large file (size > RAM)?

**P27.** Compare insertion sort vs mergesort for n = 30.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | O(n²) | direct |
| P2 | O(n) | already sorted |
| P3 | O(log n) | direct |
| P4 | yes | stable |
| P5 | yes | in-place |
| P6 | O(n+k) | direct |
| P7 | Ω(n log n) | direct |
| P8 | quickselect | direct |
| P9 | O(n²) | direct |
| P10 | insertion sort | direct |
| P11 | bubble has more swaps | direct |
| P12 | O(n log n) | direct |
| P13 | O(n) | direct |
| P14 | 3n/2 - 2 comparisons | tournament |
| P15 | counting sort | direct |
| P16 | min-heap of all + k extracts; or max-heap of size k | direct |
| P17 | data > RAM | direct |
| P18 | stable | direct |
| P19 | small d, integer keys | direct |
| P20 | O(n) swaps; n−1 max | direct |
| P21 | groups of 5 → medians → median of medians | direct |
| P22 | extreme pivot all to one side | direct |
| P23 | yes (median pivot) | direct |
| P24 | two pointers | direct |
| P25 | mergesort (no random access penalty) | direct |
| P26 | external merge sort | direct |
| P27 | insertion sort competitive for small n | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Quicksort always O(n log n) (myth) | Worst is O(n²). |
| 2 | Mergesort in-place (myth) | Needs O(n) auxiliary. |
| 3 | Heap sort stable (myth) | Not stable. |
| 4 | Counting sort O(n) always | Only when k = O(n). |
| 5 | Insertion sort = bubble sort | Different algorithms. |
| 6 | Linear search needs sorted (myth) | No. |
| 7 | Binary search on unsorted | Doesn't work. |
| 8 | Forgetting comparison-sort lower bound | Ω(n log n). |
| 9 | Treating QuickSelect worst case as O(n) | Worst is O(n²); medians-of-medians is O(n). |
| 10 | Radix sort works on floats? | Generally not directly. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Sort in O(n)" | Counting/radix/bucket if applicable. |
| "Stable sort" | Merge/insertion/counting/radix. |
| "In-place sort" | Heap/quick/bubble/insertion. |
| "k-th smallest" | QuickSelect or heap. |
| "Worst-case of quicksort" | O(n²). |
| "Lower bound comparison sort" | Ω(n log n). |
| "External / large data" | External merge sort. |
| "Nearly sorted" | Insertion sort. |
| "Sort + binary search use case" | O(n log n) preprocessing. |
| "Find median in O(n)" | Median-of-medians. |

---

## 9. Quick Revision

```
SEARCH
 linear O(n)
 binary O(log n) (sorted)
 jump O(√n)
 interpolation O(log log n) avg

SORT TABLE
 bubble: O(n²) avg/worst, O(n) best; stable, in-place
 selection: O(n²); not stable, in-place
 insertion: O(n) best, O(n²) worst; stable, in-place
 merge: O(n log n); stable, not in-place
 quick: avg O(n log n), worst O(n²); not stable, in-place
 heap: O(n log n); not stable, in-place
 counting: O(n+k); stable, not in-place
 radix: O(d(n+k)); stable
 bucket: O(n) avg; stable

LOWER BOUND comparison: Ω(n log n)

QUICKSORT
 partition: Lomuto/Hoare
 worst: sorted with bad pivot
 fix: random / median-of-3 / median-of-medians

MERGESORT: divide-conquer-merge

HEAPSORT: build + extract loop

COUNTING / RADIX / BUCKET: integer / uniform keys

SELECTION (k-th)
 sort: O(n log n)
 heap: O(n log k)
 quickselect: O(n) avg
 median-of-medians: O(n) worst

STABLE: bubble, insertion, merge, counting, radix
IN-PLACE: bubble, selection, insertion, quick, heap
```
