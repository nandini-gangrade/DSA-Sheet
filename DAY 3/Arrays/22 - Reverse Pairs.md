# [493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/description/)
[LeetCode Solution](https://leetcode.com/problems/reverse-pairs/solutions/5539989/step-by-step-explanation-challenge-day-3-revisewitharsh)

You are given an integer array `nums`. The task is to find the number of reverse pairs in the array. A reverse pair is defined as a pair of indices `(i, j)` such that:

- `0 <= i < j < nums.length`
- `nums[i] > 2 * nums[j]`

### Examples

1. **Example 1:**
   - **Input:** `nums = [1, 3, 2, 3, 1]`
   - **Output:** `2`
   - **Explanation:** The reverse pairs are:
     - `(1, 4)` with `nums[1] = 3` and `nums[4] = 1`, since `3 > 2 * 1`.
     - `(3, 4)` with `nums[3] = 3` and `nums[4] = 1`, since `3 > 2 * 1`.

2. **Example 2:**
   - **Input:** `nums = [2, 4, 3, 5, 1]`
   - **Output:** `3`
   - **Explanation:** The reverse pairs are:
     - `(1, 4)` with `nums[1] = 4` and `nums[4] = 1`, since `4 > 2 * 1`.
     - `(2, 4)` with `nums[2] = 3` and `nums[4] = 1`, since `3 > 2 * 1`.
     - `(3, 4)` with `nums[3] = 5` and `nums[4] = 1`, since `5 > 2 * 1`.

### Constraints

- `1 <= nums.length <= 5 * 10^4`
- `-2^{31} <= nums[i] <= 2^{31} - 1`

## Intuition

The brute force approach of checking each pair `(i, j)` would result in an \(O(n^2)\) solution, which is inefficient for large arrays. Instead, a more efficient solution involves modifying the merge sort algorithm to count reverse pairs during the merge process.

## Approach

We will use a modified version of the merge sort algorithm. The main idea is to count reverse pairs during the merge process:

1. **Divide and Conquer:** Similar to merge sort, split the array into two halves and recursively sort and count reverse pairs in each half.

2. **Merge Process:** While merging two halves, count reverse pairs where an element in the left half satisfies the reverse pair condition with an element in the right half.

3. **Counting Reverse Pairs:** For each element in the left subarray, count how many elements in the right subarray satisfy the reverse pair condition. This can be done efficiently during the merge process.

4. **Merge and Count:** Combine the sorted halves and count the reverse pairs by comparing elements from the left and right halves.

## Code

Here is the implementation in Python:

```python
from typing import List

class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        def merge_sort_and_count(start, end):
            if start >= end:
                return 0
            
            mid = (start + end) // 2
            count = merge_sort_and_count(start, mid) + merge_sort_and_count(mid + 1, end)
            
            j = mid + 1
            for i in range(start, mid + 1):
                while j <= end and nums[i] > 2 * nums[j]:
                    j += 1
                count += j - (mid + 1)
            
            nums[start:end + 1] = sorted(nums[start:end + 1])
            return count
        
        return merge_sort_and_count(0, len(nums) - 1)
```

## Complexity Analysis

- **Time Complexity:** \(O(n \log n)\), where \(n\) is the length of the array. This is because the algorithm is based on merge sort, which has a time complexity of \(O(n \log n)\).
- **Space Complexity:** \(O(n)\) due to the additional space used during the merge process.

This approach efficiently counts reverse pairs by leveraging the properties of merge sort, reducing the time complexity significantly compared to a brute-force solution.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
