# [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/description/)

To solve the problem of finding the length of the longest substring containing the same letter after performing at most `k` character replacements, we can use a sliding window approach with a frequency count of characters. This approach will help us efficiently find the maximum length of a substring with at most `k` different characters.

### Approach

1. **Sliding Window Technique:**
   - We maintain a window that represents the current substring we are considering.
   - We try to expand this window as much as possible by including more characters from the string.

2. **Frequency Count:**
   - Keep a frequency count of characters in the current window.
   - Track the count of the most frequently occurring character in the current window (`max_count`).

3. **Window Expansion and Contraction:**
   - For each character in the string, add it to the window and update its count.
   - Calculate the number of characters that need to be replaced to make the entire window consist of a single repeated character. This can be done using the formula: `window_length - max_count`, where `window_length` is the size of the current window.
   - If this value is greater than `k`, it means we need more than `k` replacements to make the current window valid, so we shrink the window from the left.

4. **Update Maximum Length:**
   - Throughout the process, keep track of the maximum length of a valid window.

### Implementation

Here's the implementation of the described approach:

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        max_length = 0
        left = 0
        max_count = 0
        count = {}

        for right in range(len(s)):
            char = s[right]
            count[char] = count.get(char, 0) + 1
            max_count = max(max_count, count[char])

            # Current window size is right - left + 1
            # If more than k replacements are needed, shrink window from left
            while (right - left + 1) - max_count > k:
                left_char = s[left]
                count[left_char] -= 1
                left += 1
            
            # Update maximum length found
            max_length = max(max_length, right - left + 1)

        return max_length
```

### Explanation

- **Frequency Map:** We use a dictionary `count` to store the frequency of each character in the current window.
- **`max_count`:** This keeps track of the count of the most frequently occurring character in the current window.
- **Window Adjustments:** If the current window size minus `max_count` is greater than `k`, it means we need more than `k` changes to make the window valid, so we move the left pointer to reduce the window size.
- **Max Length:** We update `max_length` with the size of the window whenever it is valid.

### Complexity

- **Time Complexity:** \(O(n)\), where \(n\) is the length of the string, because each character is processed at most twice (once added and once removed).
- **Space Complexity:** \(O(1)\), since the dictionary can have at most 26 keys (for each uppercase English letter).

This approach efficiently finds the longest valid substring by using the sliding window technique to adjust the size of the substring dynamically based on the constraints.
