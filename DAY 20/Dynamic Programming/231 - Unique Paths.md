# [62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)

To solve this problem, we need to find the number of unique paths the robot can take to move from the top-left corner to the bottom-right corner of a grid. The robot can only move down or right.

### Approach:

This problem can be approached using **Dynamic Programming** or by using **Combinatorics**.

#### 1. Dynamic Programming Approach:
We can define a 2D array `dp` where `dp[i][j]` represents the number of unique paths to reach cell `(i, j)` from the starting point `(0, 0)`.

- **Base Case**: 
  - `dp[0][0] = 1` because there is exactly one way to be at the starting point.
- **Transition**:
  - For each cell `(i, j)`, the robot could have come either from the left `(i, j-1)` or from above `(i-1, j)`. Therefore, the number of paths to `(i, j)` is the sum of paths to the cells directly above and to the left of it:
    - `dp[i][j] = dp[i-1][j] + dp[i][j-1]`
  
- **Final Answer**:
  - The answer will be `dp[m-1][n-1]` because that represents the number of paths to the bottom-right corner.

#### 2. Combinatorial Approach:
The problem can also be interpreted as a combinatorial problem where you need to make exactly `(m-1)` downward moves and `(n-1)` rightward moves. The total number of moves needed is `(m-1) + (n-1) = m+n-2`. Out of these moves, you need to choose `(m-1)` (or equivalently `(n-1)`) positions for the downward moves. This can be computed using the binomial coefficient:
- `C(m+n-2, m-1)` or `C(m+n-2, n-1)`

### Code Implementation:

Here is the implementation using Dynamic Programming:

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # Create a 2D DP array initialized to 0
        dp = [[0] * n for _ in range(m)]
        
        # Initialize the first row and first column to 1
        for i in range(m):
            dp[i][0] = 1
        for j in range(n):
            dp[0][j] = 1
        
        # Fill in the DP array
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        
        # Return the number of unique paths to reach the bottom-right corner
        return dp[m-1][n-1]
```

### Example Explanation:

1. **Example 1**:
   - Input: `m = 3, n = 7`
   - The number of unique paths to reach the bottom-right corner from the top-left is `28`.

2. **Example 2**:
   - Input: `m = 3, n = 2`
   - There are `3` unique ways to reach the bottom-right corner:
     1. Right -> Down -> Down
     2. Down -> Down -> Right
     3. Down -> Right -> Down

### Complexity Analysis:

- **Time Complexity**: O(m * n), because we fill out a `m x n` table.
- **Space Complexity**: O(m * n) for the DP array.

This solution efficiently computes the number of unique paths for the robot to reach its destination.
