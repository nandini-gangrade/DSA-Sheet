# [733. Flood Fill](https://leetcode.com/problems/flood-fill/description/)

To solve the flood fill problem, we can use a Depth First Search (DFS) or Breadth First Search (BFS) approach. The idea is to start from the given starting pixel and recursively or iteratively fill all connected pixels with the new color.

Here is a step-by-step solution using DFS:

### Approach

1. **Check Base Case**:
   - If the starting pixel is already of the target color, there's no need to change anything, and we can return the image as is.

2. **Define DFS Function**:
   - Create a recursive DFS function that will check all four directions (up, down, left, right) from the current pixel.
   - If a neighboring pixel has the same color as the starting pixel, fill it with the new color and continue the DFS from that pixel.

3. **Traverse and Fill**:
   - Start the DFS from the initial pixel `(sr, sc)`.
   - Change the color of the starting pixel and recursively fill all connected pixels with the same color.

### Code Implementation

Here's how you can implement the solution using DFS in Python:

```python
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
        # Get the starting pixel's color
        start_color = image[sr][sc]
        
        # If the starting pixel already has the target color, no changes are needed
        if start_color == color:
            return image
        
        # Dimensions of the image
        rows, cols = len(image), len(image[0])
        
        # Define the directions for 4-directional movement
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        
        def dfs(r, c):
            # Change the current pixel to the new color
            image[r][c] = color
            # Explore all four directions
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                # Check if the new position is within bounds and has the same start color
                if 0 <= nr < rows and 0 <= nc < cols and image[nr][nc] == start_color:
                    dfs(nr, nc)
        
        # Start the DFS from the starting pixel
        dfs(sr, sc)
        
        return image

# Example usage:
image1 = [[1, 1, 1], [1, 1, 0], [1, 0, 1]]
sr1, sc1, color1 = 1, 1, 2
image2 = [[0, 0, 0], [0, 0, 0]]
sr2, sc2, color2 = 0, 0, 0

sol = Solution()
print(sol.floodFill(image1, sr1, sc1, color1))  # Output: [[2, 2, 2], [2, 2, 0], [2, 0, 1]]
print(sol.floodFill(image2, sr2, sc2, color2))  # Output: [[0, 0, 0], [0, 0, 0]]
```

### Explanation of the Code

- **Base Case**: If the starting pixel's color is already the target color, we return the image unchanged to avoid unnecessary operations.
- **DFS Function**: The `dfs` function updates the current pixel's color and explores all valid neighboring pixels recursively.
- **Traversal**: The `dfs` function is initially called with the starting coordinates `(sr, sc)` to begin the flood fill process.

### Complexity Analysis

- **Time Complexity**: O(m * n), where m is the number of rows and n is the number of columns. In the worst case, we might need to visit every pixel.
- **Space Complexity**: O(m * n) in the worst case, due to the recursive
