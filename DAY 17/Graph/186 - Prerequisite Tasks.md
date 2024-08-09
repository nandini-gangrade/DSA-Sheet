# [Prerequisite Tasks](https://www.geeksforgeeks.org/problems/prerequisite-tasks/1)

To determine if it is possible to finish all tasks given the prerequisites, we can think of this problem as detecting if there is a cycle in a directed graph. Each task is a node, and each prerequisite is a directed edge from one task to another. If there is a cycle in this graph, it means that it's impossible to complete all tasks.

### Approach

1. **Graph Representation**: 
   - Represent the tasks and prerequisites as a directed graph using an adjacency list.
   - Calculate the in-degree for each task. The in-degree of a task is the number of prerequisites it has.

2. **Topological Sort using Kahn's Algorithm**:
   - Use Kahn's algorithm for topological sorting, which is based on repeatedly removing nodes with no incoming edges.
   - Initialize a queue with all tasks having in-degree 0 (i.e., no prerequisites).
   - Process each task from the queue, reducing the in-degree of its neighbors by 1. If any neighbor's in-degree becomes 0, add it to the queue.
   - Count the number of tasks processed. If this count equals the total number of tasks, it means all tasks can be completed; otherwise, there is a cycle.

### Implementation

Here's how the solution can be implemented:

```python
from collections import deque

class Solution:
    def isPossible(self, N, P, prerequisites):
        # Step 1: Create adjacency list and in-degree array
        adj = [[] for _ in range(N)]
        in_degree = [0] * N
        
        # Fill adjacency list and in-degree
        for u, v in prerequisites:
            adj[v].append(u)  # u depends on v, hence an edge from v to u
            in_degree[u] += 1
        
        # Step 2: Initialize the queue with nodes having in-degree 0
        queue = deque()
        for i in range(N):
            if in_degree[i] == 0:
                queue.append(i)
        
        # Step 3: Perform BFS/Topological sort
        count = 0  # Number of tasks processed
        while queue:
            node = queue.popleft()
            count += 1
            
            # Reduce in-degree for all neighbors
            for neighbor in adj[node]:
                in_degree[neighbor] -= 1
                if in_degree[neighbor] == 0:
                    queue.append(neighbor)
        
        # If count equals N, all tasks can be completed
        return count == N

# Example usage
sol = Solution()
print(sol.isPossible(4, 3, [[1,0],[2,1],[3,2]]))  # Output: True
print(sol.isPossible(2, 2, [[1,0],[0,1]]))  # Output: False
```

### Explanation

- **Adjacency List and In-degree Calculation**: We create an adjacency list where `adj[v]` contains all tasks that depend on task `v`. The in-degree of each task is initialized based on the prerequisites.
  
- **Queue Initialization**: We start with tasks that have no prerequisites (`in_degree[i] == 0`).

- **BFS and Topological Sorting**: By removing tasks with no prerequisites and updating their neighbors, we effectively perform a topological sort. If we can process all tasks, it indicates there is no cycle.

- **Result**: If the number of tasks processed equals `N`, we return `True`; otherwise, we return `False`.

This approach efficiently checks for cycles in the task dependency graph, ensuring that tasks can be completed in the given constraints.
