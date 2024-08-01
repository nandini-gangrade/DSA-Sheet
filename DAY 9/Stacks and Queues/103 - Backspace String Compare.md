# https://leetcode.com/problems/backspace-string-compare/description/

To solve the problem of comparing two strings when both are typed into empty text editors, we need to simulate the effect of the '#' backspace character. We can achieve this in an efficient manner using two-pointer technique that works in O(n) time and O(1) space. Let's walk through the approach:

## Approach

1. **Two Pointers:** We'll use two pointers, one for each string (`s` and `t`), starting from the end of each string. This allows us to simulate the backspace operation without needing extra space for another data structure.

2. **Backspace Simulation:** We'll traverse each string from right to left, skipping characters as necessary to account for the backspace (`#`) operations. We maintain a counter to track the number of backspaces needed (`skipS` for `s` and `skipT` for `t`).

3. **Comparison:** For each step, we find the next valid character (after accounting for backspaces) in both strings and compare them. If at any point the characters differ, we return `false`.

4. **End of Strings:** If both strings are processed completely and match, return `true`.

## Implementation

```python
class Solution(object):
    def backspaceCompare(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        def next_valid_char(index, str):
            skip = 0
            while index >= 0:
                if str[index] == '#':
                    skip += 1
                elif skip > 0:
                    skip -= 1
                else:
                    break
                index -= 1
            return index

        i, j = len(s) - 1, len(t) - 1

        while i >= 0 or j >= 0:
            i = next_valid_char(i, s)
            j = next_valid_char(j, t)

            if i >= 0 and j >= 0 and s[i] != t[j]:
                return False

            if (i >= 0) != (j >= 0):  # Check if both indices are valid or both are invalid
                return False

            i -= 1
            j -= 1

        return True

# Example Usage:
# sol = Solution()
# print(sol.backspaceCompare("ab#c", "ad#c"))  # Output: True
# print(sol.backspaceCompare("ab##", "c#d#"))  # Output: True
# print(sol.backspaceCompare("a#c", "b"))     # Output: False
```

### Explanation

- **next_valid_char Function:** This helper function moves the pointer to the next valid character that should be compared, skipping characters as necessary for backspaces.

- **Two-Pointer Traversal:** We iterate over the strings backwards, updating the pointers to skip invalidated characters and directly comparing the current valid characters.

- **Edge Cases:** If one string finishes before the other, we check if both pointers are at invalid indices (which indicates both strings are fully traversed and matched).

## Complexity

- **Time Complexity:** O(n + m), where n and m are the lengths of the strings `s` and `t`, respectively. We traverse each string once.
  
- **Space Complexity:** O(1), as we only use a few extra variables and do not store the processed strings.

This solution effectively handles the backspace operation and provides an efficient way to compare the two strings in the required time and space constraints.
