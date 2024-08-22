# [Find all possible palindromic partitions of a String](https://www.geeksforgeeks.org/problems/find-all-possible-palindromic-partitions-of-a-string/1)

Here's an explanation of the code you provided for finding all possible palindromic partitions of a given string:

### Problem Description:
Given a string `S`, the task is to find all possible palindromic partitions of the string. A palindromic partition of a string is a partitioning of the string into substrings, where each substring is a palindrome.

### Approach:
The problem is approached using backtracking. We recursively partition the string and check if the substrings formed are palindromes. If a substring is a palindrome, we continue partitioning the remaining string. The process is repeated until the entire string is partitioned. 

### Detailed Explanation of the Code:

1. **`isPalindrome` Function**:
   - This helper function checks if a substring `s[start:end]` is a palindrome. 
   - It does so by comparing the characters from the beginning and the end, moving towards the center. 
   - If any characters do not match, it returns `false`, otherwise it returns `true`.

2. **`solve` Function**:
   - This is a recursive function that partitions the string and stores the palindromic partitions in the `output` list.
   - It takes four parameters: 
     - `s`: the original string,
     - `output`: a temporary list to store current partitions,
     - `index`: the current index in the string to start partitioning from,
     - `ans`: the final list of all palindromic partitions.
   - The function checks if `index` has reached the end of the string. If so, the current partition (stored in `output`) is added to the result list `ans`.
   - It iterates from the current index to the end of the string, attempting to partition the string into substrings. For each substring, it checks if it's a palindrome using `isPalindrome`.
   - If the substring is a palindrome, it is added to `output`, and the function recursively calls itself to partition the remaining part of the string.
   - After the recursive call, the last added substring is removed (backtracking) to try other potential partitions.

3. **`allPalindromicPerms` Function**:
   - This is the main function that initializes necessary variables and calls the `solve` function.
   - It returns the list of all palindromic partitions stored in `ans`.

### Complexity:
- **Time Complexity**: O(N * 2^N), where N is the length of the string. This is due to the fact that there are 2^N possible partitions of the string, and checking if each substring is a palindrome takes O(N) time.
- **Space Complexity**: O(N^2), primarily due to the space used for storing intermediate palindromic checks and results.

### Example:

For the string `S = "madam"`, the palindromic partitions would be:
- `m a d a m`
- `m ada m`
- `madam`

### Full Python Code (Equivalent to the provided C++ code):

```python
class Solution:
    def isPalindrome(self, s, start, end):
        while start <= end:
            if s[start] != s[end]:
                return False
            start += 1
            end -= 1
        return True
    
    def solve(self, s, output, index, ans):
        if index >= len(s):
            ans.append(output[:])
            return
        
        for i in range(index, len(s)):
            if self.isPalindrome(s, index, i):
                output.append(s[index:i+1])
                self.solve(s, output, i + 1, ans)
                output.pop()
    
    def allPalindromicPerms(self, s):
        ans = []
        output = []
        self.solve(s, output, 0, ans)
        return ans

# Example usage:
sol = Solution()
print(sol.allPalindromicPerms("geeks"))
print(sol.allPalindromicPerms("madam"))
```

### Output:
For `S = "geeks"`:
- `[['g', 'e', 'e', 'k', 's'], ['g', 'ee', 'k', 's']]`

For `S = "madam"`:
- `[['m', 'a', 'd', 'a', 'm'], ['m', 'ada', 'm'], ['madam']]`

This code correctly identifies and returns all possible palindromic partitions of the string.
