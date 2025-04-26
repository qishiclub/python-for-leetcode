# data structure complexities

## List `list`

list is internally represented as a dynamic array. It allows for efficient random access and appending, but inserting or deleting elements at arbitrary positions can be costly due to the need to shift elements.

| Operation             | Average Case   | Worst Case     | Notes                           |
| --------------------- | -------------- | -------------- | ------------------------------- |
| Index (list[i])       | O(1)           | O(1)           | Direct access via index         |
| Append (append)       | O(1) amortized | O(1) amortized | Occasionally O(n) when resizing |
| Insert/Delete (end)   | O(1) amortized | O(1) amortized | Append/pop at end               |
| Insert/Delete (front) | O(n)           | O(n)           | Shifts subsequent elements      |
| Membership (x in l)   | O(n)           | O(n)           | Linear search                   |
| Pop (pop)             | O(1) (end)     | O(n) (front)   | O(1) for pop(), O(n) for pop(i) |
| Sort (sort())         | O(n log n)     | O(n log n)     | Timsort                         |
| Slice (list[a:b])     | O(b-a)         | O(b-a)         | Depends on slice length         |

## Deque `collections.deque`

deque is represented internally as a doubly linked list, allowing for efficient appends and pops from both ends. However, it does not support random access like lists.

| Operation            | Average Case | Worst Case | Notes                                 |
| -------------------- | ------------ | ---------- | ------------------------------------- |
| Append (append)      | O(1)         | O(1)       | Efficient at both ends                |
| Pop (pop)            | O(1)         | O(1)       | Efficient at both ends                |
| Append/Pop (front)   | O(1)         | O(1)       | Efficient at both ends                |
| Index (deque[i])     | O(n)         | O(n)       | No direct indexing (linear traversal) |
| Membership (x in dq) | O(n)         | O(n)       | Linear search                         |

## Set `set`

set is implemented as a hash table, allowing for average O(1) time complexity for membership tests, insertions, and deletions. However, in the worst case, these operations can degrade to O(n) due to hash collisions.

| Operation                  | Average Case       | Worst Case         | Notes                                   |
| -------------------------- | ------------------ | ------------------ | --------------------------------------- |
| Membership (x in s)        | O(1)               | O(n)               | Rarely O(n) with hash collisions        |
| Insert/Delete (add/remove) | O(1)               | O(n)               | Rarely O(n) with hash collisions        |
| Union/Intersection         | O(len(s1)+len(s2)) | O(len(s1)*len(s2)) | Intersection worst-case depends on hash |
| Iteration (for x in s)     | O(n)               | O(n)               | Iterates through all elements           |

## Dictionary `dict`

| Operation                | Average Case | Worst Case | Notes                            |
| ------------------------ | ------------ | ---------- | -------------------------------- |
| Lookup (d[key])          | O(1)         | O(n)       | Rarely O(n) with hash collisions |
| Insert/Delete            | O(1)         | O(n)       | Rarely O(n) with hash collisions |
| Membership (key in d)    | O(1)         | O(n)       | Rarely O(n) with hash collisions |
| Iteration (for key in d) | O(n)         | O(n)       | Iterates through all keys        |

## sortedcontainers module

| Operation               | Average Case | Worst Case | Notes                                |
| ----------------------- | ------------ | ---------- | ------------------------------------ |
| Insert (add)            | O(log n)     | O(log n)   | e.g., SortedList, SortedDict         |
| Delete                  | O(log n)     | O(log n)   | Balanced binary-tree implementations |
| Membership              | O(log n)     | O(log n)   | Efficient sorted structures          |
| Indexing (container[i]) | O(log n)     | O(log n)   | Efficient indexing                   |
| Iteration (for x in c)  | O(n)         | O(n)       | Iterates through all elements        |

## Heap (PriorityQueue) (heapq)


| Operation         | Average Case | Worst Case | Notes                              |
| ----------------- | ------------ | ---------- | ---------------------------------- |
| Push (heappush)   | O(log n)     | O(log n)   | Maintains heap invariant           |
| Pop (heappop)     | O(log n)     | O(log n)   | Retrieves/removes smallest element |
| Peek (heap[0])    | O(1)         | O(1)       | Retrieves smallest without removal |
| Heapify (heapify) | O(n)         | O(n)       | Linear-time heap initialization    |

## Tuple `tuple`

| Operation               | Average Case | Worst Case | Notes                   |
| ----------------------- | ------------ | ---------- | ----------------------- |
| Indexing (tuple[i])     | O(1)         | O(1)       | Immutable; direct index |
| Membership (x in t)     | O(n)         | O(n)       | Linear search           |
| Concatenation (t1 + t2) | O(n+m)       | O(n+m)     | Creates a new tuple     |

## Common Pitfalls to Keep in Mind:

- List Insert/Delete: O(n) time if inserting/removing elements at front or middle (shifting required).
- Dict/Set worst-case: O(n) lookup due to hash collisions (rare but possible).
- Deque indexing: Not efficient (O(n)), use lists if random access is frequent.
- Sorted Containers: Use external libraries (sortedcontainers) for efficient sorted insertions/deletions/indexing (standard Python does not provide balanced binary search trees).
