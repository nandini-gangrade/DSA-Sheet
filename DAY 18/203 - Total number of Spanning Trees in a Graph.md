# [Total number of Spanning Trees in a Graph](https://www.geeksforgeeks.org/total-number-spanning-trees-graph/)

To determine the total number of spanning trees in a graph that is not necessarily complete, we use Kirchhoff’s Theorem, which involves the Laplacian matrix of the graph. Here’s a step-by-step guide on how to use Kirchhoff's Theorem to compute the number of spanning trees:

### Kirchhoff’s Theorem (Matrix-Tree Theorem)

1. **Create the Adjacency Matrix**:
   - For a given graph with `n` vertices, create the adjacency matrix `A` where `A[i][j]` represents the edge between vertex `i` and vertex `j`. If there is an edge, `A[i][j] = 1`, otherwise `A[i][j] = 0`.

2. **Construct the Degree Matrix**:
   - The degree matrix `D` is a diagonal matrix where `D[i][i]` is the degree of vertex `i` (i.e., the number of edges connected to vertex `i`).

3. **Compute the Laplacian Matrix**:
   - The Laplacian matrix `L` is given by `L = D - A`. This matrix has the property that:
     - `L[i][i]` (diagonal elements) are the degrees of the vertices.
     - `L[i][j]` (off-diagonal elements) are `-1` if there is an edge between vertex `i` and vertex `j`, otherwise `0`.

4. **Form the Reduced Laplacian Matrix**:
   - To find the number of spanning trees, create a reduced Laplacian matrix by removing any one row and the corresponding column from the Laplacian matrix `L`. The remaining matrix is called the cofactor matrix.

5. **Calculate the Determinant**:
   - Compute the determinant of this cofactor matrix. The determinant of the reduced Laplacian matrix gives the total number of spanning trees in the graph.

### Example

Consider the following graph with 4 vertices and edges:

```
1 -- 2
|    |
3 -- 4
```

The adjacency matrix `A` and the degree matrix `D` are:

```
Adjacency Matrix (A):
0 1 1 0
1 0 0 1
1 0 0 1
0 1 1 0

Degree Matrix (D):
2 0 0 0
0 2 0 0
0 0 2 0
0 0 0 2
```

**Step-by-Step Calculation**:

1. **Laplacian Matrix (L)**:

   ```
   L = D - A
   L:
   2 -1 -1  0
   -1  2  0 -1
   -1  0  2 -1
    0 -1 -1  2
   ```

2. **Reduced Laplacian Matrix**:
   - Remove the first row and first column (we can choose any row and column to remove, but typically the first is chosen):

   ```
   Reduced Laplacian Matrix:
   2  0 -1
   0  2 -1
   -1 -1  2
   ```

3. **Determinant Calculation**:
   - Compute the determinant of the remaining matrix:

   ```
   Determinant of:
   2  0 -1
   0  2 -1
   -1 -1  2
   ```

   Using a method like cofactor expansion or a computational tool, the determinant is `4`.

So, the number of spanning trees for this graph is `4`.

### Python Implementation

Here’s a Python implementation to calculate the number of spanning trees using Kirchhoff’s Theorem:

```python
import numpy as np

def number_of_spanning_trees(graph):
    n = len(graph)
    # Create the Laplacian matrix
    L = np.zeros((n, n))
    for i in range(n):
        L[i][i] = sum(graph[i])
        for j in range(n):
            if graph[i][j]:
                L[i][j] = -1
    
    # Remove the first row and the first column to get the reduced Laplacian
    L_reduced = np.delete(L, 0, axis=0)
    L_reduced = np.delete(L_reduced, 0, axis=1)
    
    # Calculate the determinant
    return int(round(np.linalg.det(L_reduced)))

# Example usage
graph = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
]

print(number_of_spanning_trees(graph))  # Output: 4
```

### Summary
- Construct the Laplacian matrix `L` of the graph.
- Form the reduced Laplacian matrix by removing one row and column.
- Compute the determinant of the reduced Laplacian matrix to get the number of spanning trees.

This approach efficiently computes the number of spanning trees in a graph, leveraging matrix operations and linear algebra.
