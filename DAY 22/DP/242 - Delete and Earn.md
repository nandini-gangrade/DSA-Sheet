# [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/description/)

The problem you're dealing with is a variation of the classic "House Robber" problem, where you cannot take adjacent elements because they interfere with one another (like in the case of `nums[i]` deleting `nums[i] - 1` and `nums[i] + 1`). Here's how we can approach it:

### Approach:

1. **Create a Frequency Array**:
   - We can simplify the problem by converting it into a frequency problem. Instead of working with scattered numbers, we first create an array that represents how many points we can earn by choosing each number. For example, if `nums = [2, 2, 3, 3, 3, 4]`, we could transform it into a points array where the index represents the number, and the value at that index is the total points we can earn by choosing that number (i.e., `points[2] = 4` because there are two `2`s, and `points[3] = 9` because there are three `3`s, and so on).

2. **Dynamic Programming**:
   - Once we have this points array, the problem reduces to the "House Robber" problem: at each step, you can either:
     - Skip the current element (because you "deleted" a neighbor).
     - Take the current element (and thus delete its neighbors).
   - We can use a dynamic programming approach to calculate the maximum points:
     - Let `dp[i]` represent the maximum points we can earn considering elements up to number `i`.
     - The relation is: 
       ```
       dp[i] = max(dp[i-1], dp[i-2] + points[i])
       ```
     - This means at any number `i`, you either skip it (`dp[i-1]`) or take it and add the points of `i` plus `dp[i-2]` (because choosing `i` deletes `i-1`).

### Algorithm:

1. Create a frequency array `points` where `points[i]` stores the total points you can earn by deleting all occurrences of `i` in `nums`.
2. Use dynamic programming to find the maximum points.

### Code Implementation:

```python
class Solution:
    def deleteAndEarn(self, nums: List[int]) -> int:
        # Edge case: if nums is empty
        if not nums:
            return 0
        
        # Step 1: Create a frequency array
        max_num = max(nums)
        points = [0] * (max_num + 1)
        
        # Fill the points array
        for num in nums:
            points[num] += num
        
        # Step 2: Dynamic programming
        # dp[i] represents the maximum points we can earn by considering numbers up to i
        take, skip = 0, 0
        
        for i in range(max_num + 1):
            take_i = skip + points[i]  # If we take 'i', we add its points and skip the previous one
            skip_i = max(skip, take)   # If we skip 'i', we take the best of previous skip or take
            
            take, skip = take_i, skip_i
        
        return max(take, skip)

```

### Explanation:

1. **Edge Case Handling**: We first check if `nums` is empty. If it is, return 0 since no points can be earned.
   
2. **Points Array Creation**:
   - We determine the maximum value in `nums` (let's call it `max_num`) to create an array `points` of size `max_num + 1`. This array will store the total points we can earn by choosing each number in `nums`.

3. **Dynamic Programming Transition**:
   - `take`: Represents the maximum points we can earn if we take the current number `i`.
   - `skip`: Represents the maximum points we can earn if we skip the current number `i`.
   - At each step, we update `take` and `skip` by considering the two possible choices:
     - If we take `i`, we add the points for `i` to the previous `skip` value (since we cannot take `i-1`).
     - If we skip `i`, we take the maximum of the previous `take` and `skip`.

4. **Result**:
   - The answer is the maximum of the last `take` or `skip`, as that represents the best result we can achieve by either taking or skipping the last number.

### Time and Space Complexity:

- **Time Complexity**: O(n + m), where `n` is the length of `nums` and `m` is the maximum number in `nums` (since we create an array up to the maximum value in `nums` and process it in linear time).
- **Space Complexity**: O(m), where `m` is the maximum number in `nums`, as we need the `points` array of size `m + 1`.

### Example Walkthrough:

1. **Example 1**:
   - Input: `nums = [3, 4, 2]`
   - Points array: `[0, 0, 2, 3, 4]` (i.e., 2 points for number 2, 3 points for 3, and 4 points for 4).
   - Dynamic programming steps:
     - `take = 0, skip = 0` initially.
     - For `i = 2`: `take_i = skip + points[2] = 0 + 2 = 2`, `skip_i = max(take, skip) = max(0, 0) = 0`. Update: `take = 2, skip = 0`.
     - For `i = 3`: `take_i = skip + points[3] = 0 + 3 = 3`, `skip_i = max(take, skip) = max(2, 0) = 2`. Update: `take = 3, skip = 2`.
     - For `i = 4`: `take_i = skip + points[4] = 2 + 4 = 6`, `skip_i = max(take, skip) = max(3, 2) = 3`. Update: `take = 6, skip = 3`.
   - Final result: `max(take, skip) = max(6, 3) = 6`.

2. **Example 2**:
   - Input: `nums = [2, 2, 3, 3, 3, 4]`
   - Points array: `[0, 0, 4, 9, 4]`.
   - Dynamic programming steps:
     - For `i = 2`: `take = 4, skip = 0`.
     - For `i = 3`: `take = 9, skip = 4`.
     - For `i = 4`: `take = 8, skip = 9`.
   - Final result: `max(take, skip) = max(9, 8) = 9`.

This solution efficiently handles large inputs and ensures maximum points are earned.
