# [Word Wrap](https://www.geeksforgeeks.org/problems/word-wrap1646/1)
[GFG Solution](https://discuss.geeksforgeeks.org/comment/ea64e30a-90f0-4a3b-a053-7c9419a86dde/practice)

Given an array of integers representing the lengths of words and an integer `k` representing the maximum number of characters that can fit in one line, the task is to minimize the total cost of line breaks. The cost of a line is defined as the square of the number of extra spaces in that line. The goal is to return the minimum total cost after optimal line wrapping.

## Intuition

1. **Word Wrapping**: Words need to be arranged in lines such that the total length of words on each line, including spaces between words, does not exceed the limit `k`.

2. **Cost Calculation**: The cost for a line is the square of the number of extra spaces left after placing words in that line. To minimize the total cost, we need to distribute words across lines in such a way that this cost is minimized for all lines.

3. **Dynamic Programming Approach**: 
   - Use dynamic programming to store the minimum cost for wrapping words starting from each index in the array. 
   - Use recursion to explore all possible ways of breaking lines and memoize the results to avoid redundant calculations.

## Approach

1. **Define States**: Use a `dp` array where `dp[i]` represents the minimum cost of wrapping words starting from index `i`.

2. **Recursive Function**: Implement a recursive function that:
   - Computes the total length of words on the current line.
   - Calculates the cost if words from the current index `i` to `j` are placed on the current line.
   - Recursively computes the cost for the remaining words and combines it with the current line's cost.

3. **Base Case**: If the end of the array is reached, return `0` because there are no more words to process.

4. **Memoization**: Store the results of subproblems to avoid redundant calculations and speed up the solution.

## Code

```python
class Solution:
    def __init__(self):
        self.dp = [-1] * 501  # Initialize dp array with -1 for memoization
    
    def f(self, idx, k, nums):
        if idx >= len(nums):
            return 0
        
        if self.dp[idx] != -1:
            return self.dp[idx]
        
        sum_length = 0
        min_cost = float('inf')
        
        for i in range(idx, len(nums)):
            sum_length += nums[i]
            
            if k - sum_length >= 0 and i == len(nums) - 1:
                return 0
            elif i == len(nums) - 1:
                return min_cost
            
            if k - sum_length >= 0:
                cost = (k - sum_length) ** 2 + self.f(i + 1, k, nums)
                min_cost = min(min_cost, cost)
            else:
                break
            
            sum_length += 1
        
        self.dp[idx] = min_cost
        return min_cost
    
    def solveWordWrap(self, nums, k):
        return self.f(0, k, nums)

# Example usage
sol = Solution()
print(sol.solveWordWrap([3, 2, 2, 5], 6))  # Output: 10
print(sol.solveWordWrap([3, 2, 2], 4))    # Output: 5
```

## Complexity

- **Time Complexity**: \(O(n^2)\)
  - In the worst case, the algorithm processes each pair of indices \((i, j)\) in the `nums` array, leading to a quadratic time complexity.
  
- **Space Complexity**: \(O(n)\)
  - The space complexity is primarily due to the `dp` array used for memoization and the recursion stack.

This solution efficiently computes the minimal cost for word wrapping using dynamic programming and recursion with memoization.
