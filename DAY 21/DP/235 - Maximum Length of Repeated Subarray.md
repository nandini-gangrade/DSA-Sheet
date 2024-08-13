# [718. Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/)

To solve the problem of finding the maximum length of a subarray that appears in both `nums1` and `nums2`, we can use dynamic programming (DP). Here's a detailed approach to solve this problem:

### Approach:

1. **Dynamic Programming Table**:
   - We'll use a 2D DP array `dp` where `dp[i][j]` represents the length of the longest common subarray ending at `nums1[i-1]` and `nums2[j-1]`.
   - If `nums1[i-1] == nums2[j-1]`, then `dp[i][j] = dp[i-1][j-1] + 1`.
   - If they are not equal, `dp[i][j] = 0`.

2. **Initialization**:
   - The DP table is initialized with zeros, representing no common subarrays found initially.
   - We also maintain a variable `max_length` to track the maximum length of any common subarray found during the computation.

3. **Filling the DP Table**:
   - Iterate through both arrays and fill in the DP table using the above relation.
   - Update `max_length` whenever a longer common subarray is found.

4. **Result**:
   - After filling the DP table, `max_length` will hold the length of the longest common subarray.

### Code Implementation:

```python
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        m, n = len(nums1), len(nums2)
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        max_length = 0
        
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if nums1[i - 1] == nums2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                    max_length = max(max_length, dp[i][j])
        
        return max_length
```

### Example Explanations:

1. **Example 1**:
   - Input: `nums1 = [1,2,3,2,1]`, `nums2 = [3,2,1,4,7]`
   - The longest common subarray is `[3,2,1]`, which has a length of 3.
   - Output: `3`

2. **Example 2**:
   - Input: `nums1 = [0,0,0,0,0]`, `nums2 = [0,0,0,0,0]`
   - The entire arrays are identical, so the longest common subarray is `[0,0,0,0,0]`, which has a length of 5.
   - Output: `5`

### Complexity Analysis:

- **Time Complexity**: O(m * n), where `m` is the length of `nums1` and `n` is the length of `nums2`. We are filling out a DP table of size `m x n`.
- **Space Complexity**: O(m * n), for storing the DP table.

This approach efficiently finds the longest common subarray in two integer arrays using dynamic programming.
