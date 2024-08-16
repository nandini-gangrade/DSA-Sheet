# [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/description/)

The problem of bursting balloons can be solved using dynamic programming (DP). The challenge here is that when a balloon is burst, it affects the adjacent balloons, so we must carefully decide the order of balloon bursting to maximize the coins we collect.

### Key Observations:

1. **Out of Bounds Consideration**: If a balloon is at the boundary (first or last), we treat the out-of-bounds elements as having a value of 1. This is because if a balloon doesn't have a left or right neighbor, it is considered to be surrounded by `1`.

2. **Effect of Bursting a Balloon**: When a balloon `i` is burst, its neighboring balloons `i-1` and `i+1` affect the result. After `i` is burst, the balloons `i-1` and `i+1` become adjacent, so their product with `i` will give the coin value for that step.

### Approach:

The problem is a variant of an interval DP problem, where we divide the problem into subproblems by considering every possible balloon as the last one to be burst in its interval. The key is to think in reverse: instead of bursting the balloons in a given order, we imagine picking the last balloon to burst in each subarray.

### Plan:

1. **Dynamic Programming Table**: 
   - Let `dp[i][j]` represent the maximum coins we can collect by bursting balloons between indices `i` and `j` (inclusive). We will gradually compute the value of this table for all subarrays of `nums`.

2. **Extended Array**: 
   - We extend the `nums` array by adding 1 at both ends. This simplifies boundary conditions as we don’t have to handle out-of-bound cases separately.

3. **Recurrence Relation**:
   - For each subarray from index `i` to `j`, the goal is to choose a balloon `k` (where `i <= k <= j`) as the last balloon to burst. The coins we collect from this operation would be `nums[i-1] * nums[k] * nums[j+1]` plus the coins from bursting balloons in the subarrays before and after `k`.

   - So the recurrence relation becomes:
     \[
     dp[i][j] = \max(dp[i][j], dp[i][k-1] + dp[k+1][j] + nums[i-1] \times nums[k] \times nums[j+1])
     \]
     where `k` is the balloon we are choosing to burst last in the subarray `[i, j]`.

4. **Base Case**:
   - For a single balloon, `dp[i][i] = nums[i-1] * nums[i] * nums[i+1]` since there's only one balloon to burst.

### Algorithm:

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        # Add 1 to the start and end of the nums array to handle boundaries
        nums = [1] + nums + [1]
        n = len(nums)
        
        # DP table initialized to 0
        dp = [[0] * n for _ in range(n)]
        
        # Iterate over subarray lengths
        for length in range(1, n - 1):  # length of the window (subarray)
            for left in range(1, n - length):  # left boundary of the window
                right = left + length - 1  # right boundary of the window
                
                # Calculate the maximum coins for bursting all balloons in the subarray nums[left:right]
                for k in range(left, right + 1):
                    dp[left][right] = max(
                        dp[left][right],
                        dp[left][k - 1] + dp[k + 1][right] + nums[left - 1] * nums[k] * nums[right + 1]
                    )
        
        # The answer for bursting all balloons in the original array
        return dp[1][n - 2]
```

### Explanation:

1. **Extended Array**:
   - The `nums` array is extended to have a 1 at both the beginning and the end, so we work with indices from 1 to `n-2`. This avoids boundary checks while calculating coins.

2. **Dynamic Programming Table**:
   - `dp[i][j]` stores the maximum coins we can collect by bursting balloons in the subarray `nums[i:j]`. We gradually compute this value for increasing subarray lengths.

3. **Iterating over Subarrays**:
   - For each subarray of length `l`, we consider every balloon `k` within that subarray as the last balloon to be burst and compute the maximum coins by splitting the subarray into two parts: the part before `k` and the part after `k`.

4. **Result**:
   - The final result is found in `dp[1][n-2]`, which represents bursting all balloons in the original `nums` array.

### Time Complexity:
- The time complexity is \(O(n^3)\), where \(n\) is the length of the extended `nums` array (which is the original length plus 2). This is because we iterate over all subarrays, and for each subarray, we check every balloon within that subarray.

### Example Walkthrough:

For the input `nums = [3,1,5,8]`:

- We extend `nums` to `[1,3,1,5,8,1]`.
- The dynamic programming table `dp` is filled for subarrays of increasing lengths.
- The optimal burst sequence yields a maximum coin collection of 167.

### Example:

```python
nums = [3,1,5,8]
solution = Solution()
print(solution.maxCoins(nums))  # Output: 167
```

### Explanation of Example:

- We start with `nums = [3,1,5,8]`.
- After bursting balloons optimally, we collect coins as follows:
  - Burst balloon at index 1: coins = `3*1*5 = 15`
  - Burst balloon at index 3: coins = `3*5*8 = 120`
  - Burst balloon at index 0: coins = `1*3*8 = 24`
  - Burst balloon at index 2: coins = `1*8*1 = 8`
- The total is `15 + 120 + 24 + 8 = 167`.

Thus, the result is 167.
