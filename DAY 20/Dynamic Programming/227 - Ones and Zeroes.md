# [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/description/)

To solve the problem of finding the size of the largest subset of binary strings that contain at most `m` zeros and `n` ones, we can use dynamic programming (DP). This problem can be visualized as a knapsack problem where each binary string is an item with a cost (number of zeros and ones) and a value (contributing to the size of the subset).

### Approach

1. **DP Array Initialization:**
   - We'll use a 2D DP array `dp[i][j]` where `i` represents the number of zeros allowed and `j` represents the number of ones allowed. The value at `dp[i][j]` represents the maximum size of the subset that can be formed with at most `i` zeros and `j` ones.

2. **DP Array Update:**
   - For each string in `strs`, count the number of zeros (`zero_count`) and ones (`one_count`).
   - Update the DP table in reverse (to avoid overwriting values that are needed later) by iterating from `m` down to `zero_count` and from `n` down to `one_count`.
   - Update the DP value as `dp[i][j] = max(dp[i][j], dp[i-zero_count][j-one_count] + 1)`.

3. **Result Extraction:**
   - The result will be found in `dp[m][n]`, which represents the maximum subset size that can be formed with up to `m` zeros and `n` ones.

### Implementation

Here's the Python implementation of the above approach:

```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        # Initialize DP table with all zeros
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        
        # Process each string in the list
        for s in strs:
            # Count zeros and ones in the current string
            zero_count = s.count('0')
            one_count = len(s) - zero_count
            
            # Update the DP table in reverse to avoid overwriting values prematurely
            for i in range(m, zero_count - 1, -1):
                for j in range(n, one_count - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1)
        
        # The answer is the maximum subset size with at most m zeros and n ones
        return dp[m][n]
```

### Explanation

- **Counting Zeros and Ones:**
  - For each binary string `s`, `zero_count` gives the number of '0's, and `one_count` gives the number of '1's.
  
- **Reverse Iteration:**
  - We iterate the DP table in reverse (from `m` to `zero_count` and `n` to `one_count`) to ensure that each string is only used once in the calculation.
  
- **DP Transition:**
  - The transition formula `dp[i][j] = max(dp[i][j], dp[i-zero_count][j-one_count] + 1)` considers whether to include the current string `s` in the subset or not.

### Complexity

- **Time Complexity:** O(L * m * n), where `L` is the length of `strs`. This is because we update the DP table for each string.
- **Space Complexity:** O(m * n) for the DP table.

This approach efficiently finds the maximum subset size that meets the given constraints on the number of zeros and ones.
