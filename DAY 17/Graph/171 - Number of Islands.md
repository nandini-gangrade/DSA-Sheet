# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/description/)

To solve the problem of counting the number of islands in a 2D grid, we can use Depth First Search (DFS) or Breadth First Search (BFS) to explore the connected components of '1's. The idea is to iterate through each cell of the grid, and every time we encounter a '1', we increment our island count and use DFS or BFS to mark all the connected '1's as visited, effectively "sinking" the island.

Here’s a step-by-step approach using DFS:

### Approach

1. **Initialize Variables**:
   - Count variable `num_islands` to keep track of the number of islands.
   - Directions array `directions` to simplify exploring the adjacent cells (up, down, left, right).

2. **DFS Function**:
   - A recursive DFS function that marks all '1's connected to the starting cell as visited by changing them to '0's.

3. **Traverse the Grid**:
   - Loop through each cell in the grid.
   - When a '1' is found, increment the island count and call the DFS function to mark all connected '1's.

4. **Edge Cases**:
   - If the grid is empty or only contains water, the number of islands is zero.

### Code Implementation

Here is the Python code implementing the above approach:

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0
        
        num_islands = 0
        rows, cols = len(grid), len(grid[0])
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        
        def dfs(r, c):
            # Mark the current cell as visited
            grid[r][c] = '0'
            # Explore all adjacent cells in 4 possible directions
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == '1':
                    dfs(nr, nc)
        
        # Traverse each cell in the grid
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':  # Found an island
                    num_islands += 1
                    dfs(r, c)  # Sink the island
        
        return num_islands

# Example usage:
grid1 = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
grid2 = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

sol = Solution()
print(sol.numIslands(grid1))  # Output: 1
print(sol.numIslands(grid2))  # Output: 3
```

### Explanation of the Code

- **DFS Function**: The `dfs` function is used to explore all connected '1's starting from the given cell (r, c). It changes '1's to '0's to mark them as visited.
- **Grid Traversal**: The nested loops traverse each cell in the grid. When a '1' is encountered, it represents an unvisited island, so we increment the island count and call the `dfs` function to "sink" the entire island by marking all its connected land cells as '0'.

### Complexity Analysis

- **Time Complexity**: O(m * n), where m is the number of rows and n is the number of columns in the grid. Each cell is visited once.
- **Space Complexity**: O(m * n) in the worst case for the recursive call stack in DFS, especially if the grid forms a single large island. In practice, the space complexity is much smaller due to the call stack's depth being the size of the largest connected component of '1's.

This approach efficiently counts the number of islands in the grid by exploring and marking all parts of each island found, ensuring no island is counted more than once.
