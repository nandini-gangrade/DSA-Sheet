# [289. Game of Life](https://leetcode.com/problems/game-of-life/description/)
[LeetCode Solution](https://leetcode.com/problems/game-of-life/solutions/5540092/best-solution-challenge-day-1-revisewitharsh)

Conway's Game of Life is a zero-player game that takes place on a 2D grid where each cell can be either alive or dead. The state of each cell in the next step is determined by the number of its live neighbors according to four rules:

1. Any live cell with fewer than two live neighbors dies (under-population).
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies (over-population).
4. Any dead cell with exactly three live neighbors becomes a live cell (reproduction).

## Approach

1. **Simultaneous Updates:** We need to ensure that the board is updated simultaneously, meaning we cannot overwrite a cell and use its new state to determine the state of another cell.
   
2. **In-Place Updates:** To solve the problem in-place, we can use temporary states to encode changes:
   - Use `-1` to represent a live cell that dies.
   - Use `2` to represent a dead cell that becomes live.

3. **Count Live Neighbors:** For each cell, we will count the number of live neighbors by checking the eight possible directions (up, down, left, right, and four diagonals).

4. **Final Update:** After determining the state changes, we update the grid to reflect the new states, converting `-1` back to `0` and `2` back to `1`.

## Code

```python []
from typing import List

class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        m, n = len(board), len(board[0])
        
        # Directions representing the 8 possible neighbors
        directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
        
        # Function to count live neighbors
        def countLiveNeighbors(x, y):
            live_neighbors = 0
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n and abs(board[nx][ny]) == 1:
                    live_neighbors += 1
            return live_neighbors
        
        # First pass: apply the rules and mark changes using temporary states
        for i in range(m):
            for j in range(n):
                live_neighbors = countLiveNeighbors(i, j)
                
                # Rule 1 or Rule 3
                if board[i][j] == 1 and (live_neighbors < 2 or live_neighbors > 3):
                    board[i][j] = -1  # Mark as dead (was alive)
                
                # Rule 4
                if board[i][j] == 0 and live_neighbors == 3:
                    board[i][j] = 2  # Mark as live (was dead)
        
        # Second pass: finalize the board with the actual states
        for i in range(m):
            for j in range(n):
                if board[i][j] == -1:
                    board[i][j] = 0
                elif board[i][j] == 2:
                    board[i][j] = 1
```

## Complexity Analysis

- **Time Complexity:** \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns. We iterate through each cell once and check its neighbors.
  
- **Space Complexity:** \(O(1)\), as we are modifying the board in-place and using only a constant amount of extra space.

## Handling Infinite Grid

The problem constraints mention that the board is theoretically infinite. In practice, this would mean handling cases where live cells are near the borders. There are a few strategies to address this:

1. **Padding with Dead Cells:** One approach is to add an extra border of dead cells around the grid. This ensures that calculations for edge cells have a uniform number of neighbors to consider.

2. **Dynamic Expansion:** Alternatively, we could dynamically expand the grid by adding rows and columns of dead cells if the current pattern reaches the border and needs more space.

3. **Wrapping (Torus):** Another approach is to treat the grid as a torus, where the edges are connected, wrapping the grid's behavior. However, this approach may not always suit every application of the Game of Life.

For solving the in-place version efficiently on the given constraints, managing an infinite grid can typically involve careful initialization and checks to prevent edge effects or undesired border growth.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
