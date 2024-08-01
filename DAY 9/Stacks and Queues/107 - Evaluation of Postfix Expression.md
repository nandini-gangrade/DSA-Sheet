# [Evaluation of Postfix Expression](https://www.geeksforgeeks.org/problems/evaluation-of-postfix-expression1735/1)

Given a string `S` representing a postfix expression, evaluate the expression and return the final value. The operators in the expression include basic arithmetic operators: `+`, `-`, `*`, and `/`.

### Example

- **Input**: `S = "231*+9-"`
- **Output**: `-4`
- **Explanation**: After solving the given expression:
  - `2` and `3` are operands, `1` is another operand.
  - `3 * 1 = 3`, resulting in stack `[2, 3]`.
  - `2 + 3 = 5`, resulting in stack `[5]`.
  - `5 - 9 = -4`.

## Intuition

The postfix expression, also known as Reverse Polish Notation (RPN), is a mathematical notation in which operators follow their operands. The main advantage is that it doesn't need any parentheses as long as each operator has a fixed number of operands. The order of operations is determined by the position of operators and operands.

## Approach

1. **Use a Stack**: The core idea is to use a stack data structure to evaluate the postfix expression.
  
2. **Traverse the Expression**:
   - For each character in the string:
     - If it is an operand (number), push it onto the stack.
     - If it is an operator, pop the required number of operands from the stack, perform the operation, and push the result back onto the stack.

3. **Perform Operations**:
   - For binary operators like `+`, `-`, `*`, and `/`, pop two operands, apply the operator, and push the result back.
   - Since the stack is Last In First Out (LIFO), ensure the order of operations is correct (pop the second operand first, then the first).

4. **Return Result**: After processing all characters, the stack should have one element, which is the result of the expression.

## Code

```python
class Solution:
    
    # Function to evaluate a postfix expression.
    def evaluatePostfix(self, S):
        # Stack to hold the operands
        stack = []

        # Iterate over each character in the postfix expression
        for char in S:
            # If the character is an operand (0-9), push it to the stack
            if char.isdigit():
                stack.append(int(char))
            else:
                # Pop the top two operands from the stack for the operation
                # Note: second operand should be popped before first operand because it's a stack
                first = stack.pop()
                second = stack.pop()
                
                # Perform the operation based on the operator
                if char == '+':
                    stack.append(second + first)
                elif char == '-':
                    stack.append(second - first)
                elif char == '*':
                    stack.append(second * first)
                elif char == '/':
                    # Use integer division for consistency
                    stack.append(second // first)

        # The final result will be the only remaining element in the stack
        return stack[-1]

# Example usage:
solution = Solution()
print(solution.evaluatePostfix("231*+9-"))  # Output: -4
print(solution.evaluatePostfix("123+*8-")) # Output: -3
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the postfix expression. We process each character exactly once.
  
- **Space Complexity**: \(O(n)\), where \(n\) is the length of the postfix expression. In the worst case, the stack might need to store all operands before an operator appears.
