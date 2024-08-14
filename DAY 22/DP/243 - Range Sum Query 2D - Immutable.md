# [304. Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/description/)

The problem you're facing requires handling multiple queries to calculate the sum of elements inside a rectangle in a 2D matrix efficiently. Given the constraints, we need an approach that allows `sumRegion` queries to be computed in O(1) time.

### Approach:
To achieve O(1) query time for `sumRegion`, we can use a **2D prefix sum** technique. The idea is to precompute the sum of all elements in the matrix up to each point `(i, j)`, which allows us to quickly compute the sum of any submatrix using inclusion-exclusion.

### Steps:

1. **Precompute a 2D prefix sum array**:
   - Create a 2D array `prefixSum` where `prefixSum[i][j]` stores the sum of all elements in the rectangle from `(0,0)` to `(i,j)` in the matrix.
   - For any submatrix, the sum can be computed using the formula:
     ```
     sumRegion(row1, col1, row2, col2) = prefixSum[row2][col2]
                                        - prefixSum[row1-1][col2] (if row1 > 0)
                                        - prefixSum[row2][col1-1] (if col1 > 0)
                                        + prefixSum[row1-1][col1-1] (if both row1 > 0 and col1 > 0)
     ```
     This formula uses inclusion-exclusion to avoid double-counting.

2. **Calculate the prefixSum array**:
   - For each cell `(i, j)`, the prefix sum is computed as:
     ```
     prefixSum[i][j] = matrix[i][j]
                     + prefixSum[i-1][j] (if i > 0)
                     + prefixSum[i][j-1] (if j > 0)
                     - prefixSum[i-1][j-1] (if both i > 0 and j > 0)
     ```

3. **sumRegion Calculation**:
   - Once the `prefixSum` array is computed, each `sumRegion` query can be answered in O(1) time using the inclusion-exclusion formula mentioned earlier.

### Code Implementation:

```python
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        # Edge case: if the matrix is empty
        if not matrix or not matrix[0]:
            return
        
        m, n = len(matrix), len(matrix[0])
        # Initialize prefixSum array with an extra row and column (to handle edge cases easily)
        self.prefixSum = [[0] * (n + 1) for _ in range(m + 1)]
        
        # Build the prefix sum array
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                self.prefixSum[i][j] = (matrix[i-1][j-1]
                                        + self.prefixSum[i-1][j]
                                        + self.prefixSum[i][j-1]
                                        - self.prefixSum[i-1][j-1])

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        # Use the precomputed prefix sums to calculate the sum in constant time
        return (self.prefixSum[row2 + 1][col2 + 1]
                - self.prefixSum[row1][col2 + 1]
                - self.prefixSum[row2 + 1][col1]
                + self.prefixSum[row1][col1])

# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```

### Explanation:

1. **Prefix Sum Construction**:
   - We initialize a `prefixSum` array of size `(m+1) x (n+1)` to handle boundary conditions easily.
   - For each element `(i, j)` in the `matrix`, we compute `prefixSum[i+1][j+1]` by adding the current matrix element and the appropriate values from the `prefixSum` array to avoid double-counting (following the formula).

2. **sumRegion Method**:
   - This method retrieves the sum of the submatrix using the inclusion-exclusion principle from the `prefixSum` array. This allows for O(1) query time.

### Example Walkthrough:

Let’s take the example matrix:

```
matrix = [
    [3, 0, 1, 4, 2],
    [5, 6, 3, 2, 1],
    [1, 2, 0, 1, 5],
    [4, 1, 0, 1, 7],
    [1, 0, 3, 0, 5]
]
```

After constructing the `prefixSum` array, it looks like this:

```
prefixSum = [
    [0, 0,  0,  0,  0,  0],
    [0, 3,  3,  4,  8,  10],
    [0, 8, 14, 18, 24, 27],
    [0, 9, 17, 21, 28, 36],
    [0, 13, 22, 26, 34, 49],
    [0, 14, 23, 30, 38, 58],
    [0, 15, 24, 33, 41, 63]
]
```

Now let's look at the queries:

1. **sumRegion(2, 1, 4, 3)**:
   - Using the formula:
     ```
     sum = prefixSum[5][4] - prefixSum[2][4] - prefixSum[5][1] + prefixSum[2][1]
     sum = 38 - 24 - 14 + 8 = 8
     ```
   - Output: `8`

2. **sumRegion(1, 1, 2, 2)**:
   - Using the formula:
     ```
     sum = prefixSum[3][3] - prefixSum[1][3] - prefixSum[3][1] + prefixSum[1][1]
     sum = 21 - 4 - 9 + 3 = 11
     ```
   - Output: `11`

3. **sumRegion(1, 2, 2, 4)**:
   - Using the formula:
     ```
     sum = prefixSum[3][5] - prefixSum[1][5] - prefixSum[3][2] + prefixSum[1][2]
     sum = 36 - 10 - 17 + 3 = 12
     ```
   - Output: `12`

### Time and Space Complexity:

- **Time Complexity**:
  - **Constructor**: O(m * n), where `m` is the number of rows and `n` is the number of columns in the matrix. This is because we compute the prefix sum for every element.
  - **sumRegion**: O(1) for each query, since we are only accessing a constant number of elements in the `prefixSum` array.

- **Space Complexity**: O(m * n) due to the storage of the `prefixSum` array.

This solution efficiently handles up to `10^4` calls in constant time after an initial preprocessing step.
