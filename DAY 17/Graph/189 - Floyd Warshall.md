# [Floyd Warshall](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1)

To solve the problem of finding the shortest distances between every pair of vertices in a given edge-weighted directed graph using the Floyd-Warshall algorithm, we need to update the adjacency matrix in-place to reflect the shortest paths. The Floyd-Warshall algorithm is suitable for this problem because it computes shortest paths between all pairs of vertices efficiently with a time complexity of \(O(n^3)\), which is acceptable for the given constraint (up to 100 vertices).

### Floyd-Warshall Algorithm Overview

The Floyd-Warshall algorithm works by iteratively updating the shortest paths between all pairs of vertices. For each intermediate vertex \(k\), it updates the shortest path between all pairs of vertices \((i, j)\) by checking if a path through \(k\) offers a shorter path than the currently known shortest path.

### Key Points

1. **Initialization**:
   - The matrix is initialized such that if `matrix[i][j]` is -1, it indicates no direct edge between vertex \(i\) and vertex \(j\). These entries will be treated as infinite distance initially, except for the diagonal entries where `matrix[i][i]` should be 0.

2. **Algorithm**:
   - Iterate over all vertices as intermediate points.
   - For each pair of vertices \((i, j)\), check if a path through the intermediate vertex \(k\) provides a shorter path than the currently known shortest path.

3. **Edge Cases**:
   - Direct distances where no path exists should be kept as -1 if they remain unreachable after processing.

Here's how you can implement the Floyd-Warshall algorithm in C++:

```cpp
#include <vector>
#include <algorithm>

void shortest_distance(std::vector<std::vector<int>>& matrix) {
    int n = matrix.size();
    
    // Floyd-Warshall algorithm
    for (int k = 0; k < n; ++k) {
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                // Skip if no path exists from i to k or from k to j
                if (matrix[i][k] != -1 && matrix[k][j] != -1) {
                    if (matrix[i][j] == -1 || matrix[i][k] + matrix[k][j] < matrix[i][j]) {
                        matrix[i][j] = matrix[i][k] + matrix[k][j];
                    }
                }
            }
        }
    }
}
```

### Explanation

1. **Initialization**:
   - The input matrix is directly used to store the shortest paths.

2. **Three Nested Loops**:
   - **Outer Loop**: Iterates over all possible intermediate vertices \(k\).
   - **Middle Loop**: Iterates over all possible starting vertices \(i\).
   - **Inner Loop**: Iterates over all possible ending vertices \(j\).
   - Updates the shortest path from \(i\) to \(j\) if a shorter path through \(k\) is found.

3. **Checking for Shorter Paths**:
   - If both `matrix[i][k]` and `matrix[k][j]` are not -1 (indicating there is a path), it checks if the path through \(k\) is shorter than the currently known path from \(i\) to \(j\).

### Complexity

- **Time Complexity**: \(O(n^3)\), where \(n\) is the number of vertices. This is due to the three nested loops iterating over all vertex pairs and intermediate vertices.
- **Space Complexity**: \(O(1)\) extra space since the algorithm modifies the input matrix in-place.

This approach ensures that the matrix will correctly reflect the shortest distances between all pairs of vertices after the algorithm completes.
