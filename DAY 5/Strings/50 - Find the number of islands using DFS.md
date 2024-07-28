# [Find the number of islands using DFS](https://www.geeksforgeeks.org/find-the-number-of-islands-using-dfs/)

To solve the problem of finding the number of islands in a binary 2D matrix, we can use a graph traversal technique such as Depth-First Search (DFS) or Breadth-First Search (BFS). Each '1' in the matrix represents land, and adjacent '1's (horizontally, vertically, or diagonally) are part of the same island. Our task is to count how many disconnected groups of '1's (islands) are present in the matrix.

## Approach

1. **Initialize Count**: Start by initializing a counter to zero. This will keep track of the number of islands.

2. **Traverse the Matrix**: Iterate through each cell in the matrix. If a cell contains '1', it indicates that part of an island is found.

3. **Perform DFS/BFS**: Upon finding a '1', use DFS (or BFS) to mark all adjacent '1's as visited (or change them to '0') to ensure they are not counted again. This traversal marks the entire island.

4. **Increment the Island Counter**: After finishing the traversal of one island, increment the island counter.

5. **Continue the Process**: Continue scanning the entire matrix, repeating the above steps to ensure all islands are counted.

## DFS Implementation

Here's the code implementation using DFS:

```python
class Solution:
    def numIslands(self, grid):
        if not grid:
            return 0

        def dfs(r, c):
            # Check for out-of-bounds or water cells
            if r < 0 or c < 0 or r >= len(grid) or c >= len(grid[0]) or grid[r][c] == '0':
                return
            
            # Mark the cell as visited
            grid[r][c] = '0'

            # Visit all 8 adjacent cells
            directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
            for dr, dc in directions:
                dfs(r + dr, c + dc)

        num_islands = 0

        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == '1':  # Found an island
                    dfs(r, c)
                    num_islands += 1  # Increment the island count

        return num_islands

# Example usage:
matrix = [
    ['1', '1', '0', '0', '0'],
    ['0', '1', '0', '0', '1'],
    ['1', '0', '0', '1', '1'],
    ['0', '0', '0', '0', '0'],
    ['1', '0', '1', '0', '0']
]

solution = Solution()
print(solution.numIslands(matrix))  # Output: 4
```

## Explanation of the Code

- **DFS Function**: The `dfs` function checks whether the current cell is out of bounds or is water ('0'). If not, it marks the cell as visited by setting it to '0'. Then, it recursively calls itself for all 8 possible directions (horizontal, vertical, and diagonal).

- **Traversal of the Grid**: The grid is traversed using nested loops. Whenever an unvisited '1' is found, `dfs` is invoked, marking the entire island as visited.

- **Counting Islands**: Each time a new island (unvisited '1') is encountered, `num_islands` is incremented.

## Complexity Analysis

- **Time Complexity**: \(O(M \times N)\), where \(M\) is the number of rows and \(N\) is the number of columns. Each cell is visited once.

- **Space Complexity**: \(O(M \times N)\) in the worst case, which occurs when the entire grid is filled with land, requiring space for the recursion stack.

This solution efficiently counts the number of islands in a binary matrix by using DFS to explore each island and marking it as visited to ensure accurate counting.
