# [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/)

To solve the problem of splitting an integer array `nums` into `k` non-empty subarrays such that the largest sum of any subarray is minimized, we can use a binary search combined with a greedy checking algorithm. Here’s a step-by-step approach:

## Approach

1. **Binary Search**:
   - The key is to determine the minimum possible value of the largest sum of subarrays when split into `k` parts. To find this, perform a binary search on the possible values of the largest sum.
   
2. **Greedy Check**:
   - For each candidate value of the largest sum (from the binary search), use a greedy approach to determine if it's possible to split the array into `k` or fewer subarrays where the sum of each subarray does not exceed this candidate value.

### Detailed Steps

1. **Binary Search Setup**:
   - The lower bound (`left`) of the search range is the maximum value in the array, because any valid partition must be at least as large as the largest element (otherwise, that element wouldn't fit in any subarray).
   - The upper bound (`right`) is the sum of all elements in the array, which is the scenario where the entire array is one subarray.

2. **Greedy Partition Check**:
   - For each midpoint value from the binary search, try to partition the array using a greedy approach:
     - Traverse the array and keep adding elements to the current subarray until adding another element would exceed the midpoint value.
     - Start a new subarray when this happens.
     - Count the number of subarrays required. If it's less than or equal to `k`, then the midpoint value is a feasible largest sum.

## Python Code

```python
class Solution:
    def splitArray(self, nums, k):
        def canSplit(max_sum):
            current_sum = 0
            required_subarrays = 1
            for num in nums:
                if current_sum + num > max_sum:
                    required_subarrays += 1
                    current_sum = num
                    if required_subarrays > k:
                        return False
                else:
                    current_sum += num
            return True
        
        left = max(nums)
        right = sum(nums)
        
        while left < right:
            mid = (left + right) // 2
            if canSplit(mid):
                right = mid
            else:
                left = mid + 1
        
        return left
```

### Explanation

1. **Binary Search**:
   - The function starts with `left` as the maximum value in the array and `right` as the total sum of the array.
   - The search narrows down the range to find the smallest possible maximum subarray sum that allows splitting the array into `k` subarrays.

2. **Greedy Check (`canSplit`)**:
   - Checks if it's possible to split the array into `k` or fewer subarrays such that no subarray sum exceeds the given `max_sum`.
   - This function iterates through the array and keeps track of the current sum of the subarray. If adding a new element exceeds the `max_sum`, it starts a new subarray and increments the count of required subarrays.

## Complexity

- **Time Complexity**: \(O(n \log S)\)
  - Where \(n\) is the number of elements in the array and \(S\) is the sum of all elements. The binary search takes \(O(\log S)\) and for each mid value, the greedy check takes \(O(n)\).

- **Space Complexity**: \(O(1)\)
  - Only a few extra variables are used, and the array itself is not modified.

This approach efficiently finds the minimum largest sum of any subarray by combining binary search with a greedy checking strategy.
