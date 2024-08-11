# [778. Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/description/)

To solve the problem of finding the least time until you can swim from the top-left to the bottom-right of the matrix given the elevation constraints, you can use a combination of Dijkstra's algorithm and a priority queue. The problem is essentially about finding the shortest path in a weighted grid where weights are the elevation values, and you can swim between cells as long as their elevation is below or equal to the current time `t`.

### Approach

1. **Use Dijkstra's Algorithm:**
   - Treat the problem as finding the shortest path on a weighted grid, where the weight of moving into a cell is defined by the elevation value at that cell.

2. **Priority Queue:**
   - Utilize a min-heap (priority queue) to always expand the least-cost cell first. This allows you to efficiently find the minimum time required to reach the target cell.

3. **Initialize the Queue:**
   - Start from the top-left corner `(0, 0)` with an initial time equal to the elevation at that cell.

4. **Expand Cells:**
   - For each cell, attempt to move to its adjacent cells. Only move to cells if the elevation of both cells is less than or equal to the current time `t`.

5. **Track Minimum Time:**
   - Continue expanding cells and updating the minimum time required to reach each cell until you reach the bottom-right corner `(n-1, n-1)`.

### Implementation

Here's the Python code implementing the above approach:

```python
import heapq
from typing import List

class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        n = len(grid)
        # Directions for moving in 4 possible ways: right, down, left, up
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        
        # Priority queue with (time, x, y) tuples
        pq = [(grid[0][0], 0, 0)]
        # Matrix to track the minimum time to reach each cell
        min_time = [[float('inf')] * n for _ in range(n)]
        min_time[0][0] = grid[0][0]
        
        while pq:
            current_time, x, y = heapq.heappop(pq)
            
            # If we reached the bottom-right corner, return the time
            if x == n - 1 and y == n - 1:
                return current_time
            
            # Explore neighbors
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    next_time = max(current_time, grid[nx][ny])
                    if next_time < min_time[nx][ny]:
                        min_time[nx][ny] = next_time
                        heapq.heappush(pq, (next_time, nx, ny))
        
        return -1  # If unreachable, though per constraints, it should be reachable
```

### Explanation

1. **Priority Queue Initialization:**
   - Start with the top-left corner of the grid and initialize the priority queue with the elevation value at that cell.

2. **Processing Cells:**
   - Extract the cell with the smallest time value from the priority queue. For each cell, explore its neighbors and update their minimum time required to reach them.

3. **Neighbor Exploration:**
   - For each neighbor, calculate the time needed to reach it as the maximum of the current time and the neighbor's elevation. Push this updated time into the priority queue if it's better than previously recorded times.

4. **Termination:**
   - The process terminates when you extract the bottom-right corner cell from the priority queue, and the corresponding time is the answer.

### Complexity

- **Time Complexity:** \(O(n^2 \log n)\), where \(n\) is the size of the grid. Each cell is processed once, and operations with the priority queue are logarithmic with respect to the number of cells.
- **Space Complexity:** \(O(n^2)\), due to the storage required for the `min_time` matrix and the priority queue.

This approach efficiently finds the minimum time needed to reach the target cell given the constraints of the problem.
