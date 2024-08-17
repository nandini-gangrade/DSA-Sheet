# [402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/description/)

The problem asks to return the smallest possible integer after removing `k` digits from a given number string `num`. We must maintain the relative order of digits while removing the digits that would result in the smallest possible number. The main challenge is to do this efficiently, given that the length of the number can be large (up to 100,000).

### Key Idea:
We can approach this problem using a **greedy algorithm**. The goal is to remove digits that are large and out of place to make the number smaller, while maintaining the left-to-right order.

To achieve this efficiently, we use a **monotonic stack**. The idea is to build the smallest possible number by traversing the digits of `num` and maintaining a stack of digits in increasing order. If the current digit is smaller than the last digit in the stack, we pop from the stack (i.e., remove the larger digit) and push the smaller digit. This process simulates removing the largest digits to make the number smaller.

### Steps:
1. **Stack Simulation**:
   - Use a stack to store the digits of the smallest number as we iterate through the input string.
   - If the current digit is smaller than the top of the stack (and we still need to remove more digits), pop the stack to remove the larger digits.
   - Push the current digit to the stack.
   
2. **Remove Remaining Digits**:
   - After processing all digits, if we haven't removed `k` digits, pop additional digits from the stack until we've removed exactly `k`.

3. **Handle Leading Zeros**:
   - After constructing the number, remove any leading zeros.

4. **Edge Case**:
   - If we remove all digits (i.e., `k == len(num)`), return "0".

### Code Implementation:

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        
        # Traverse each digit in the string `num`
        for digit in num:
            # While the current digit is smaller than the last one in the stack and we still need to remove digits (k > 0)
            while stack and k > 0 and stack[-1] > digit:
                stack.pop()  # Remove the last digit
                k -= 1  # Decrease the count of digits to remove
            
            # Push the current digit into the stack
            stack.append(digit)
        
        # If there are still digits to remove, remove them from the end of the number (stack)
        while k > 0:
            stack.pop()
            k -= 1
        
        # Join the stack into a string and remove any leading zeros
        result = ''.join(stack).lstrip('0')
        
        # If the result is empty after stripping zeros, return "0"
        return result if result else "0"
```

### Explanation:

1. **Stack Simulation**:
   - For each digit in `num`, we compare it with the top of the stack (the last added digit).
   - If the current digit is smaller and we still have digits to remove (`k > 0`), we pop the stack, effectively removing a larger, out-of-place digit to make the resulting number smaller.

2. **Remove Excess Digits**:
   - After processing the entire string, if `k` is still greater than 0 (meaning we haven't removed enough digits), we pop the remaining digits from the stack.

3. **Handle Leading Zeros**:
   - The result might contain leading zeros, especially after popping digits, so we use `.lstrip('0')` to remove them.
   - If the final result is an empty string (which happens when the number becomes zero), we return "0".

### Time Complexity:
- **O(n)**, where `n` is the length of `num`. We traverse the string once, and each digit is pushed and popped from the stack at most once.

### Space Complexity:
- **O(n)** for the stack to store the digits of the resulting number.

### Example Walkthrough:

#### Example 1:
Input: `num = "1432219", k = 3`
- Initial num: 1432219
- Remove 4 (k = 2): Stack becomes [1, 3, 2]
- Remove 3 (k = 1): Stack becomes [1, 2]
- Remove 2 (k = 0): Stack becomes [1, 2, 1]
- Final stack: [1, 2, 1, 9]
- Answer: "1219"

#### Example 2:
Input: `num = "10200", k = 1`
- Initial num: 10200
- Remove 1 (k = 0): Stack becomes [0, 2, 0, 0]
- Strip leading zeros: "200"
- Answer: "200"

#### Example 3:
Input: `num = "10", k = 2`
- Remove both digits, no digits remain.
- Answer: "0"

### Edge Cases:
1. **All digits removed**: If `k == len(num)`, return "0".
2. **Leading Zeros**: Ensure no leading zeros in the result unless the result is "0".

This approach efficiently solves the problem using a greedy stack-based solution.
