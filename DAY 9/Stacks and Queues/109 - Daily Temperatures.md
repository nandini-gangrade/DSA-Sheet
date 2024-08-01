# [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)

Given an array of integers `temperatures`, where each integer represents the temperature of a day, return an array `answer` such that for each day `i`, `answer[i]` contains the number of days until a warmer temperature occurs. If no warmer day exists, `answer[i]` should be `0`.

## Intuition

The problem requires looking ahead in the array to find when the next warmer temperature occurs. A straightforward approach would involve a nested loop checking each day after day `i` for a warmer temperature, but this would result in a time complexity of \(O(n^2)\), which is inefficient for large inputs.

## Approach

We can solve this problem efficiently using a monotonic stack. The stack will store indices of the temperatures, and we will ensure that the temperatures represented by these indices are always in a decreasing order. This allows us to efficiently determine when a warmer temperature is found.

1. **Initialize a Result Array**: Create an array `answer` of the same length as `temperatures`, initialized to zero. This will store the number of days to wait for each day.

2. **Use a Stack**: Use a stack to keep track of the indices of the temperatures in a decreasing order.

3. **Iterate Through Temperatures**: For each temperature:
   - While the stack is not empty and the current temperature is greater than the temperature at the index stored at the top of the stack:
     - Pop the top of the stack and calculate the number of days between the current index and the popped index. Update the `answer` for the popped index.
   - Push the current index onto the stack.

4. **Return Result**: The stack will ensure that each index is only processed once, making this approach efficient.

## Code Implementation

```python
class Solution:
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        n = len(temperatures)
        answer = [0] * n  # Initialize answer array with zeros
        stack = []  # Stack to hold indices of temperatures

        for i in range(n):
            # While stack is not empty and the current temperature is greater than
            # the temperature at the index stored at the top of the stack
            while stack and temperatures[i] > temperatures[stack[-1]]:
                prev_index = stack.pop()
                answer[prev_index] = i - prev_index  # Calculate days waited
            stack.append(i)  # Push current index onto the stack

        return answer
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of days. Each temperature is pushed and popped from the stack at most once.
- **Space Complexity**: \(O(n)\), for storing the stack and the answer array.

This approach ensures that we efficiently compute the number of days to wait for each day using a single pass through the `temperatures` array, making it optimal for large input sizes.
