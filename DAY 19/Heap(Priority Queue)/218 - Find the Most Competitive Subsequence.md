# [1673. Find the Most Competitive Subsequence](https://leetcode.com/problems/find-the-most-competitive-subsequence/description/)

The problem requires finding the **most competitive subsequence** of length `k` from a given list of integers `nums`. A subsequence is derived by deleting some or no elements from the array without changing the order of the remaining elements. The subsequence should be lexicographically smallest among all possible subsequences of length `k`.

### Approach & Intuition

The key idea here is to maintain a **stack** to construct the most competitive subsequence. The stack will help keep track of the smallest elements while ensuring that the subsequence remains of the required length `k`.

**Step-by-Step Approach:**

1. **Initialization:**
   - Start with an empty stack that will hold the most competitive subsequence.

2. **Iterate Over Elements:**
   - Traverse the `nums` list while maintaining the stack.
   - For each element `num` at index `i`, compare it with the top of the stack (`stack[-1]`).

3. **Stack Adjustment:**
   - While the current element `num` is smaller than the top of the stack and there are enough elements left in `nums` to ensure that we can still make a subsequence of length `k`, remove the top element of the stack. This ensures the subsequence remains competitive.

4. **Adding to Stack:**
   - If the stack's size is less than `k`, append the current element to the stack.

5. **Final Output:**
   - After processing all elements, the stack will contain the most competitive subsequence of length `k`.

### Code Implementation

```python
class Solution:
    def mostCompetitive(self, nums: List[int], k: int) -> List[int]:
        # This list will hold the most competitive subsequence
        stack = []
        
        # Loop over the numbers with an index
        for i, num in enumerate(nums):
            # We want to maintain a stack that is always ordered and has length at most k
            while stack and stack[-1] > num and len(stack) - 1 + len(nums) - i >= k:
                stack.pop()
            if len(stack) < k:
                stack.append(num)
        
        return stack
```

### Complexity Analysis

- **Time Complexity:** 
  - The time complexity of this algorithm is **O(n)**, where `n` is the length of the `nums` array. This is because each element is pushed and popped from the stack at most once.

- **Space Complexity:**
  - The space complexity is **O(k)**, where `k` is the length of the required subsequence. This is because the stack will hold at most `k` elements.

### Intuition Behind the Approach

The intuition is based on greedy decision-making:
- By iterating through the array and maintaining a stack, you ensure that the smallest possible elements are kept for the final subsequence.
- The while loop allows us to discard larger elements if a smaller one can be included, making the subsequence more competitive.

This approach ensures that we efficiently build the smallest subsequence possible by leveraging the stack data structure's properties.
