# [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/description/)
[LeetCode Solution](https://leetcode.com/problems/subarray-sum-equals-k/solutions/5535865/step-by-step-explanation-challenge-day-3-revisewitharsh)

Given an array of integers `nums` and an integer `k`, return the total number of contiguous subarrays whose sum equals `k`.

### Examples

**Example 1:**

- **Input:** `nums = [1,1,1]`, `k = 2`
- **Output:** `2`
- **Explanation:** There are two subarrays that sum up to `2`: `[1,1]` and `[1,1]`.

**Example 2:**

- **Input:** `nums = [1,2,3]`, `k = 3`
- **Output:** `2`
- **Explanation:** There are two subarrays that sum up to `3`: `[1,2]` and `[3]`.


## Intuition

To efficiently find the number of subarrays with a sum equal to `k`, we can use the concept of prefix sums along with a hash map to keep track of the counts of prefix sums we have seen so far.

## Approach

1. **Prefix Sum Calculation:** Compute the prefix sum for each element in the array. The prefix sum up to index `i` is the sum of all elements from the start of the array up to `i`.

2. **Hash Map for Prefix Sums:** Use a hash map to store the frequency of each prefix sum encountered. This helps in quickly checking how many times a particular prefix sum has occurred.

3. **Determine Subarrays:** For each prefix sum, calculate the required prefix sum that would result in a subarray sum equal to `k`. If this required prefix sum exists in the hash map, add its count to the result.

### Detailed Steps

1. Initialize a hash map to keep track of the frequency of prefix sums, starting with `{0: 1}` to handle the case where a prefix sum exactly equals `k`.

2. Iterate through the `nums` array, maintaining a running `current_sum` which is the prefix sum up to the current index.

3. For each `current_sum`, check if `current_sum - k` exists in the hash map. If it does, it means there are subarrays that end at the current index and sum up to `k`.

4. Update the hash map with the current prefix sum.

5. Return the total count of subarrays that sum up to `k`.

## Code

```python []
from collections import defaultdict

class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefix_sum_count = defaultdict(int)
        prefix_sum_count[0] = 1  # Initialize with 0 prefix sum count for the base case
        current_sum = 0
        count = 0
        
        for num in nums:
            current_sum += num
            if (current_sum - k) in prefix_sum_count:
                count += prefix_sum_count[current_sum - k]
            prefix_sum_count[current_sum] += 1
        
        return count
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\), where \(n\) is the length of the `nums` array. We process each element of the array once and perform constant time operations for each element.
- **Space Complexity:** \(O(n)\), where \(n\) is the length of the `nums` array. The hash map stores up to `n` prefix sums.

This approach efficiently finds the number of subarrays with a sum equal to `k` using prefix sums and a hash map, ensuring a linear time complexity suitable for large inputs.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
