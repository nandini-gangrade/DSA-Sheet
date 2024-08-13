# [200. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

To solve the problem of finding the length of the longest strictly increasing subsequence (LIS) in an integer array `nums`, we can approach it using two methods:

1. **Dynamic Programming (O(n^2) approach)**:
   - This is the straightforward method, where we use dynamic programming to find the LIS.
   
2. **Binary Search + Dynamic Programming (O(n log n) approach)**:
   - This is a more optimized solution that uses a combination of dynamic programming and binary search to achieve a better time complexity.

### Approach 1: Dynamic Programming (O(n^2))

1. **DP Array**:
   - We maintain a DP array where `dp[i]` represents the length of the longest increasing subsequence that ends with `nums[i]`.
   - Initially, each element in the DP array is set to 1, because the smallest LIS ending with any element is the element itself.

2. **DP Update**:
   - For each element `nums[i]`, we check all previous elements `nums[j]` where `j < i`. If `nums[j] < nums[i]`, then `dp[i]` can be updated as `dp[i] = max(dp[i], dp[j] + 1)`.

3. **Result**:
   - The length of the longest increasing subsequence is the maximum value in the DP array.

### Implementation (O(n^2)):

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1] * n
        
        for i in range(1, n):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
        
        return max(dp)
```

### Approach 2: Binary Search + Dynamic Programming (O(n log n))

1. **Tail Array**:
   - We maintain an array `tails` where `tails[i]` represents the smallest ending element of any increasing subsequence of length `i+1`.

2. **Binary Search**:
   - For each element `nums[i]`, we use binary search to find its position in the `tails` array.
   - If `nums[i]` is larger than all elements in `tails`, append it.
   - If `nums[i]` can replace an element in `tails`, replace the first element that is greater than or equal to `nums[i]`.

3. **Result**:
   - The length of the `tails` array at the end represents the length of the longest increasing subsequence.

### Implementation (O(n log n)):

```python
import bisect

class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        tails = []
        
        for num in nums:
            index = bisect.bisect_left(tails, num)
            if index < len(tails):
                tails[index] = num
            else:
                tails.append(num)
        
        return len(tails)
```

### Example Explanations:

1. **Example 1**:
   - Input: `nums = [10,9,2,5,3,7,101,18]`
   - The LIS is `[2,3,7,101]`, so the output is `4`.

2. **Example 2**:
   - Input: `nums = [0,1,0,3,2,3]`
   - The LIS is `[0,1,2,3]`, so the output is `4`.

3. **Example 3**:
   - Input: `nums = [7,7,7,7,7,7,7]`
   - The LIS is `[7]` since all elements are the same, so the output is `1`.

### Complexity Analysis:

- **O(n^2) Approach**:
  - **Time Complexity**: O(n^2)
  - **Space Complexity**: O(n)
  
- **O(n log n) Approach**:
  - **Time Complexity**: O(n log n)
  - **Space Complexity**: O(n)

The binary search approach (`O(n log n)`) is optimal for larger input sizes and is the recommended solution when performance is a critical factor.
