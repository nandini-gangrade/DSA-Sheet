# [1192. Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/description/)

To solve the problem of finding critical connections in a network of servers, we can use a graph algorithm known as Tarjan's Algorithm for finding bridges in an undirected graph. A bridge (or critical connection) is an edge in a graph that, when removed, increases the number of connected components in the graph. 

Here's a step-by-step approach to implement this using Python:

### Tarjan's Algorithm Overview

1. **Graph Representation**:
   - Use an adjacency list to represent the graph.

2. **DFS Traversal**:
   - Perform a Depth-First Search (DFS) traversal to explore all nodes and edges.
   - Maintain two arrays during DFS:
     - `discovery_time[]`: The discovery time of each node.
     - `low[]`: The lowest discovery time reachable from the node.
   - An edge `(u, v)` is a bridge if `low[v] > discovery_time[u]` after visiting node `v`.

3. **Tarjan's Algorithm**:
   - Initialize `discovery_time` and `low` arrays with `-1` (indicating unvisited).
   - Perform DFS from each unvisited node and update the `low` values based on back edges.
   - Collect edges that satisfy the bridge condition.

### Implementation

Here’s how you can implement Tarjan’s Algorithm in Python to find all critical connections:

```python
from typing import List

class Solution:
    def criticalConnections(self, n: int, connections: List[List[int]]) -> List[List[int]]:
        def dfs(node, parent):
            nonlocal time
            discovery_time[node] = low[node] = time
            time += 1
            
            for neighbor in graph[node]:
                if discovery_time[neighbor] == -1:  # If neighbor is not visited
                    dfs(neighbor, node)
                    # Check if the subtree rooted at neighbor has a connection back to one of the ancestors of node
                    low[node] = min(low[node], low[neighbor])
                    # If the lowest vertex reachable from subtree under neighbor is below node's discovery time, it's a bridge
                    if low[neighbor] > discovery_time[node]:
                        bridges.append([node, neighbor])
                elif neighbor != parent:  # Update low value of node for parent function calls
                    low[node] = min(low[node], discovery_time[neighbor])

        # Initialize graph
        graph = [[] for _ in range(n)]
        for u, v in connections:
            graph[u].append(v)
            graph[v].append(u)

        # Arrays to keep track of discovery times and low values
        discovery_time = [-1] * n
        low = [-1] * n
        time = 0
        bridges = []

        # Run DFS from each unvisited node
        for i in range(n):
            if discovery_time[i] == -1:
                dfs(i, -1)

        return bridges
```

### Explanation

1. **Graph Initialization**:
   - Construct an adjacency list from the given connections.

2. **DFS Function**:
   - Traverse the graph using DFS.
   - Update `discovery_time` and `low` values.
   - Determine bridges based on the condition `low[neighbor] > discovery_time[node]`.

3. **Execution**:
   - Start DFS from each unvisited node to ensure all components are covered.
   - Collect and return the bridges.

### Complexity Analysis

- **Time Complexity**: O(V + E), where V is the number of vertices and E is the number of edges. Each node and edge is visited once.
- **Space Complexity**: O(V + E) due to the adjacency list and other auxiliary data structures.

This approach efficiently finds all critical connections (bridges) in the network, handling the constraints effectively.
