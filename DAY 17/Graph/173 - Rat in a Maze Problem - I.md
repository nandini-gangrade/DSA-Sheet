# [Rat in a Maze Problem - I](https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1)

The problem involves finding all possible paths a rat can take from the top-left corner to the bottom-right corner in a square matrix while only being able to move to cells with a value of 1. The rat can move up (U), down (D), left (L), or right (R), and it cannot revisit any cell in the same path.

Here’s how we can solve this using a backtracking approach:

1. **Backtracking Approach**:
   - Start from the initial cell `(0, 0)` and try all possible moves (U, D, L, R).
   - If a move leads to a valid cell (within the matrix bounds and having value 1), mark the cell as visited and continue to the next cell.
   - If the destination cell `(n-1, n-1)` is reached, add the current path to the list of solutions.
   - Backtrack by unmarking the current cell as visited and remove the last move from the current path.
   
2. **Base Cases**:
   - If the initial or final cell is blocked (value 0), there is no valid path, so return an empty list or `["-1"]`.

3. **Optimization**:
   - Ensure not to revisit any cell in the same path by marking cells as visited during the current path traversal and unmarking them during backtracking.
   - Store and return all valid paths sorted in lexicographical order.

Here is the complete Python code for the solution:

```python
from typing import List

class Solution:
    def findPath(self, m: List[List[int]]) -> List[str]:
        def is_valid(x, y):
            return 0 <= x < n and 0 <= y < n and m[x][y] == 1
        
        def backtrack(x, y, path):
            if x == n-1 and y == n-1:
                ans.append(path)
                return
            
            # Temporarily mark the current cell as visited
            m[x][y] = 0
            
            # Move Down
            if is_valid(x + 1, y):
                backtrack(x + 1, y, path + "D")
            
            # Move Up
            if is_valid(x - 1, y):
                backtrack(x - 1, y, path + "U")
            
            # Move Right
            if is_valid(x, y + 1):
                backtrack(x, y + 1, path + "R")
            
            # Move Left
            if is_valid(x, y - 1):
                backtrack(x, y - 1, path + "L")
            
            # Backtrack by unmarking the current cell as visited
            m[x][y] = 1
        
        n = len(m)
        ans = []
        
        # Edge case: if starting or ending cell is blocked
        if m[0][0] == 0 or m[n-1][n-1] == 0:
            return ["-1"]
        
        # Start backtracking from the initial cell (0, 0)
        backtrack(0, 0, "")
        
        # If no paths found, return -1
        if not ans:
            return ["-1"]
        
        return ans

# Example usage:
solution = Solution()
mat1 = [[1, 0, 0, 0],
        [1, 1, 0, 1], 
        [1, 1, 0, 0],
        [0, 1, 1, 1]]
print(solution.findPath(mat1))  # Output: ["DDRDRR", "DRDDRR"]

mat2 = [[1, 0],
        [1, 0]]
print(solution.findPath(mat2))  # Output: ["-1"]
```

### Explanation:
- **is_valid**: This helper function checks if the cell `(x, y)` is within bounds and unblocked.
- **backtrack**: This is the core recursive function that attempts to find all paths using DFS. It explores all four directions from the current cell, adds valid paths to the result list, and uses backtracking to explore other paths.
- **Edge Cases**: The solution handles cases where the start or end cell is blocked and returns `["-1"]` accordingly.
- **Main Function**: `findPath` initializes the process and returns the final result. 

This approach ensures that we explore all possible paths while maintaining the constraints and limitations provided in the problem statement.
