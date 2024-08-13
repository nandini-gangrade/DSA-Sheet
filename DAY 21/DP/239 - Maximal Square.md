# [221. Maximal Square](https://leetcode.com/problems/maximal-square/description/)

To solve the problem of finding the largest square containing only `1`s in a given `m x n` binary matrix and returning its area, we can use a dynamic programming approach similar to the one used for counting square submatrices with all ones. Here's how we can approach it:

### Approach:
1. **DP Table Definition**:
   - Define a 2D DP table where `dp[i][j]` represents the side length of the largest square whose bottom-right corner is at `(i, j)`.

2. **State Transition**:
   - If `matrix[i][j]` is `'1'`, then `dp[i][j]` will be the minimum of the values from the left cell (`dp[i][j-1]`), the top cell (`dp[i-1][j]`), and the top-left diagonal cell (`dp[i-1][j-1]`) plus one. This is because a square of side greater than `1` can only exist if all three of those squares are also valid.
   - If `matrix[i][j]` is `'0'`, then `dp[i][j]` will be `0` as no square can end at that position.

3. **Tracking the Maximum Square**:
   - As you update the DP table, keep track of the maximum value in `dp[i][j]`, as this will represent the side length of the largest square found.

4. **Return the Area**:
   - The area of the largest square will be the square of the maximum side length found.

### Implementation:

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix:
            return 0
        
        m, n = len(matrix), len(matrix[0])
        dp = [[0] * n for _ in range(m)]
        max_side = 0
        
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == '1':
                    if i == 0 or j == 0:
                        dp[i][j] = 1
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                    max_side = max(max_side, dp[i][j])
        
        return max_side * max_side
```

### Explanation:

1. **Initialization**:
   - The DP table is initialized with zeros, and we iterate through the matrix to fill it based on the state transition logic.

2. **DP Table Update**:
   - For each cell `(i, j)` in the matrix, if `matrix[i][j]` is `'1'`, update `dp[i][j]` based on the minimum of the three neighboring cells plus one.

3. **Tracking the Maximum Square**:
   - While updating, we keep track of the largest side length encountered.

4. **Calculate and Return Area**:
   - The area of the largest square is `max_side * max_side`.

### Complexity Analysis:
- **Time Complexity**: O(m * n), where `m` is the number of rows and `n` is the number of columns in the matrix. We iterate through each cell once.
- **Space Complexity**: O(m * n) for the DP table. This can be optimized to O(n) by using a single array if needed.

### Example Walkthrough:
For the input matrix:
```
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
```
The DP table will look like:
```
[
  [1,0,1,0,0],
  [1,0,1,1,1],
  [1,1,2,2,2],
  [1,0,0,1,0]
]
```
The largest side length is `2`, so the area of the largest square is `2 * 2 = 4`.

This dynamic programming approach efficiently finds the largest square of `1`s in the given matrix and calculates its area.
