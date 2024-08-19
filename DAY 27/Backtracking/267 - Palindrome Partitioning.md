# [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)

The task is to partition the given string `s` such that every substring in the partition is a **palindrome**. We need to return all possible palindrome partitionings of `s`.

### Approach:
We can solve this problem using **backtracking**. The key idea is to try every possible partition of the string and check if each substring in the partition is a palindrome.

### Steps:
1. **Backtracking**: We start from the beginning of the string, and for each position, we try to partition the string into substrings. For every partition, we check if the substring is a palindrome.
   - If it is a palindrome, we recursively partition the remaining part of the string.
   - If the entire string is partitioned into palindromes, we add this partition to the result.

2. **Palindrome Check**: For each substring we create, we need a helper function to check whether the substring is a palindrome. This can be done by checking if the string is equal to its reverse.

### Detailed Solution:

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        result = []
        
        # Helper function to check if a given string is a palindrome
        def is_palindrome(sub: str) -> bool:
            return sub == sub[::-1]
        
        # Backtracking function to find all palindrome partitions
        def backtrack(start: int, path: List[str]):
            # If we have reached the end of the string, add the current path to result
            if start == len(s):
                result.append(path[:])  # Add a copy of the path
                return
            
            # Explore every possible partition
            for end in range(start, len(s)):
                substring = s[start:end+1]
                # If the substring is a palindrome, proceed with the rest
                if is_palindrome(substring):
                    path.append(substring)  # Choose
                    backtrack(end+1, path)  # Explore
                    path.pop()  # Unchoose (backtrack)
        
        # Start the backtracking from the beginning of the string
        backtrack(0, [])
        return result
```

### Explanation:

1. **`is_palindrome` function**:
   - This helper function takes a substring and checks if it is a palindrome by comparing the substring with its reverse.

2. **`backtrack` function**:
   - `start` keeps track of the current position from which we are trying to partition the string.
   - `path` is the current partition (list of substrings) that we are building.
   - If we reach the end of the string (i.e., `start == len(s)`), it means we have found a valid partition, so we add `path` to the result.
   - For every position from `start` to the end of the string, we extract a substring and check if it is a palindrome. If it is, we add it to the path and recursively call `backtrack` for the remaining part of the string (i.e., starting from `end + 1`).
   - After exploring all options, we remove the last added substring (backtrack) and try the next possibility.

3. **Base Case**:
   - When `start` equals the length of the string, we have reached the end of the string, meaning we have a valid partition, so we add it to the result.

### Example Walkthrough:

#### Example 1:
```python
s = "aab"
```

- We start with an empty path `[]` and try every possible partition:
  1. The first partition is `"a"`, which is a palindrome, so we proceed with the rest of the string.
  2. Now, we are left with `"ab"`. We partition it as `"a"` and `"b"` (both are palindromes).
  3. So, one valid partition is `["a", "a", "b"]`.
  4. Another option is to partition `"aab"` as `["aa", "b"]`, where `"aa"` is a palindrome.

Thus, the result for this example is:
```python
[["a", "a", "b"], ["aa", "b"]]
```

#### Example 2:
```python
s = "a"
```

- There's only one possible partition, which is `["a"]`.

Thus, the result is:
```python
[["a"]]
```

### Time Complexity:
- **Time Complexity**: The time complexity is \( O(2^n \cdot n) \), where \( n \) is the length of the string. This is because there are \( 2^n \) possible partitions, and for each partition, we are checking if the substrings are palindromes, which takes \( O(n) \) time in the worst case.
  
- **Space Complexity**: The space complexity is \( O(n) \) for the recursion stack, where \( n \) is the length of the string, and \( O(n) \) space for storing the current path.

### Conclusion:
This approach efficiently solves the problem using backtracking, exploring all possible partitions and filtering only those that consist of palindromes. It ensures that we find all valid palindrome partitions for the given string.
