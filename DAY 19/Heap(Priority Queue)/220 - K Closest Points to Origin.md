# [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/)

### Problem Explanation

You are given a list of points in a 2D plane, and you need to find the `k` closest points to the origin `(0, 0)`. The Euclidean distance formula will be used to determine the distance of each point from the origin. The task is to return the `k` closest points. The result does not need to be in any specific order, just that the `k` closest points are returned.

### Approach & Intuition

**Steps:**

1. **Calculate the Euclidean Distance:**
   - For each point `(x, y)`, calculate the squared Euclidean distance from the origin. The squared distance can be calculated as \( x^2 + y^2 \) (note that we can skip taking the square root because we only need to compare distances, not the actual distance values).
   
2. **Heap Data Structure:**
   - Use a max-heap (priority queue) to keep track of the `k` closest points. A max-heap ensures that the point with the largest distance (among the `k` closest) is at the root of the heap.
   - If the heap size exceeds `k`, remove the farthest point (i.e., the root of the heap) to maintain only the closest `k` points.
   
3. **Heap Maintenance:**
   - Iterate through all points, calculating the distance and pushing each point into the heap. If the heap exceeds size `k`, remove the maximum element (which is the farthest point) to maintain the closest points.

4. **Extract the Points:**
   - After processing all the points, the heap will contain the `k` closest points.

### Code Implementation

```python
import heapq

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        # Max-heap to store the k closest points with respect to distance
        max_heap = []
        
        for x, y in points:
            distance = -(x*x + y*y)  # Negative distance to maintain a max-heap
            if len(max_heap) < k:
                heapq.heappush(max_heap, (distance, [x, y]))
            else:
                heapq.heappushpop(max_heap, (distance, [x, y]))
        
        return [point for (_, point) in max_heap]
```

### Complexity Analysis

- **Time Complexity:** 
  - Building the heap of size `k` takes **O(k)**.
  - For each of the remaining `(n - k)` points, we push the point into the heap and pop the farthest point. Each push and pop operation takes **O(log k)**.
  - Hence, the overall time complexity is **O(n log k)** where `n` is the number of points.

- **Space Complexity:**
  - The space complexity is **O(k)** since we only store `k` points in the heap.

### Example Explanation

- **Example 1:**
  - Input: `points = [[1,3],[-2,2]], k = 1`
  - Output: `[[-2, 2]]`
  - Explanation: The distance of (1,3) from origin is `√10`, and for (-2,2) it is `√8`. Since `√8 < √10`, the point `(-2,2)` is closer to the origin and is the correct output.

- **Example 2:**
  - Input: `points = [[3,3],[5,-1],[-2,4]], k = 2`
  - Output: `[[3,3], [-2,4]]`
  - Explanation: The two closest points are `[-2,4]` and `[3,3]` based on their distances from the origin.

This solution efficiently finds the `k` closest points by leveraging a max-heap, ensuring that we handle potentially large inputs within the time and space constraints provided.
