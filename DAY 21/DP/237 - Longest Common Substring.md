# [Longest Common Substring](https://www.geeksforgeeks.org/problems/longest-common-substring1452/1)

To solve the problem of finding the length of the longest common substring between two given strings `str1` and `str2`, we can use dynamic programming. Here's a step-by-step explanation of the approach:

### Dynamic Programming Approach:

1. **DP Table Initialization**:
   - We create a 2D DP table where `dp[i][j]` will store the length of the longest common substring that ends with `str1[i-1]` and `str2[j-1]`.

2. **State Transition**:
   - If `str1[i-1] == str2[j-1]`, then we can extend the common substring that ends at `str1[i-1]` and `str2[j-1]`, so `dp[i][j] = dp[i-1][j-1] + 1`.
   - If the characters do not match, `dp[i][j] = 0` because the substring ends at that position.

3. **Result**:
   - The maximum value in the DP table will give us the length of the longest common substring.

4. **Space Optimization**:
   - Instead of using a full 2D DP table, we can optimize space by using two 1D arrays, as we only need the current and previous rows at any point in time.

### Implementation:

```python
class Solution:
    def longestCommonSubstr(self, str1: str, str2: str) -> int:
        n = len(str1)
        m = len(str2)
        
        # Initialize the DP table with 0s
        dp = [[0] * (m + 1) for _ in range(n + 1)]
        max_len = 0
        
        # Build the table
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                if str1[i - 1] == str2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                    max_len = max(max_len, dp[i][j])
                else:
                    dp[i][j] = 0
        
        return max_len
```

### Explanation:

1. **Initialization**:
   - The DP table is initialized with zeros. `dp[i][j]` is 0 when either `i` or `j` is 0 because there's no common substring with an empty string.

2. **Filling the DP Table**:
   - The table is filled based on whether the characters from `str1` and `str2` match at the respective indices.
   - Whenever a match is found, the length of the common substring is updated based on the previous lengths stored in the DP table.

3. **Finding the Maximum Length**:
   - During the table update, we keep track of the maximum value found in the DP table, which represents the length of the longest common substring.

### Example Walkthrough:

For `str1 = "ABCDGH"` and `str2 = "ACDGHR"`:
- The DP table will have a maximum value of `4`, corresponding to the common substring `"CDGH"`.

For `str1 = "ABC"` and `str2 = "ACB"`:
- The DP table will have a maximum value of `1`, corresponding to the common substrings `"A"`, `"B"`, or `"C"`.

### Complexity Analysis:
- **Time Complexity**: O(n * m), where `n` is the length of `str1` and `m` is the length of `str2`.
- **Space Complexity**: O(n * m) using the full DP table, or O(min(n, m)) with space optimization.

This approach efficiently finds the longest common substring using dynamic programming.
