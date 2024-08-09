# [BFS of graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)

To perform Breadth First Traversal (BFS) on a directed graph starting from node `0`, we can use a queue data structure. The goal is to visit all nodes that are reachable from node `0` in the order of their levels, where each level represents a set of nodes that can be reached with an additional edge from the nodes in the previous level.

Here's a step-by-step approach to solve the problem:

### Approach

1. **Initialize Structures**:
   - Use a queue to help with the level-order traversal of the graph.
   - Use a boolean list `visited` to keep track of which nodes have already been visited, preventing cycles and repeated nodes in the BFS traversal.

2. **Start from Node 0**:
   - Enqueue node `0` and mark it as visited.

3. **Traverse the Graph**:
   - While the queue is not empty, perform the following steps:
     - Dequeue the front node from the queue and add it to the BFS result.
     - For each unvisited adjacent node of the current node, mark it as visited and enqueue it.

4. **Output the Result**:
   - Once the queue is empty, the BFS traversal is complete. The result is the list of nodes in the order they were visited.

### Code Implementation

Here's the implementation of the BFS algorithm for the given graph in Python:

```python
from collections import deque

class Solution:
    def bfsOfGraph(self, V, adj):
        # Initialize a queue for BFS and a visited list
        queue = deque([0])
        visited = [False] * V
        bfs_result = []
        
        # Start from the 0th node
        visited[0] = True
        
        while queue:
            # Dequeue a vertex from the queue
            node = queue.popleft()
            bfs_result.append(node)
            
            # Get all adjacent vertices of the dequeued vertex
            # If an adjacent has not been visited, mark it visited and enqueue it
            for neighbor in adj[node]:
                if not visited[neighbor]:
                    queue.append(neighbor)
                    visited[neighbor] = True
        
        return bfs_result

# Example usage:
V = 5
adj = [[1, 2, 3], [], [4], [], []]

sol = Solution()
print(sol.bfsOfGraph(V, adj))  # Output: [0, 1, 2, 3, 4]
```

### Complexity Analysis

- **Time Complexity**: O(V + E), where V is the number of vertices and E is the number of edges. This is because each vertex and edge is processed once in the BFS traversal.
- **Space Complexity**: O(V), due to the space used by the queue and the visited list.

This implementation efficiently traverses all nodes that are reachable from the starting node `0`, leveraging the BFS approach to ensure nodes are visited level-by-level. This makes it well-suited for scenarios where you need to explore shortest paths or levels in a graph, as BFS naturally explores all neighbors of a node before moving to the next level.
