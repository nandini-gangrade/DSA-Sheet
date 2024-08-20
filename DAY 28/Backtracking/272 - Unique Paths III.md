# [980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii/description/)

The problem you're dealing with is a variation of the classic **"unique paths"** problem, but with additional constraints. In this specific problem, you have a grid with obstacles and empty cells, and your goal is to find all unique paths from a starting cell to an ending cell, while visiting every non-obstacle cell exactly once.

Here's a breakdown of the problem, intuition, approach, code, and complexity:

### Problem Explanation

You are given a grid with:
- **1** representing the starting square.
- **2** representing the ending square.
- **0** representing empty squares that you can walk over.
- **-1** representing obstacles that you cannot walk over.

The task is to count all possible paths from the starting square to the ending square, such that every empty cell (0) is visited exactly once.

### Intuition

To solve this problem, you can use **Depth-First Search (DFS)** to explore all possible paths. Here's the intuition behind the approach:
1. **DFS Traversal**: Use DFS to explore all possible moves from the current cell.
2. **Tracking Visited Cells**: Keep track of visited cells to ensure that you don’t revisit them in the same path.
3. **Base Cases**:
   - If you reach the ending cell and have visited all required cells, it counts as a valid path.
   - If you hit an obstacle or go out of bounds, terminate that path.
4. **Backtracking**: After exploring all possible paths from the current cell, revert changes to explore new paths.

### Approach

1. **Initialization**:
   - Parse the grid to locate the starting and ending points.
   - Count the total number of non-obstacle cells that need to be visited.
   - Convert the starting and ending points to usable format and set the grid values to 0.

2. **DFS Function**:
   - If the current cell is the destination and all non-obstacle cells have been visited, increase the count.
   - Mark the current cell as visited and recursively explore all four directions (up, down, left, right).
   - Unmark the current cell (backtracking) after exploring all paths from it.

3. **Final Computation**:
   - Call the DFS function from the starting point and return the count of valid paths.

### Code

Here's the provided C++ code translated to Python:

```python
class Solution:
    def uniquePathsIII(self, grid: List[List[int]]) -> int:
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]  # right, down, left, up
        
        def dfs(r, c, remaining):
            if (r, c) == end:
                return 1 if remaining == 0 else 0
            
            # Temporarily mark this cell as visited
            temp = grid[r][c]
            grid[r][c] = -1  # Mark as visited
            paths = 0
            
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < len(grid) and 0 <= nc < len(grid[0]) and grid[nr][nc] != -1:
                    paths += dfs(nr, nc, remaining - 1)
            
            # Unmark this cell as visited
            grid[r][c] = temp
            return paths

        start = end = None
        zeros = 0
        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == 1:
                    start = (r, c)
                    grid[r][c] = 0
                elif grid[r][c] == 2:
                    end = (r, c)
                    grid[r][c] = 0
                elif grid[r][c] == 0:
                    zeros += 1
        
        if not start or not end:
            return 0

        return dfs(start[0], start[1], zeros)
```

### Complexity Analysis

1. **Time Complexity**:
   - The time complexity is \(O(4^T)\), where \(T\) is the number of non-obstacle cells. This is due to the recursive exploration of all possible paths in the grid.
   - Each cell is visited and unvisited (backtracked) multiple times, leading to exponential growth in the number of recursive calls.

2. **Space Complexity**:
   - The space complexity is \(O(N \times M)\) for the grid and call stack. The call stack can grow up to the size of the grid in the worst case.

Given the constraints (with a maximum grid size of 20x20), this approach is feasible and should work efficiently within the problem's limits.
