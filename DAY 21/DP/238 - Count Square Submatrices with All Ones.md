# [1277. Count Square Submatrices with All Ones](https://leetcode.com/problems/count-square-submatrices-with-all-ones/description/)

To solve the problem of counting the number of square submatrices that have all ones in a given `m * n` matrix, we can use a dynamic programming approach. Here's the detailed explanation and code:

### Approach:
1. **DP Table Definition**:
   - Define a 2D DP table where `dp[i][j]` represents the size of the largest square submatrix whose bottom-right corner is at `(i, j)`.

2. **State Transition**:
   - If the matrix value at `(i, j)` is `1`, then `dp[i][j]` will be the minimum of the values from the left cell (`dp[i][j-1]`), the top cell (`dp[i-1][j]`), and the top-left diagonal cell (`dp[i-1][j-1]`) plus one. This is because a square of size greater than `1x1` can only exist if all three of those squares are also valid.
   - If the matrix value at `(i, j)` is `0`, then `dp[i][j]` will be `0` as no square can end at that position.

3. **Counting Squares**:
   - The sum of all values in the DP table will give the total number of square submatrices that have all ones.

### Implementation:

```python
class Solution:
    def countSquares(self, matrix: List[List[int]]) -> int:
        if not matrix:
            return 0
        
        # Initialize the DP table with the same dimensions as matrix
        dp = [[0] * len(matrix[0]) for _ in range(len(matrix))]
        total_squares = 0
        
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == 1:
                    if i == 0 or j == 0:  # If it's on the first row or first column
                        dp[i][j] = 1
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                    total_squares += dp[i][j]
        
        return total_squares
```

### Explanation:

1. **Initialization**:
   - The DP table is initialized with the same dimensions as the input matrix, filled with zeros.

2. **DP Table Update**:
   - For each cell `(i, j)` in the matrix, if the matrix value is `1`, update `dp[i][j]` based on the minimum of the values from the neighboring cells (`top`, `left`, and `top-left diagonal`) plus one.

3. **Summing Up**:
   - Each entry in the DP table represents the size of the largest square ending at that position, so summing up all the values in the DP table gives the total number of square submatrices.

### Complexity Analysis:
- **Time Complexity**: O(m * n), where `m` is the number of rows and `n` is the number of columns in the matrix. We iterate through each cell in the matrix once.
- **Space Complexity**: O(m * n) for the DP table. This can be optimized to O(n) by using a single array instead of a 2D table if memory usage is a concern.

### Example Walkthrough:
For the matrix:
```
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
```
The DP table will look like:
```
[
  [0,1,1,1],
  [1,1,2,2],
  [0,1,2,3]
]
```
The sum of all entries in the DP table is `15`, which is the total number of square submatrices with all ones.

This solution efficiently counts the number of square submatrices in the given matrix that contain all ones using dynamic programming.
