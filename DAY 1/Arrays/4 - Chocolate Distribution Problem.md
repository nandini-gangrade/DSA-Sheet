# [Chocolate Distribution Problem](https://www.geeksforgeeks.org/problems/chocolate-distribution-problem3825/1)
[GFG Solution 👈](https://discuss.geeksforgeeks.org/comment/d0ca575e-1df7-4b5e-96cb-55941a171e06/practice)

Given an array `A[]` of positive integers of size `N`, where each value represents the number of chocolates in a packet, the goal is to distribute chocolate packets among `M` students such that:
1. Each student gets exactly one packet.
2. The difference between the maximum number of chocolates given to a student and the minimum number of chocolates given to a student is minimized.

### Examples

**Example 1:**

- **Input:**  
  `N = 8`, `M = 5`  
  `A = [3, 4, 1, 9, 56, 7, 9, 12]`
  
- **Output:**  
  `6`

- **Explanation:**  
  The minimum difference between maximum chocolates and minimum chocolates is `9 - 3 = 6` by choosing the following `M` packets: `{3, 4, 9, 7, 9}`.

**Example 2:**

- **Input:**  
  `N = 7`, `M = 3`  
  `A = [7, 3, 2, 4, 9, 12, 56]`

- **Output:**  
  `2`

- **Explanation:**  
  The minimum difference between maximum chocolates and minimum chocolates is `4 - 2 = 2` by choosing the following `M` packets: `{3, 2, 4}`.

## Intuition

To minimize the difference between the maximum and minimum chocolates distributed, we can take advantage of sorting. By sorting the array, we can consider subarrays of size `M` to find the optimal distribution. The idea is that the optimal set of packets is likely to be grouped together after sorting, allowing us to efficiently compute the minimum difference.

## Approach

1. **Sort the Array:**
   - First, sort the array `A[]`. This allows us to evaluate contiguous subarrays of size `M`.

2. **Sliding Window to Find Minimum Difference:**
   - Initialize a variable `min_diff` to a very large number (e.g., `infinity`) to store the minimum difference found.
   - Iterate over the sorted array with a window of size `M`:
     - For each subarray of size `M`, calculate the difference between the maximum and minimum elements (`A[i+M-1] - A[i]`).
     - Update `min_diff` with the minimum difference found.

3. **Return Result:**
   - After iterating through all possible subarrays, `min_diff` will contain the minimum difference.

## Code

```python
class Solution:
    def findMinDiff(self, A, N, M):
        # Sort the array
        A.sort()
        
        # Initialize min_diff to a large value
        min_diff = float('inf')
        
        # Traverse the array with a window of size M
        for i in range(N - M + 1):
            # Calculate the difference between the current window's max and min
            diff = A[i + M - 1] - A[i]
            
            # Update min_diff if we found a smaller difference
            if diff < min_diff:
                min_diff = diff
        
        # Return the minimum difference found
        return min_diff
```

## Complexity Analysis

- **Time Complexity:** O(N log N)  
  The primary time-consuming operation is sorting the array, which takes O(N log N). The subsequent iteration through the array takes O(N).

- **Space Complexity:** O(1)  
  The algorithm uses a constant amount of extra space, as it only needs a few variables for calculations and does not use any additional data structures.

This approach efficiently finds the minimum difference by leveraging the properties of sorted arrays and sliding window techniques. By examining only the necessary windows, we minimize computational overhead and achieve the desired result within optimal time complexity.


---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [GFG](https://discuss.geeksforgeeks.org/comment/d0ca575e-1df7-4b5e-96cb-55941a171e06/practice) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
