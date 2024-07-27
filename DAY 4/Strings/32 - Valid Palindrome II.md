# [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/description/)
[LeetCode Solution](https://leetcode.com/problems/valid-palindrome-ii/solutions/5544401/easy-solution-challenge-day-4-revisewitharsh) 

Given a string `s`, we need to check if it's possible to make it a palindrome by removing at most one character. A palindrome reads the same forward and backward, so our task is to see if we can achieve this property with minimal modifications.

## Approach

1. **Two-Pointer Technique**: Use two pointers, one starting from the beginning (`left`) and the other from the end (`right`) of the string.
2. **Compare Characters**: Move the pointers towards each other, comparing the characters at each step.
3. **Handle Mismatch**: If a mismatch is found:
   - Check if removing the character at `left` or `right` allows the rest of the string to be a palindrome.
   - This can be done by checking if the substrings `s[left+1:right+1]` or `s[left:right]` are palindromes.
4. **Continue Until End**: If the pointers cross without needing to remove more than one character, the string can be a palindrome with at most one deletion.

## Implementation

#### Python

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        def is_palindrome_range(left: int, right: int) -> bool:
            while left < right:
                if s[left] != s[right]:
                    return False
                left += 1
                right -= 1
            return True

        left, right = 0, len(s) - 1
        
        while left < right:
            if s[left] != s[right]:
                # Check the two possibilities when there's a mismatch
                return is_palindrome_range(left + 1, right) or is_palindrome_range(left, right - 1)
            left += 1
            right -= 1
        
        return True
```

#### C++

```cpp
class Solution {
public:
    bool validPalindrome(string s) {
        auto is_palindrome_range = [&](int left, int right) {
            while (left < right) {
                if (s[left] != s[right]) return false;
                left++;
                right--;
            }
            return true;
        };
        
        int left = 0, right = s.size() - 1;
        
        while (left < right) {
            if (s[left] != s[right]) {
                // Check the two possibilities when there's a mismatch
                return is_palindrome_range(left + 1, right) || is_palindrome_range(left, right - 1);
            }
            left++;
            right--;
        }
        
        return true;
    }
};
```

#### Java

```java
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return isPalindromeRange(s, left + 1, right) || isPalindromeRange(s, left, right - 1);
            }
            left++;
            right--;
        }
        
        return true;
    }
    
    private boolean isPalindromeRange(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) return false;
            left++;
            right--;
        }
        return true;
    }
}
```

#### JavaScript

```javascript
var validPalindrome = function(s) {
    const isPalindromeRange = (left, right) => {
        while (left < right) {
            if (s[left] !== s[right]) return false;
            left++;
            right--;
        }
        return true;
    };
    
    let left = 0, right = s.length - 1;
    
    while (left < right) {
        if (s[left] !== s[right]) {
            return isPalindromeRange(left + 1, right) || isPalindromeRange(left, right - 1);
        }
        left++;
        right--;
    }
    
    return true;
};
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string `s`. We may traverse the string twice in the worst case (once fully, then once for each possible deletion).
- **Space Complexity**: \(O(1)\), as we're only using a few pointers and variables, regardless of the input size.

This solution efficiently checks for the possibility of transforming the input string into a palindrome with at most one deletion using the two-pointer technique.
