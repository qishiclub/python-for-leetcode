# Time Complexity Estimation for LeetCode Problems

| Complexity Upper Bound | Possible Algorithms                          | Typical Constraints (LeetCode) |
| ---------------------- | -------------------------------------------- | ------------------------------ |
| $O(n \cdot 2^n)$       | Brute-force DFS, Bitmask                     | $n \leq 20$                    |
| $O(n^3)$               | Brute-force, Floyd-Warshall, 3-D DP          | $n \leq 300$                   |
| $O(n^2)$               | 2-D DP, BFS, DFS                             | $n \leq 1000$                  |
| $O(n \log n)$          | Sort, Binary Search, Dijkstra                | $n \leq 10^5$                  |
| $O(n)$                 | Hashing, Prefix Sum, Union-Find, Two-Pointer | $n \leq 10^6$                  |
| $O(\log n)$            | Binary Search                                | $n \leq 10^{18}$               |

## Explanation

- **$O(n \cdot 2^n)$**: Usually involves exploring all subsets or permutations. Commonly solved using bitmasking or DFS with pruning. Limited to very small inputs due to exponential growth.

- **$O(n^3)$**: Often used in problems involving Floyd-Warshall for all-pairs shortest paths or DP problems with three-dimensional state arrays.

- **$O(n^2)$**: Suitable for typical matrix problems, DP with 2-D state arrays, or traversals involving nested loops. BFS or DFS with adjacency matrices or grids often fall under this complexity.

- **$O(n \log n)$**: Algorithms requiring sorting (Merge sort, Quick sort), binary search, or priority queue-based algorithms like Dijkstra fall here.

- **$O(n)$**: Optimal complexity involving linear traversals, hashing to achieve constant-time lookups, two-pointers, prefix sums for cumulative calculations, or union-find for disjoint set problems.

- **$O(\log n)$**: Represents highly efficient search-based algorithms, mainly binary search on large sorted or implicitly sorted datasets.
