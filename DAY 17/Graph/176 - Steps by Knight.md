# [Steps by Knight](https://www.geeksforgeeks.org/problems/steps-by-knight5927/1)

To solve the problem of finding the minimum steps a knight will take to reach a target position on a chessboard, we can use a Breadth-First Search (BFS) approach. The BFS algorithm is suitable for finding the shortest path in an unweighted graph, and in this case, the chessboard can be considered as such a graph with positions as nodes and valid knight moves as edges.

### Explanation

1. **Representation of Moves**:
   - A knight on a chessboard has up to 8 possible moves. These moves can be represented as offsets to the current position. The possible moves are:
     - \((+2, +1)\), \((+2, -1)\), \((-2, +1)\), \((-2, -1)\)
     - \((+1, +2)\), \((+1, -2)\), \((-1, +2)\), \((-1, -2)\)

2. **BFS Initialization**:
   - We start the BFS from the initial position of the knight.
   - We use a queue to explore each position the knight can reach.
   - We also maintain a `visited` matrix to keep track of visited positions to avoid re-processing them.

3. **Processing the Queue**:
   - For each position, calculate all possible new positions using the knight's move offsets.
   - If a new position matches the target position, return the current count of steps.
   - If the new position is valid (within bounds and not visited), mark it as visited and enqueue it for further exploration.

4. **Return Result**:
   - If the queue is exhausted without finding the target position, return -1, although this should not happen given valid inputs since a knight can eventually reach any position on an empty board.

### Implementation

Here's the implementation of the solution:

```python
from collections import deque

class Solution:
    def is_valid(self, x, y, n, visited):
        # Check if the position is within bounds and not yet visited
        return 0 <= x < n and 0 <= y < n and not visited[x][y]

    def minStepToReachTarget(self, KnightPos, TargetPos, N):
        # Convert 1-based index to 0-based index for internal processing
        sx, sy = KnightPos[0] - 1, KnightPos[1] - 1
        tx, ty = TargetPos[0] - 1, TargetPos[1] - 1

        # If the knight is already at the target position
        if sx == tx and sy == ty:
            return 0

        # All possible moves of a knight
        moves = [(2, 1), (2, -1), (-2, 1), (-2, -1), (1, 2), (1, -2), (-1, 2), (-1, -2)]

        # Initialize the visited matrix
        visited = [[False] * N for _ in range(N)]
        visited[sx][sy] = True

        # Initialize the queue for BFS with the starting position and step count
        q = deque([(sx, sy, 0)])

        # BFS loop
        while q:
            x, y, steps = q.popleft()

            # Explore all possible knight moves
            for dx, dy in moves:
                nx, ny = x + dx, y + dy

                # Check if the new position is the target
                if nx == tx and ny == ty:
                    return steps + 1

                # If the new position is valid, mark as visited and add to queue
                if self.is_valid(nx, ny, N, visited):
                    visited[nx][ny] = True
                    q.append((nx, ny, steps + 1))

        # If no path is found (should not happen with valid input), return -1
        return -1
```

### Key Points

- **BFS for Shortest Path**: BFS is used because it explores all nodes at the present "depth" level before moving on to nodes at the next depth level, ensuring the shortest path in an unweighted graph.
- **Visited Matrix**: Helps in avoiding repeated processing of the same position, optimizing the search.
- **Edge Cases**: The solution handles cases where the knight starts at the target position immediately. 

This implementation efficiently finds the shortest path for the knight to reach the target position using BFS, which is optimal for unweighted scenarios like a chessboard with free moves.
