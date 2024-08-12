# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

To solve the problem of finding the number of distinct ways to climb a staircase with `n` steps, where you can either take 1 step or 2 steps at a time, we can recognize that this problem is a classic example of the Fibonacci sequence.

### Approach

1. **Base Cases:**
   - If `n = 1`, there is only 1 way to climb the stairs (1 step).
   - If `n = 2`, there are 2 ways to climb the stairs (either 1+1 steps or 2 steps).

2. **Recursive Relationship:**
   - For any number of steps `n`, the number of ways to reach step `n` is the sum of the ways to reach step `n-1` (by taking a single step from `n-1` to `n`) and the ways to reach step `n-2` (by taking a double step from `n-2` to `n`).
   - This can be expressed as:
     \[
     \text{ways}(n) = \text{ways}(n-1) + \text{ways}(n-2)
     \]
   - This is similar to the Fibonacci sequence, where each term is the sum of the previous two terms.

3. **Iterative Solution:**
   - Instead of using recursion, which can lead to excessive function calls and increased time complexity, we use an iterative approach to build up the solution from the base cases.

### Implementation

Here's the Python code to implement this approach:

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # Base cases
        if n == 1:
            return 1
        if n == 2:
            return 2
        
        # Initialize the first two steps
        first = 1
        second = 2
        
        # Calculate the number of ways for each step from 3 to n
        for i in range(3, n + 1):
            current = first + second
            # Update the previous two steps
            first = second
            second = current
        
        return second
```

### Explanation

- **Initialization:**
  - `first` represents the number of ways to reach the first step.
  - `second` represents the number of ways to reach the second step.

- **Iterative Calculation:**
  - For each step from 3 to `n`, compute the number of ways to reach that step (`current`) as the sum of the ways to reach the previous two steps.
  - Update `first` and `second` to move up the staircase.

- **Final Result:**
  - After iterating through all the steps, `second` will contain the number of ways to reach the nth step.

### Complexity

- **Time Complexity:** O(n), since we calculate the number of ways for each step from 3 to n once.
- **Space Complexity:** O(1), since we only use a constant amount of extra space for the variables `first`, `second`, and `current`.

This approach efficiently computes the number of distinct ways to climb a staircase with `n` steps.
