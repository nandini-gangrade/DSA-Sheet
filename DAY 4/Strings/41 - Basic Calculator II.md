# [227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/description/)
[Leetcode Solution](https://leetcode.com/problems/basic-calculator-ii/solutions/5544990/easy-solution-challenge-day-4-revisewitharsh)

To solve the problem of evaluating a mathematical expression given as a string, you can use a stack-based approach to handle the operators and maintain the order of operations. Here's a structured approach to achieve this:

## Approach

1. **Initialization**:
   - Use a stack to keep track of numbers and intermediate results.
   - Maintain a current number being processed and a variable to keep track of the last operator encountered.

2. **Iteration through the String**:
   - Traverse the string character by character.
   - Update the current number when encountering digits.
   - When encountering an operator or the end of the string:
     - Evaluate the last number based on the previous operator and update the stack.
     - Update the operator for the next set of operations.
     - Reset the current number for the next number in the expression.

3. **Final Calculation**:
   - After processing all characters, there might be a number left to process. Add this to the stack.

4. **Summarize the Result**:
   - Sum all numbers in the stack to get the final result.

### Detailed Steps

1. **Handle Spaces**: Ignore spaces to avoid unnecessary processing.

2. **Handle Numbers**: Extract and convert numbers from the string.

3. **Handle Operators**: Depending on the operator (`+`, `-`, `*`, `/`), perform the respective arithmetic operation.

4. **Integer Division**: Ensure division truncates towards zero as specified.

## Code

```python
class Solution:
    def calculate(self, s: str) -> int:
        def apply_op(ops, num, op):
            if op == '+':
                ops.append(num)
            elif op == '-':
                ops.append(-num)
            elif op == '*':
                ops[-1] = ops[-1] * num
            elif op == '/':
                ops[-1] = int(ops[-1] / num)  # Truncate towards zero
        
        ops = []
        num = 0
        op = '+'
        n = len(s)
        
        i = 0
        while i < n:
            char = s[i]
            
            if char.isdigit():
                num = num * 10 + int(char)
            elif char in '+-*/':
                apply_op(ops, num, op)
                num = 0
                op = char
            elif char == ' ':
                pass
            
            i += 1
        
        apply_op(ops, num, op)  # Apply the last number
        return sum(ops)

# Example usage
sol = Solution()
print(sol.calculate("3+2*2"))  # Output: 7
print(sol.calculate("3/2"))    # Output: 1
print(sol.calculate("3+5 / 2"))  # Output: 5
```

## Explanation

1. **`apply_op` Function**: Handles different operations based on the operator. It applies `+` and `-` directly to the stack, and for `*` and `/`, it performs the operation with the last element in the stack.

2. **Processing Loop**:
   - Accumulate digits to form numbers.
   - When encountering an operator, apply the previous number with the last operator and update the current operator.
   - At the end of the loop, apply the last accumulated number with the last operator.

3. **Final Computation**: Sum all numbers in the stack to get the final result.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the input string. Each character is processed once.
- **Space Complexity**: \(O(n)\) in the worst case due to the stack storing all numbers.
