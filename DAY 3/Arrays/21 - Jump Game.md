# [55. Jump Game](https://leetcode.com/problems/jump-game/description/)
[LeetCode Solution](https://leetcode.com/problems/jump-game/solutions/5539964/step-by-step-explanation-challenge-day-3-revisewitharsh)

You are given an integer array `nums` where each element represents the maximum jump length you can make from that position. You start at the first index and aim to reach the last index. The task is to determine whether it is possible to reach the last index from the first index.

### Examples

1. **Example 1:**
   - **Input:** `nums = [2, 3, 1, 1, 4]`
   - **Output:** `True`
   - **Explanation:** You can jump 1 step from index 0 to 1, then 3 steps to the last index.

2. **Example 2:**
   - **Input:** `nums = [3, 2, 1, 0, 4]`
   - **Output:** `False`
   - **Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

### Constraints

- `1 <= nums.length <= 10^4`
- `0 <= nums[i] <= 10^5`

## Intuition

The key to solving this problem is to track the farthest point you can reach as you traverse the array. If at any point you find that your current position is beyond the farthest reachable point, you can't proceed further. Conversely, if you can reach or exceed the last index at any point, you can successfully reach the end.

## Approach

The approach uses a greedy algorithm to keep track of the maximum reachable index as you iterate through the array.

1. **Initialize `max_reach`:** Set it to 0 to indicate the farthest index you can reach from the start.

2. **Iterate over the array:**
   - For each index `i`, check if `i` is beyond `max_reach`. If it is, return `False` because you cannot move beyond this point.
   - Update `max_reach` as the maximum of its current value and `i + nums[i]` (the farthest you can reach from the current index).
   - If `max_reach` is greater than or equal to the last index, return `True` since you can reach the end.

3. **End of Loop:** If you complete the loop without returning `True`, it means you can reach the last index.

## Code

Here's the implementation in Python:

```python
from typing import List

class Solution:
    def canJump(self, nums: List[int]) -> bool:
        max_reach = 0  # Initialize the farthest index we can reach
        
        for i in range(len(nums)):
            if i > max_reach:
                # If the current index is beyond what we can reach, return False
                return False
            
            # Update the farthest index we can reach from this point
            max_reach = max(max_reach, i + nums[i])
            
            # If we can reach or go beyond the last index, return True
            if max_reach >= len(nums) - 1:
                return True
        
        # If we finish the loop, it means we can reach the last index
        return True
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\), where \(n\) is the length of `nums`. The algorithm iterates through the array once.
- **Space Complexity:** \(O(1)\), as we use only a constant amount of extra space to store the `max_reach` variable.

This greedy approach efficiently determines whether you can reach the last index by focusing on the maximum reach at each step and is optimal for the given constraints.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
