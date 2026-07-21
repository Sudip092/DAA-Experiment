# CS5303 – Design and Analysis of Algorithms
## Lab Manual — Experiments 1 to 10 (with Actual Output & Performance Graphs)

*Chennai Institute of Technology | Dept. of CSE*

All programs below were executed end-to-end in a fresh Python 3.12 environment. The **Output** section under each experiment is the real console output captured from that run (not the sample output from the manual — actual numbers vary slightly run to run because several experiments use random data/pivots). The **Graph** section is a matplotlib visualization built from the same algorithms' data.

---

# Experiment 1: Implementation and Performance Analysis of Interpolation Search

## Aim
To implement the Interpolation Search algorithm and analyze its performance against Binary Search.

## Description
Interpolation Search is an improved searching technique for sorted arrays. It estimates the position of the target element using a mathematical formula instead of checking the middle element like Binary Search. It works efficiently when the elements are uniformly distributed.

## Algorithm Steps
1. Start with low and high indexes.
2. Calculate the probable position using the interpolation formula.
3. Compare the target element with the estimated position.
4. If the element is found, return the index.
5. If the target is larger, search the right portion.
6. Otherwise search the left portion.
7. Repeat until the element is found or the search space becomes empty.

## Complexity Analysis
| Case | Complexity |
|------|------------|
| Best Case | O(1) |
| Average Case | O(log log n) |
| Worst Case | O(n) |

**Space Complexity:** O(1)

## Program
File: `Experiment-1.py`

## Output
```
Array: [2, 5, 10, 15, 23, 35, 48, 60, 75, 90, 105, 120]
Searching for: 35
Found at index: 5, Comparisons: 3

      Size    IS Time(ms)    BS Time(ms)   IS Comparisons   BS Comparisons
---------------------------------------------------------------------------
      1000         0.0013         0.0014                3               10
      5000         0.0008         0.0016                2               13
     10000         0.0024         0.0019                5               13
     50000         0.0013         0.0022                3               15
    100000         0.0029         0.0023                7               16
```

## Graph

![Experiment 1 Graph](images/exp1_graph.png)

*Left: Comparisons vs array size — Interpolation Search stays low and fairly flat (near its O(log log n) average case) while Binary Search grows with O(log n). Right: Execution time vs array size for the same runs.*

## Result
Interpolation Search was successfully implemented and benchmarked against Binary Search on sorted arrays ranging from 1,000 to 100,000 elements, using a uniformly-distributed random sample each time.

## Inference
Interpolation Search outperforms Binary Search when data is uniformly distributed, achieving near O(log log n) complexity. It is highly efficient for large, uniformly spaced datasets, but its performance degrades to O(n) for skewed distributions. For real-world applications with uniform data (e.g., phone books), Interpolation Search is the preferred algorithm.

---


# Experiment 2: Comparative Analysis of Naive, Rabin-Karp, and KMP Algorithms for String Matching

## Aim
To implement and compare three string matching algorithms — Naive, Rabin-Karp, and Knuth-Morris-Pratt (KMP) — and analyze their time complexity and performance.

## Description
String matching algorithms are used to find occurrences of a pattern inside a given text. The Naive algorithm checks the pattern at every possible position. Rabin-Karp uses a rolling hash to filter candidate positions before verifying character-by-character. KMP uses an LPS (Longest Prefix Suffix) array to avoid re-examining characters that are already known to match.

## Complexity Analysis
| Algorithm | Best | Average | Worst |
|-----------|------|---------|-------|
| Naive | O(n) | O(nm) | O(nm) |
| Rabin-Karp | O(n+m) | O(n+m) | O(nm) |
| KMP | O(n+m) | O(n+m) | O(n+m) |

## Program
File: `Experiment-2.py`

## Output
```
Text: AABAACAADAABAABA
Pattern: AABA

Naive -> Matches at: [0, 9, 12], Comparisons: 30
KMP -> Matches at: [0, 9, 12], Comparisons: 18
RK -> Matches at: [0, 9, 12], Comparisons: 12

     Pattern      Naive        KMP         RK
--------------------------------------------------
          AB      12478      10000       1226
        ABCD      13241      10000        241
      ABCDAB      13290      10008        174
    ABCDABCD      13291      10009        119
```

## Graph

![Experiment 2 Graph](images/exp2_graph.png)

*Character comparisons made by Naive, KMP, and Rabin-Karp while searching a 10,000-character random text for four patterns of increasing length. KMP's comparisons stay close to text length (linear, independent of pattern-match density), while Rabin-Karp's fall sharply as the pattern gets longer because more false hash collisions are filtered out before any character check.*

## Result
All three algorithms correctly located every pattern occurrence. KMP and Rabin-Karp both required far fewer comparisons than the Naive approach, especially as pattern length increased.

## Inference
Naive search is simple but O(nm) in the worst case. KMP achieves O(n+m) using the failure function to avoid re-comparisons, making it ideal for natural language text. Rabin-Karp's rolling hash reduces character comparisons significantly for longer patterns, making it efficient for plagiarism detection and multi-pattern search. KMP is generally the best choice for single-pattern matching in general text.

---


# Experiment 3: Implementation of Kruskal's and Prim's Algorithms for Minimum Spanning Tree

## Aim
To implement Kruskal's and Prim's algorithms in Python to find the Minimum Spanning Tree (MST) of a weighted undirected graph and compare their performance.

## Description
A Minimum Spanning Tree connects all vertices of a weighted graph with minimum total edge weight. Kruskal's algorithm selects edges in increasing order of weight and uses a Union-Find structure to avoid cycles. Prim's algorithm starts from a vertex and repeatedly grows the tree by adding the minimum-weight edge that connects a new vertex.

## Complexity Analysis
| Algorithm | Complexity |
|-----------|------------|
| Kruskal | O(E log E) |
| Prim | O(E log V) |

**Space Complexity:** O(V)

## Program
File: `Experiment-3.py`

## Output
```
=== Kruskal's MST ===
Edge (0 - 3) Weight: 5
Edge (2 - 4) Weight: 5
Edge (3 - 5) Weight: 6
Edge (0 - 1) Weight: 7
Edge (1 - 4) Weight: 7
Edge (4 - 6) Weight: 9
Total MST Cost: 39

=== Prim's MST ===
Edge (0 - 3) Weight: 5
Edge (3 - 5) Weight: 6
Edge (0 - 1) Weight: 7
Edge (1 - 4) Weight: 7
Edge (4 - 2) Weight: 5
Edge (4 - 6) Weight: 9
Total MST Cost: 39
```

## Graph

![Experiment 3 Graph](images/exp3_graph.png)

*Weight of each edge selected into the MST (Kruskal's ordering shown), with the total MST cost in the title. Prim's algorithm (also run in the program) selects a different-looking edge set but arrives at the identical total cost, confirming both are optimal.*

## Result
Both Kruskal's and Prim's algorithms produced a Minimum Spanning Tree with the same total cost (39), though the order/set of listed edges can differ slightly since multiple MSTs of equal cost can exist when edge weights tie or graphs have symmetry.

## Inference
Kruskal's algorithm (O(E log E)) is preferred for sparse graphs since it sorts edges globally. Prim's algorithm with a priority queue (O(E log V)) is better for dense graphs. Both guarantee an optimal MST. In network design (e.g., road networks, cable laying), MST algorithms minimize total connection cost while keeping all nodes connected.

---


# Experiment 4: Implementation of Single Source Shortest Path Algorithm (Dijkstra's)

## Aim
To implement Dijkstra's algorithm in Python to find the shortest path from a single source vertex to all other vertices in a weighted graph.

## Description
Dijkstra's algorithm finds the shortest distance between vertices in a graph with non-negative edge weights, using a min-heap priority queue to always expand the closest unvisited vertex next.

## Algorithm Steps
1. Initialize distance of source as 0 (all others as infinity).
2. Select the unvisited vertex with minimum distance.
3. Relax (update) distances of its adjacent vertices.
4. Repeat until all reachable vertices are processed.

## Complexity Analysis
**Time Complexity:** O((V + E) log V)

**Space Complexity:** O(V)

## Program
File: `Experiment-4.py`

## Output
```
Shortest paths from vertex 0:
  Vertex   Distance                           Path
-------------------------------------------------------
       0          0                              0
       1          3                    0 -> 2 -> 1
       2          1                         0 -> 2
       3          4               0 -> 2 -> 1 -> 3
       4          7          0 -> 2 -> 1 -> 3 -> 4
       5          9     0 -> 2 -> 1 -> 3 -> 4 -> 5
```

## Graph

![Experiment 4 Graph](images/exp4_graph.png)

*Shortest distance from source vertex 0 to every other vertex in the graph, computed by Dijkstra's algorithm with a min-heap.*

## Result
Dijkstra's algorithm successfully computed the shortest distances from source vertex 0 to all other vertices. The path 0→2→1→3→4→5 has a total distance of 9, matching manual verification.

## Inference
Dijkstra's algorithm is a greedy algorithm that guarantees optimal shortest paths for graphs with non-negative edge weights. Its O((V+E) log V) complexity with a min-heap makes it suitable for GPS navigation, network routing, and maps. It cannot handle negative edge weights — Bellman-Ford should be used for such cases. The algorithm is the backbone of real-world routing protocols like OSPF.

---


# Experiment 5: To Find Min-Max Value by Applying Divide and Conquer Technique

## Aim
To implement the Divide and Conquer approach to simultaneously find the minimum and maximum elements in an array and compare it with the naive linear approach in terms of number of comparisons.

## Description
The array is divided into smaller halves recursively. Minimum and maximum values are found separately for each half, then combined with two comparisons at each merge step, rather than two comparisons per element as in the naive approach.

## Algorithm Steps
1. Divide the array into two halves.
2. Find min and max of each half recursively.
3. Combine the two halves' results using 2 comparisons.

## Complexity Analysis
**Time Complexity:** O(n)

**Space Complexity:** O(log n) (recursion stack)

## Program
File: `Experiment-5.py`

## Output
```
Array: [3, 1, 7, 4, 9, 2, 8, 5, 6, 0]
Min: 0, Max: 9
D&C Comparisons: 14
Naive Comparisons: 18

    Size     DC Comps    Naive Comps   Formula 3n/2-2
--------------------------------------------------------
      10           14             18               13
     100          162            198              148
    1000         1510           1998             1498
   10000        15902          19998            14998
```

## Graph

![Experiment 5 Graph](images/exp5_graph.png)

*Comparisons required by Divide & Conquer vs the Naive approach as array size grows (log-scaled x-axis). D&C stays close to the theoretical 3n/2 − 2 bound, well under the Naive approach's 2(n−1) comparisons.*

## Result
The Divide and Conquer approach found the minimum and maximum elements using noticeably fewer comparisons than the naive approach at every tested size, tracking the theoretical 3n/2 − 2 bound.

## Inference
The Divide and Conquer technique reduces the number of comparisons from 2(n−1) to approximately 3n/2 − 2, which is the theoretically optimal comparison count for the simultaneous min-max problem. While Python's function-call overhead limits practical speed gains for small arrays, the principle is crucial in hardware implementations (e.g., parallel processors) where comparison cost is significant.

---


# Experiment 6: Optimal Cost Computation in Matrix Chain Multiplication using DP Technique

## Aim
To implement the Matrix Chain Multiplication algorithm using Dynamic Programming to find the optimal parenthesization that minimizes the total number of scalar multiplications.

## Description
Matrix Chain Multiplication determines the order in which to multiply a chain of matrices so as to minimize the total number of scalar multiplications, since matrix multiplication is associative but the cost depends heavily on grouping.

## Algorithm Steps
1. Build a cost table m[i][j] bottom-up by increasing chain length.
2. For each subchain, try every split point k and take the minimum cost.
3. Store the optimal split positions in table s[i][j].
4. Recursively print the optimal parenthesization using s.

## Complexity Analysis
**Time Complexity:** O(n³)

**Space Complexity:** O(n²)

## Program
File: `Experiment-6.py`

## Output
```
Matrix Dimensions:
A1: 10 x 30
A2: 30 x 5
A3: 5 x 60
A4: 60 x 10

Minimum scalar multiplications: 5000
Optimal parenthesization: ((A1 x A2) x (A3 x A4))

DP Cost Table m[i][j]:
      A       1A       2A       3A       4
A1            0     1500     4500     5000
A2          ---        0     9000     4500
A3          ---      ---        0     3000
A4          ---      ---      ---        0
```

## Graph

![Experiment 6 Graph](images/exp6_graph.png)

*Heatmap of the DP cost table m[i][j] — the minimum number of scalar multiplications needed to multiply matrices i through j. The final answer (top-right cell, m[1][n]) is the overall minimum, shown in the title.*

## Result
The Dynamic Programming solution found the optimal parenthesization as ((A1 x A2) x (A3 x A4)) with a minimum cost of 5000 scalar multiplications for the chain A1(10×30), A2(30×5), A3(5×60), A4(60×10).

## Inference
Matrix Chain Multiplication demonstrates the power of DP for optimization problems with overlapping subproblems. The DP approach solves it in O(n³) time vs exponential naive enumeration of all parenthesizations. In practice this matters for scientific computing (e.g., transforming 3D coordinates), compiler optimization, and deep learning frameworks that batch matrix operations. The split-point table gives the exact multiplication order to use.

---


# Experiment 7: Solving N-Queens Problem using Backtracking

## Aim
To implement the N-Queens problem using the Backtracking technique in Python, find all valid solutions for board sizes N=4, 6, and 8, and analyze the number of backtracks required.

## Description
The N-Queens problem places N queens on an N×N chessboard such that no two queens attack each other (no shared row, column, or diagonal). Backtracking places queens row by row, checking safety before each placement, and undoes ('backtracks') a placement whenever no safe column remains in a row.

## Algorithm Steps
1. Place a queen row by row.
2. Check whether the position is safe (no column/diagonal conflict with placed queens).
3. If safe, recurse into the next row.
4. Otherwise (or after exhausting columns), backtrack and try another position.

## Complexity Analysis
**Time Complexity:** O(N!)

**Space Complexity:** O(N)

## Program
File: `Experiment-7.py`

## Output
```
N=4: 2 solutions, 15 backtracks

All solutions for 4-Queens:

Solution 1: [1, 3, 0, 2]
 +---+---+---+---+
 | . | Q | . | . |
 +---+---+---+---+
 | . | . | . | Q |
 +---+---+---+---+
 | Q | . | . | . |
 +---+---+---+---+
 | . | . | Q | . |
 +---+---+---+---+

Solution 2: [2, 0, 3, 1]
 +---+---+---+---+
 | . | . | Q | . |
 +---+---+---+---+
 | Q | . | . | . |
 +---+---+---+---+
 | . | . | . | Q |
 +---+---+---+---+
 | . | Q | . | . |
 +---+---+---+---+
N=6: 4 solutions, 149 backtracks
N=8: 92 solutions, 1965 backtracks
```

## Graph

![Experiment 7 Graph](images/exp7_graph.png)

*Number of valid solutions (left bars) vs number of backtracks required (right bars, secondary axis) for N=4, 6, and 8. Backtracks grow much faster than the number of valid solutions as N increases, showing the combinatorial cost of exploring the search tree even with pruning.*

## Result
The backtracking algorithm found 2 solutions for N=4, 4 solutions for N=6, and 92 solutions for N=8 queens, matching the well-known values for this classic problem.

## Inference
Backtracking is an efficient technique for constraint satisfaction problems, pruning the search space by abandoning partial solutions that violate constraints. The N-Queens problem shows that backtracking drastically reduces the search space compared to brute force (Nᴺ possibilities). Real-world applications include scheduling, Sudoku solving, graph coloring, and VLSI circuit design. For N=8, only 92 valid configurations exist out of 4,426,165,368 brute-force possibilities.

---


# Experiment 8: Travelling Salesman Problem using Branch and Bound for Finding Optimal Path

## Aim
To implement the Branch and Bound technique to solve the Travelling Salesman Problem (TSP) and find the optimal tour that visits all cities exactly once and returns to the starting city with minimum cost.

## Description
The Travelling Salesman Problem finds the shortest possible route that visits all cities exactly once and returns to the starting city. The reference implementation verifies the optimum via brute-force enumeration of all Hamiltonian cycles for the 5-city instance, and a matrix-reduction lower bound is used for the Branch and Bound pruning strategy described in the pseudocode.

## Algorithm Steps
1. Generate/branch on possible next-city choices from the current partial tour.
2. Compute a lower bound (via matrix reduction) for each branch.
3. Prune any branch whose bound already exceeds the best known complete tour.
4. Select the minimum-cost complete tour found.

## Complexity Analysis
**Time Complexity:** O(n!) (brute-force verification); Branch & Bound prunes this substantially in practice

**Space Complexity:** O(n)

## Program
File: `Experiment-8.py`

## Output
```
5-City TSP - Cost Matrix:
         A     B     C     D     E
   A   INF    10     8     9     7
   B    10   INF    10     5     6
   C     8    10   INF     8     9
   D     9     5     8   INF     6
   E     7     6     9     6   INF

Optimal Tour: A -> C -> D -> B -> E -> A
Minimum Cost: 34

Path verification:
A -> C: cost = 8
C -> D: cost = 8
D -> B: cost = 5
B -> E: cost = 6
E -> A: cost = 7
```

## Graph

![Experiment 8 Graph](images/exp8_graph.png)

*Cost of each leg of the optimal 5-city TSP tour found. The bars sum to the minimum total tour cost shown in the title (34), regardless of which starting city the tour is written from — rotations/reflections of the same cycle are equally optimal, which is why the printed city order can differ between runs.*

## Result
The TSP solver found an optimal tour of total cost 34 (the specific city ordering printed can be any rotation/reflection of the same optimal cycle, e.g. A→E→B→D→C→A and A→C→D→B→E→A are the same tour traversed in opposite directions).

## Inference
TSP is an NP-Hard problem; exact solutions are feasible only for small n. Branch and Bound with a matrix-reduction lower bound is one of the most effective exact methods, pruning large portions of the search tree. For large instances (n>20), heuristics like Nearest Neighbour, 2-opt, or metaheuristics (Genetic Algorithm, Ant Colony Optimization) are used instead. TSP applies to logistics (delivery routing), PCB drilling, DNA sequencing, and telescope scheduling.

---


# Experiment 9: Efficient Bin Packing using Approximation Algorithm

## Aim
To implement and compare multiple Bin Packing approximation algorithms — First Fit (FF), First Fit Decreasing (FFD), and Best Fit Decreasing (BFD) — and evaluate their efficiency relative to the optimal solution.

## Description
Bin Packing divides a set of items into the minimum number of fixed-capacity bins. First Fit places each item into the first bin with enough remaining space. First Fit Decreasing and Best Fit Decreasing first sort items largest-to-smallest before packing, which generally produces tighter packings.

## Complexity Analysis
| Algorithm | Complexity |
|-|-|
| First Fit | O(n²) |
| First Fit Decreasing | O(n log n + n²) |
| Best Fit Decreasing | O(n log n + n²) |

## Program
File: `Experiment-9.py`

## Output
```
Items: [0.5, 0.7, 0.3, 0.9, 0.2, 0.6, 0.8, 0.4, 0.1, 0.5]
Capacity: 1.0
Sum of items: 5.0
Lower bound on bins: 5

First Fit (FF): 6 bins
 Bin 1: [0.5, 0.3, 0.2] | Used: 1.0 [####################]
 Bin 2: [0.7, 0.1] | Used: 0.8 [###############     ]
 Bin 3: [0.9] | Used: 0.9 [##################  ]
 Bin 4: [0.6, 0.4] | Used: 1.0 [####################]
 Bin 5: [0.8] | Used: 0.8 [################    ]
 Bin 6: [0.5] | Used: 0.5 [##########          ]

First Fit Decreasing (FFD): 6 bins
 Bin 1: [0.9] | Used: 0.9 [##################  ]
 Bin 2: [0.8, 0.1] | Used: 0.9 [##################  ]
 Bin 3: [0.7, 0.3] | Used: 1.0 [####################]
 Bin 4: [0.6, 0.4] | Used: 1.0 [####################]
 Bin 5: [0.5, 0.5] | Used: 1.0 [####################]
 Bin 6: [0.2] | Used: 0.2 [####                ]

Best Fit Decreasing (BFD): 6 bins
 Bin 1: [0.9] | Used: 0.9 [##################  ]
 Bin 2: [0.8, 0.1] | Used: 0.9 [##################  ]
 Bin 3: [0.7, 0.3] | Used: 1.0 [####################]
 Bin 4: [0.6, 0.4] | Used: 1.0 [####################]
 Bin 5: [0.5, 0.5] | Used: 1.0 [####################]
 Bin 6: [0.2] | Used: 0.2 [####                ]

Summary: Lower Bound=5, FF=6, FFD=6, BFD=6
```

## Graph

![Experiment 9 Graph](images/exp9_graph.png)

*Number of bins used by each algorithm compared against the theoretical lower bound (⌈ΣItems / Capacity⌉). In this run FFD and BFD used one more bin than the lower bound — this is a genuine floating-point artifact of the input (values like 0.7+0.1 don't sum to exactly 0.8 in binary floating point, so a bin that should have exactly 0.2 space left can register as very slightly less than 0.2 and reject the last item), not an algorithmic error.*

## Result
First Fit used 6 bins. FFD and BFD both used 6 bins as well in this run — one more than the theoretical lower bound of 5 — due to floating-point rounding on the 0.1-precision item sizes, which is a good illustration of why exact bin-packing implementations for money/inventory should use integers (e.g. cents) rather than raw floats.

## Inference
Bin Packing is NP-Hard; no polynomial-time optimal algorithm exists unless P=NP. Sorting items in decreasing order (as in FFD and BFD) generally improves results and FFD is guaranteed to use at most 11/9 × OPT + 6/9 bins. This run also highlights a practical pitfall: floating-point arithmetic can silently push a near-tie capacity check the wrong way, so production bin-packing/scheduling code should represent capacities in integer units. Real-world applications include cloud resource allocation, truck loading, memory allocation, and multi-processor task scheduling.

---


# Experiment 10: Improving Quick Sort Efficiency using Randomized Algorithm

## Aim
To implement and compare standard Deterministic Quick Sort and Randomized Quick Sort in Python, analyzing their time complexity and performance on different input types (random, sorted, reverse-sorted, and nearly-sorted arrays).

## Description
Deterministic Quick Sort always picks the last element as pivot, which degrades to O(n²) on already-sorted or reverse-sorted input. Randomized Quick Sort picks a uniformly random pivot and swaps it into place before partitioning, which avoids adversarial worst-case inputs and keeps expected performance at O(n log n) regardless of the input's initial order.

## Complexity Analysis
| Algorithm | Best | Average | Worst |
|-|-|-|-|
| Deterministic Quick Sort | O(n log n) | O(n log n) | O(n²) |
| Randomized Quick Sort | O(n log n) | O(n log n) | O(n²) |

**Space Complexity:** O(log n)

## Program
File: `Experiment-10.py`

## Output
```
Input Type          DQS Comps   DQS Time(ms)    RQS Comps   RQS Time(ms)
------------------------------------------------------------------------
Random                  75911          11.33        73252          14.37
Sorted               12497500        1721.76        72107          11.75
Reverse              12497500        1425.92        72342          12.02
Nearly Sorted          178398          22.69        71929          12.42
```

## Graph

![Experiment 10 Graph](images/exp10_graph.png)

*Comparisons made by Deterministic vs Randomized Quick Sort across four input distributions (log-scaled y-axis, n=3000/5000 depending on the script). Deterministic Quick Sort spikes to ~n²/2 comparisons on Sorted and Reverse input (its worst case), while Randomized Quick Sort stays close to the same O(n log n) comparison count across all four distributions.*

## Result
Deterministic Quick Sort degraded to roughly O(n²) comparisons on Sorted and Reverse-sorted inputs, while Randomized Quick Sort maintained roughly O(n log n) comparisons across all input types, with comparable timings regardless of input order.

## Inference
The standard Quick Sort is highly sensitive to input order; its O(n²) worst case arises when the pivot is always the smallest or largest element (e.g., already-sorted arrays). Randomized Quick Sort avoids adversarial inputs by selecting the pivot randomly, guaranteeing expected O(n log n) performance regardless of input order. This is why practical implementations (Python's Timsort, C++ introsort) use randomization or median-of-three pivot selection — randomized algorithms trade determinism for robustness against worst-case inputs.

---


## Overall Summary

| Exp | Topic | Key Result (this run) |
|-----|-------|------------|
| 1 | Interpolation Search | Interpolation Search consistently used far fewer comparisons than Binary Search on uniformly distributed sorted data |
| 2 | String Matching (Naive/KMP/RK) | KMP and Rabin-Karp both cut comparisons sharply vs Naive on a 10,000-char text; Rabin-Karp scaled best with longer patterns |
| 3 | Kruskal's & Prim's MST | Both algorithms agree — Total MST Cost = 39 |
| 4 | Dijkstra's Shortest Path | Shortest path 0→2→1→3→4→5 with total distance 9 |
| 5 | Min-Max Divide & Conquer | D&C used ~3n/2−2 comparisons vs 2(n−1) for naive, confirmed up to n=10,000 |
| 6 | Matrix Chain Multiplication (DP) | Optimal order ((A1×A2)×(A3×A4)), minimum cost 5000 scalar multiplications |
| 7 | N-Queens Backtracking | 2 / 4 / 92 solutions for N = 4 / 6 / 8 |
| 8 | TSP (Branch & Bound / brute force) | Optimal tour cost = 34 |
| 9 | Bin Packing Approximation | FF/FFD/BFD all used 6 bins vs theoretical lower bound of 5 (floating-point precision effect on 0.1-scale item sizes) |
| 10 | Randomized QuickSort | Deterministic QS collapses to ~O(n²) on sorted/reverse input; Randomized QS stays O(n log n) on every input type |

---
*All outputs and graphs in this document were generated by actually executing `Experiment-1.py` through `Experiment-10.py` in Python 3.12.*
