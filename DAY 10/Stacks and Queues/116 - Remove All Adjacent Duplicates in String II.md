# [1209. Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/description/)

- Given a string `s` and an integer `k`, we need to repeatedly remove `k` adjacent equal characters from `s`.
- The removal should continue until no more `k` adjacent characters exist.

## Intuition

- We can use a stack to keep track of characters and their counts.
- Traverse the string:
  - For each character, check if the top of the stack has the same character.
  - If so, increment the count.
  - If the count reaches `k`, pop the character from the stack.
  - If the character is different, push it onto the stack with a count of `1`.
- Finally, construct the resulting string from the stack.

## Approach

1. **Use a Stack:** Maintain a stack of pairs `(char, count)` where `char` is a character in the string and `count` is the number of consecutive occurrences.
2. **Iterate through the String:**
   - If the stack is not empty and the top of the stack has the same character as the current one, increment the count.
   - If the count equals `k`, pop the element from the stack.
   - If the current character is different from the top of the stack, push `(char, 1)` onto the stack.
3. **Build the Result String:** After processing the entire string, the stack contains the final characters and their counts. Use these to construct the resulting string.

## Code

```python
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        # Initialize stack
        stack = []
        
        # Iterate through the characters in the string
        for char in s:
            if stack and stack[-1][0] == char:
                # Increment count if the character matches the stack's top
                stack[-1][1] += 1
                # If count reaches k, pop the element
                if stack[-1][1] == k:
                    stack.pop()
            else:
                # Push the character onto the stack with a count of 1
                stack.append([char, 1])
        
        # Construct the result string from the stack
        result = ''.join(char * count for char, count in stack)
        return result
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\), where \(n\) is the length of the string `s`. Each character is pushed and popped from the stack at most once.
- **Space Complexity:** \(O(n)\), for storing characters and counts in the stack.

This approach effectively and efficiently reduces the problem to a manageable size by leveraging a stack to track sequences of characters and their counts.
