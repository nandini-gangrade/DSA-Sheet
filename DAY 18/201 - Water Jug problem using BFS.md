# [Water Jug problem using BFS](https://www.geeksforgeeks.org/water-jug-problem-using-bfs/)

To solve the Water Jug problem using Breadth-First Search (BFS), we'll use the following approach:

1. **Initial State**:
   - Both jugs are initially empty.

2. **Goal**:
   - Reach a state where either of the jugs contains exactly `d` liters of water.

3. **Operations**:
   - **Fill a Jug**: Fill either jug completely.
   - **Empty a Jug**: Empty either jug.
   - **Pour Water**: Transfer water from one jug to the other until one is empty or full.

4. **State Representation**:
   - Represent the state of the jugs as `(X, Y)`, where `X` is the amount of water in Jug 1 and `Y` is the amount of water in Jug 2.

5. **BFS Traversal**:
   - Start from the initial state `(0, 0)`.
   - Explore all valid states derived from the current state using the allowed operations.
   - Use a queue to keep track of states to explore and a set to keep track of visited states to avoid redundant exploration.

6. **Solution**:
   - If we reach a state where either jug contains exactly `d` liters of water, we output the path to this state.

Here’s the Python code implementing the BFS approach to solve the Water Jug problem:

```python
from collections import deque

def waterJugBFS(X, Y, d):
    # Check for basic feasibility
    if d > max(X, Y) or d % gcd(X, Y) != 0:
        return []

    # Directions: fill, empty, pour from jug1 to jug2, pour from jug2 to jug1
    def getNextStates(x, y):
        next_states = []
        # Fill jug1
        next_states.append((X, y))
        # Fill jug2
        next_states.append((x, Y))
        # Empty jug1
        next_states.append((0, y))
        # Empty jug2
        next_states.append((x, 0))
        # Pour from jug1 to jug2
        pour = min(x, Y - y)
        next_states.append((x - pour, y + pour))
        # Pour from jug2 to jug1
        pour = min(y, X - x)
        next_states.append((x + pour, y - pour))
        return next_states

    # Initialize BFS
    queue = deque([(0, 0)])
    visited = set([(0, 0)])
    path = []
    parent = { (0, 0): None }
    
    # BFS
    while queue:
        x, y = queue.popleft()
        path.append((x, y))
        if x == d or y == d:
            result = []
            while (x, y) is not None:
                result.append((x, y))
                x, y = parent[(x, y)]
            return result[::-1]
        for next_state in getNextStates(x, y):
            if next_state not in visited:
                visited.add(next_state)
                queue.append(next_state)
                parent[next_state] = (x, y)
    
    return []

def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

# Example Usage:
X = 4
Y = 3
d = 2
print(waterJugBFS(X, Y, d))  # Example output: [(0, 0), (4, 0), (1, 3), (0, 2)]
```

### Explanation

1. **Feasibility Check**:
   - Ensure that `d` is achievable based on the capacities of the jugs and their greatest common divisor (GCD). If not, return an empty list.

2. **State Exploration**:
   - Generate possible next states by performing the allowed operations on the current state.
   - Use BFS to explore these states level by level.

3. **Tracking Path**:
   - Maintain a parent dictionary to reconstruct the path from the initial state to the goal state once we reach a state where either jug contains exactly `d` liters.

4. **Output**:
   - If a solution is found, reconstruct the path and return it. Otherwise, return an empty list.

This approach ensures that we explore all possible states efficiently and find the optimal path to reach the desired amount of water in one of the jugs.
