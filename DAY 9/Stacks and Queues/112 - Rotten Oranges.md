# [Rotten Oranges](https://www.geeksforgeeks.org/problems/rotten-oranges2536/1)

1. **Rotting Mechanism**: A rotten orange at `(i, j)` can rot adjacent fresh oranges in the neighboring cells `(i-1, j)`, `(i+1, j)`, `(i, j-1)`, `(i, j+1)` in one unit of time.
2. **BFS Approach**: Use BFS to simulate the rotting process starting from all initial rotten oranges simultaneously. This ensures that we process the grid level by level, which directly correlates with time units.

## Approach

1. **Initialization**:
   - Use a queue to keep track of the rotten oranges and their positions.
   - Maintain counters for fresh oranges and total time.

2. **BFS Execution**:
   - For each rotten orange, rot all its neighboring fresh oranges.
   - Track the time it takes for each level of BFS to complete.

3. **Edge Cases**:
   - If after processing all possible rotten oranges, there are still fresh oranges left, it means not all oranges can rot, and we return `-1`.

### Detailed Steps

1. **Identify Initial States**:
   - Traverse the grid to find all initial rotten oranges and count the number of fresh oranges.
   - Store rotten oranges in a queue to start BFS.

2. **Process Grid Using BFS**:
   - For each level of BFS, process all oranges at the current level.
   - For each orange, rot its adjacent fresh oranges and update the queue and counts accordingly.
   - Increase the time after processing all oranges at the current level.

3. **Final Check**:
   - If there are still fresh oranges left after BFS completes, return `-1`.
   - Otherwise, return the time taken.

## Code
```python
from collections import deque

class Solution:
    def orangesRotting(self, grid):
        if not grid:
            return -1
        
        m, n = len(grid), len(grid[0])
        rotten = deque()
        fresh_count = 0
        
        # Collect all initial rotten oranges and count fresh oranges
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 2:
                    rotten.append((i, j))
                elif grid[i][j] == 1:
                    fresh_count += 1
        
        # Directions for moving up, down, left, right
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        time = 0
        
        # BFS process
        while rotten and fresh_count > 0:
            size = len(rotten)
            for _ in range(size):
                x, y = rotten.popleft()
                for dx, dy in directions:
                    nx, ny = x + dx, y + dy
                    if 0 <= nx < m and 0 <= ny < n and grid[nx][ny] == 1:
                        grid[nx][ny] = 2
                        rotten.append((nx, ny))
                        fresh_count -= 1
            time += 1
        
        return time if fresh_count == 0 else -1
```

## Complexity Analysis

- **Time Complexity**: \(O(n \times m)\), where \(n\) and \(m\) are the dimensions of the grid. Each cell is processed at most once during BFS.
- **Space Complexity**: \(O(n \times m)\) for the queue used in BFS and the grid storage.

This solution is efficient for the given problem constraints and ensures that all fresh oranges are processed correctly.
