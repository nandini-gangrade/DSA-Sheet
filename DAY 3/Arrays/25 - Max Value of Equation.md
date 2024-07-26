# [1499. Max Value of Equation](https://leetcode.com/problems/max-value-of-equation/description/)
[LeetCode Solution](https://leetcode.com/problems/max-value-of-equation/solutions/5540158/best-solution-challenge-day-3-revisewitharsh)

You are given an array `points` containing coordinates of points on a 2D plane, sorted by the x-values. Each point is represented as `[xi, yi]` where `xi < xj` for all `1 <= i < j <= points.length`. You are also given an integer `k`.

You need to find the maximum value of the equation `yi + yj + |xi - xj|` for all pairs of points `(i, j)` such that `|xi - xj| <= k` and `1 <= i < j <= points.length`.

## Intuition

To solve this problem efficiently, you need to:
1. **Leverage the Sorted Order:** The `points` array is sorted by x-values, which helps us maintain a sequential check of pairs while efficiently managing conditions on the x-values.
2. **Use a Data Structure to Maintain Candidates:** A deque (double-ended queue) helps us efficiently manage and retrieve the maximum value of `yi - xi` while iterating through points.

## Approach

1. **Initialize Data Structures:** Use a deque to keep track of the indices of points. The deque will store indices of points in such a way that it helps us efficiently check and update the maximum value of the equation.
2. **Iterate Through Points:**
   - **Remove Out-of-Range Points:** Ensure that the x-values of the points in the deque satisfy the condition `|xi - xj| <= k`. Remove any point from the front of the deque that does not meet this condition.
   - **Calculate and Update Result:** For the current point, if there are valid points in the deque, calculate the value of the equation using the point at the front of the deque. Update the result if this value is greater than the current maximum.
   - **Maintain Deque Order:** Maintain the deque in such a way that it is always ordered by `yi - xi` in decreasing order. Remove points from the back of the deque if they do not help in maximizing the equation for the current point.
   - **Add Current Point:** Add the current point to the deque.

3. **Return the Maximum Value:** After iterating through all points, the result will be the maximum value of the equation found.

## Code

```python []
from collections import deque
from typing import List

class Solution:
    def findMaxValueOfEquation(self, points: List[List[int]], k: int) -> int:
        # Initialize the result to a very small number
        max_value = float('-inf')
        
        # Deque to store the indices of points
        d = deque()
        
        for j in range(len(points)):
            # Remove indices from the deque where x-values are out of range
            while d and points[j][0] - points[d[0]][0] > k:
                d.popleft()
                
            # If deque is not empty, calculate the potential maximum value
            if d:
                max_value = max(max_value, points[d[0]][1] - points[d[0]][0] + points[j][1] + points[j][0])
                
            # Maintain deque to ensure it is ordered by yi - xi
            while d and points[d[-1]][1] - points[d[-1]][0] < points[j][1] - points[j][0]:
                d.pop()
                
            # Add the current index to the deque
            d.append(j)
        
        return max_value
```

## Complexity

- **Time Complexity:** \(O(n)\), where \(n\) is the number of points. Each point is added and removed from the deque at most once.
- **Space Complexity:** \(O(n)\), due to the space used by the deque to store indices.

This approach efficiently computes the maximum value of the equation while respecting the constraint on the x-values using a sliding window mechanism facilitated by a deque.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
