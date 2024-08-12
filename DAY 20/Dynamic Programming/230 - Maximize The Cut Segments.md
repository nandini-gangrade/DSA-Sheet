# [Maximize The Cut Segments](https://www.geeksforgeeks.org/problems/cutted-segments1642/1)

To solve this problem, we need to determine the maximum number of segments we can obtain by cutting a line segment of length `n` using cuts of lengths `x`, `y`, or `z`.

### Approach:

This problem can be solved using dynamic programming. We'll define a `dp` array where `dp[i]` represents the maximum number of segments that can be obtained from a line segment of length `i`.

### Steps:

1. **Initialization**: 
   - Create a `dp` array of size `n + 1` and initialize all elements to `-1`, indicating that initially, no segments can be made.
   - Set `dp[0] = 0`, because no cuts are needed for a line segment of length `0`.

2. **Filling the DP array**:
   - Iterate over each length `i` from `1` to `n`.
   - For each `i`, check if we can make a valid cut of length `x`, `y`, or `z`. If a cut is possible, update the `dp[i]` to the maximum number of segments obtained by adding 1 to the `dp` value of the remaining length (`i-x`, `i-y`, or `i-z`).

3. **Result**:
   - The value in `dp[n]` will give the maximum number of segments. If `dp[n]` is still `-1`, it means it's not possible to cut the segment into valid lengths, so return `0`.

### Code Implementation:

```python
class Solution:
    
    # Function to find the maximum number of cuts.
    def maximizeTheCuts(self, n, x, y, z):
        # Initialize dp array with -1
        dp = [-1] * (n + 1)
        
        # Base case: no length, no cuts
        dp[0] = 0
        
        # Fill the dp array
        for i in range(1, n + 1):
            if i >= x and dp[i - x] != -1:
                dp[i] = max(dp[i], dp[i - x] + 1)
            if i >= y and dp[i - y] != -1:
                dp[i] = max(dp[i], dp[i - y] + 1)
            if i >= z and dp[i - z] != -1:
                dp[i] = max(dp[i], dp[i - z] + 1)
        
        # If dp[n] is still -1, return 0, else return dp[n]
        return dp[n] if dp[n] != -1 else 0
```

### Example Explanation:

Let's walk through the provided examples:

1. **Example 1**:
   - Input: `n = 4, x = 2, y = 1, z = 1`
   - The line segment length is `4`.
   - Possible cuts: `2, 1, 1`.
   - We can cut the segment into `4` pieces of length `1`. Hence, the result is `4`.

2. **Example 2**:
   - Input: `n = 5, x = 5, y = 3, z = 2`
   - The line segment length is `5`.
   - Possible cuts: `5, 3, 2`.
   - We can cut the segment into `2` pieces with lengths `3` and `2`. Hence, the result is `2`.

### Complexity Analysis:

- **Time Complexity**: O(n). We iterate over each length from `1` to `n`, and for each length, we make constant-time updates based on the possible cuts.
- **Space Complexity**: O(n). We use a `dp` array of size `n + 1` to store the maximum number of cuts for each length.

This solution efficiently calculates the maximum number of cuts that can be made for a given segment length.
