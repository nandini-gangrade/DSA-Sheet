# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

To implement the `minWindow` method for finding the minimum window substring of `s` that contains all characters of `t`, you can follow the sliding window approach with two pointers. Here's a detailed explanation along with the code:

### Approach

1. **Initialization**:
   - **`need`**: A Counter to store the frequency of each character in `t`.
   - **`window`**: A defaultdict to store the frequency of each character in the current window of `s`.
   - **`have`**: A count of how many unique characters from `t` are currently in the window with the required frequency.
   - **`required`**: The number of unique characters needed in the window, which is the size of the `need` Counter.
   - **`res`**: A tuple to keep track of the minimum window length and its start and end indices.

2. **Sliding Window**:
   - Expand the window by moving the `right` pointer and update the `window` Counter.
   - If the window contains all the required characters with the correct frequencies, try to shrink the window from the left using the `left` pointer.
   - Keep track of the smallest valid window found.

3. **Edge Cases**:
   - If `t` is longer than `s`, immediately return an empty string because it's impossible to find such a window.

### Code Implementation

Here's the complete implementation in Python:

```python
from collections import Counter, defaultdict

class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if not s or not t:
            return ""

        # Frequency count of characters in t
        need = Counter(t)
        window = defaultdict(int)
        
        # Number of unique characters that match the requirement
        have = 0
        required = len(need)
        
        # Result tuple (window length, left, right)
        res = float('inf'), None, None
        
        left = 0
        
        # Expand the window with the right pointer
        for right in range(len(s)):
            char = s[right]
            window[char] += 1
            
            # Check if the current character satisfies the requirement
            if char in need and window[char] == need[char]:
                have += 1
            
            # Shrink the window from the left as long as it's valid
            while have == required:
                # Update the result if the current window is smaller
                if (right - left + 1) < res[0]:
                    res = (right - left + 1, left, right)
                
                # Move the left pointer
                window[s[left]] -= 1
                if s[left] in need and window[s[left]] < need[s[left]]:
                    have -= 1
                left += 1
        
        # Return the smallest window found
        return "" if res[0] == float('inf') else s[res[1]:res[2] + 1]
```

### Explanation

- **Initialization**:
  - **`need`**: Tracks the count of each character required.
  - **`window`**: Keeps track of characters in the current window of `s`.
  - **`have`**: Counts how many unique characters from `t` are met in the current window with required frequency.
  - **`res`**: Stores the smallest valid window size and its position.

- **Sliding Window Mechanism**:
  - The right pointer (`right`) expands the window.
  - When the window is valid (i.e., contains all required characters with the correct frequency), the left pointer (`left`) is used to contract the window to find the minimum size.
  - The result is updated whenever a smaller valid window is found.

### Complexity

- **Time Complexity**: \(O(m + n)\)
  - The two pointers (`left` and `right`) traverse the string `s` at most once, and operations with hashmaps are constant time on average.

- **Space Complexity**: \(O(n)\)
  - The hashmaps `need` and `window` store character frequencies where `n` is the length of string `t`.

This approach is efficient and handles large inputs well within the given constraints.
