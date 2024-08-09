# [1162. As Far from Land as Possible](https://leetcode.com/problems/as-far-from-land-as-possible/description/)

To solve this problem, we can utilize the Breadth-First Search (BFS) algorithm. BFS is suitable for finding the shortest path in an unweighted grid, and in this case, it helps to calculate the maximum distance from any water cell to the nearest land cell.

Here's the approach we'll take:

1. **Identify Land Cells**: Start by identifying all land cells and add them to a queue.
2. **Multi-source BFS**: Perform BFS from all the land cells simultaneously. This helps propagate the distance from land cells to all water cells.
3. **Track the Maximum Distance**: During the BFS traversal, keep track of the maximum distance encountered from any water cell to the nearest land cell.
4. **Edge Cases**: Handle edge cases where the grid is entirely land or entirely water by returning -1.

### Step-by-Step Implementation

1. **Initialization**:
   - Create a queue and enqueue all land cells.
   - Maintain a visited matrix to keep track of visited cells.

2. **Perform BFS**:
   - Dequeue each cell, explore its neighbors (up, down, left, right).
   - If a neighbor is a water cell and hasn't been visited, mark it as visited, enqueue it, and update its distance.
   - Keep track of the maximum distance.

3. **Return Result**:
   - If there are no water cells or no land cells, return -1.
   - Otherwise, return the maximum distance found.

Here is the Python implementation of the above logic:

```python
from collections import deque

class Solution:
    def maxDistance(self, grid: List[List[int]]) -> int:
        n = len(grid)
        
        # Initialize the queue with all land cells
        queue = deque()
        for i in range(n):
            for j in range(n):
                if grid[i][j] == 1:
                    queue.append((i, j))
        
        # Edge case: If no land or no water, return -1
        if len(queue) == 0 or len(queue) == n * n:
            return -1
        
        # Perform BFS from all land cells
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        max_distance = -1
        
        while queue:
            x, y = queue.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n and grid[nx][ny] == 0:
                    grid[nx][ny] = grid[x][y] + 1
                    max_distance = max(max_distance, grid[nx][ny] - 1)
                    queue.append((nx, ny))
        
        return max_distance

# Example usage:
sol = Solution()
print(sol.maxDistance([[1,0,1],[0,0,0],[1,0,1]]))  # Output: 2
print(sol.maxDistance([[1,0,0],[0,0,0],[0,0,0]]))  # Output: 4
```

### Explanation:

1. **Initialization**:
   - We initialize a queue with all land cells and mark their positions.
   - If the grid is entirely land or water, we return -1 immediately.

2. **BFS Traversal**:
   - For each cell in the queue, we explore its neighbors. If a neighbor is water and hasn't been visited (i.e., it's still 0), we update its distance and enqueue it.
   - We keep updating the maximum distance encountered during this traversal.

3. **Result**:
   - The final value of `max_distance` is the maximum distance from any water cell to the nearest land cell.

This approach ensures that we efficiently find the maximum distance using multi-source BFS, with a time complexity of O(n^2).
