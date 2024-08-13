# [91. Decode Ways](https://leetcode.com/problems/decode-ways/description/)

To solve the problem of counting the number of ways to decode a given string of digits into letters, you can use dynamic programming. Here's a detailed breakdown of the approach:

### Approach:

1. **Dynamic Programming Array**:
   - Let's define a `dp` array where `dp[i]` represents the number of ways to decode the substring `s[0:i]`.
   - Initialize `dp[0] = 1` because there is exactly one way to decode an empty string (by doing nothing).

2. **Iterate Through the String**:
   - For each character in the string, consider both single-digit and two-digit possibilities:
     - **Single-Digit**: If `s[i-1]` is between `'1'` and `'9'`, then `dp[i]` can include all the ways to decode the substring `s[0:i-1]`.
     - **Two-Digit**: If the two characters `s[i-2:i]` form a valid number between `'10'` and `'26'`, then `dp[i]` can include all the ways to decode the substring `s[0:i-2]`.

3. **Handle Edge Cases**:
   - If the string starts with `'0'`, it is not decodable, so return `0`.
   - Any sequence with an invalid two-digit number (e.g., "06") also invalidates the decoding path.

4. **Final Answer**:
   - The value `dp[len(s)]` will give the total number of ways to decode the entire string `s`.

### Code Implementation:

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        # Edge case for empty string or string starting with '0'
        if not s or s[0] == '0':
            return 0
        
        n = len(s)
        dp = [0] * (n + 1)
        dp[0] = 1  # There's one way to decode an empty string
        dp[1] = 1  # There's one way to decode a string of length 1, if it's valid
        
        for i in range(2, n + 1):
            # Single digit decoding
            if s[i-1] != '0':
                dp[i] += dp[i-1]
            
            # Two digits decoding
            two_digit = int(s[i-2:i])
            if 10 <= two_digit <= 26:
                dp[i] += dp[i-2]
        
        return dp[n]
```

### Example Explanations:

1. **Example 1**:
   - Input: `s = "12"`
   - Possible decodings: `"AB"` (1 2) and `"L"` (12)
   - Output: `2`

2. **Example 2**:
   - Input: `s = "226"`
   - Possible decodings: `"BZ"` (2 26), `"VF"` (22 6), and `"BBF"` (2 2 6)
   - Output: `3`

3. **Example 3**:
   - Input: `s = "06"`
   - The string is not decodable because `"06"` is not a valid encoding.
   - Output: `0`

### Complexity Analysis:

- **Time Complexity**: O(n), where `n` is the length of the string. We only need to iterate through the string once.
- **Space Complexity**: O(n), for the `dp` array used to store the number of ways to decode each substring.

This solution efficiently counts the number of ways to decode the string while handling all edge cases.
