# [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/description/)

## Problem Understanding

Given two strings `s` and `t`, we need to find how many different subsequences of `s` can form the string `t`. A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

### Examples

**Example 1:**

- **Input:** `s = "rabbbit"`, `t = "rabbit"`
- **Output:** `3`

There are 3 distinct ways to form "rabbit" from "rabbbit":

1. `rabb`b`it`
2. `rab`b`bit`
3. `ra`b`bbit`

**Example 2:**

- **Input:** `s = "babgbag"`, `t = "bag"`
- **Output:** `5`

There are 5 distinct ways to form "bag" from "babgbag":

1. `ba`bg`bag`
2. `ba`b`gbag`
3. `bab`g`bag`
4. `babg`bag
5. `babgba`g

## Intuition

To solve the problem, we use dynamic programming to build a solution iteratively. The key idea is to maintain a table `dp` where `dp[i][j]` represents the number of distinct subsequences of `s[:i]` that equals `t[:j]`. Here are the main points:

- If `t` is empty (`j = 0`), there is exactly one subsequence of `s` that matches `t`, which is the empty subsequence. Hence, `dp[i][0] = 1` for all `i`.
- If `s` is empty (`i = 0`) and `t` is not, there are no subsequences that can form `t`. Hence, `dp[0][j] = 0` for `j > 0`.
- If the current characters `s[i-1]` and `t[j-1]` match, then we can either use this character to match with `t` or skip it. Therefore, `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]`.
- If the characters do not match, the character `s[i-1]` cannot contribute to a match, so `dp[i][j] = dp[i-1][j]`.

## Approach

1. **Initialize the DP Table**: Create a 2D table `dp` with dimensions `(len(s)+1) x (len(t)+1)`.

2. **Base Case**: Set `dp[i][0] = 1` for all `i` because an empty `t` is a subsequence of any `s`.

3. **Fill the DP Table**:
   - Iterate over `i` from `1` to `len(s)`.
   - Iterate over `j` from `1` to `len(t)`.
   - Update `dp[i][j]` based on whether `s[i-1]` matches `t[j-1]`.

4. **Return the Result**: The answer is `dp[len(s)][len(t)]`, which gives the number of distinct subsequences of `s` that equal `t`.

## Code Implementation

```python
class Solution(object):
    def numDistinct(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: int
        """
        m, n = len(s), len(t)
        
        # Create a 2D DP array initialized with zeros
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        
        # Every string can match an empty t by deleting all characters
        for i in range(m + 1):
            dp[i][0] = 1
        
        # Fill the DP table
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                # If the characters match
                if s[i - 1] == t[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j]
                else:
                    dp[i][j] = dp[i - 1][j]
        
        # The answer is in the bottom-right corner of the table
        return dp[m][n]

# Example usage:
solution = Solution()
print(solution.numDistinct("rabbbit", "rabbit"))  # Output: 3
print(solution.numDistinct("babgbag", "bag"))    # Output: 5
```

## Complexity Analysis

- **Time Complexity**: \(O(m. n)\), where \(m\) is the length of `s` and \(n\) is the length of `t`. We fill a table of size \(mn\).
- **Space Complexity**: \(O(m. n)\), which is required for the DP table.

This dynamic programming approach efficiently calculates the number of distinct subsequences using a table to store intermediate results, avoiding redundant calculations and making the solution feasible for larger input sizes.
