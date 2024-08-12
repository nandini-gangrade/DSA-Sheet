# [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/)

To solve this problem, you can use Dynamic Programming to find the minimum path sum from the top-left corner to the bottom-right corner of the grid.

### Approach:

1. **Define the DP Table**:
   - Let `dp[i][j]` represent the minimum path sum to reach cell `(i, j)` from the top-left corner `(0, 0)`.

2. **Base Case**:
   - The starting point `dp[0][0]` is simply the value at the top-left corner of the grid: `dp[0][0] = grid[0][0]`.

3. **Transition**:
   - For each cell `(i, j)`, the minimum path sum to reach that cell can come from either the left `(i, j-1)` or from above `(i-1, j)`. Therefore, the value of `dp[i][j]` is the minimum of the two possible paths plus the value of the current cell:
     - `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`
   - Special care must be taken for the cells in the first row and the first column, as they can only be reached from one direction (left for the first row, above for the first column).

4. **Final Answer**:
   - The answer will be `dp[m-1][n-1]`, representing the minimum path sum to reach the bottom-right corner of the grid.

### Code Implementation:

Here is the implementation using Dynamic Programming:

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        
        # Initialize the dp array with the first cell's value
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = grid[0][0]
        
        # Fill in the first row
        for j in range(1, n):
            dp[0][j] = dp[0][j-1] + grid[0][j]
        
        # Fill in the first column
        for i in range(1, m):
            dp[i][0] = dp[i-1][0] + grid[i][0]
        
        # Fill in the rest of the dp array
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
        
        # The answer is the value at the bottom-right corner
        return dp[m-1][n-1]
```

### Example Explanation:

1. **Example 1**:
   - Input: `grid = [[1,3,1],[1,5,1],[4,2,1]]`
   - The minimum path sum is `7`, corresponding to the path `1 → 3 → 1 → 1 → 1`.

2. **Example 2**:
   - Input: `grid = [[1,2,3],[4,5,6]]`
   - The minimum path sum is `12`, corresponding to the path `1 → 2 → 3 → 6`.

### Complexity Analysis:

- **Time Complexity**: O(m * n), where `m` is the number of rows and `n` is the number of columns in the grid. We iterate through each cell exactly once.
- **Space Complexity**: O(m * n) for the `dp` array. This can be optimized to O(n) by reusing a single row for dynamic programming if space optimization is needed.

This solution efficiently computes the minimum path sum from the top-left to the bottom-right corner of the grid, considering only valid moves (down or right).
