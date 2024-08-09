# [DFS of Graph](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

To perform a Depth First Search (DFS) traversal of a connected, undirected graph, you can use a recursive approach. In DFS, you start from a given node (in this case, node 0) and explore as far as possible along each branch before backtracking. This means you visit a node, mark it as visited, then recursively visit all its unvisited adjacent nodes.

Here's a step-by-step breakdown of how you can implement DFS for a graph:

### Approach

1. **Initialize Structures**:
   - Use a list `visited` to keep track of which nodes have been visited to avoid revisiting them.
   - Use a list `dfs_result` to store the nodes in the order they are visited during the DFS traversal.

2. **DFS Recursive Function**:
   - Create a recursive function `dfs` that:
     - Marks the current node as visited.
     - Adds the current node to the DFS result.
     - Recursively visits all unvisited adjacent nodes of the current node.

3. **Start DFS from Node 0**:
   - Call the `dfs` function starting from node 0.

4. **Output the Result**:
   - Return the `dfs_result` list, which contains the nodes in the order they were visited.

### Code Implementation

Here is the Python implementation of the DFS algorithm using recursion:

```python
class Solution:
    
    # Function to return a list containing the DFS traversal of the graph.
    def dfsOfGraph(self, V, adj):
        # Initialize a visited list to keep track of visited nodes
        visited = [False] * V
        dfs_result = []
        
        # Call the recursive dfs function starting from node 0
        self.dfs(0, adj, visited, dfs_result)
        
        return dfs_result
    
    def dfs(self, node, adj, visited, dfs_result):
        # Mark the current node as visited
        visited[node] = True
        # Add the current node to the DFS result
        dfs_result.append(node)
        
        # Recur for all the vertices adjacent to this vertex
        for neighbor in adj[node]:
            if not visited[neighbor]:
                self.dfs(neighbor, adj, visited, dfs_result)

# Example usage:
V = 5
adj = [[2, 3, 1], [0], [0, 4], [0], [2]]

sol = Solution()
print(sol.dfsOfGraph(V, adj))  # Output: [0, 2, 4, 3, 1]
```

### Explanation of the Code

- **`dfsOfGraph` Method**: This method initializes the `visited` list and the `dfs_result` list. It then calls the recursive `dfs` function starting from node `0`.

- **`dfs` Method**: This method is the core of the DFS traversal:
  - It marks the current node as visited and adds it to the result list.
  - It then iterates through all adjacent nodes. If an adjacent node hasn't been visited, it recursively calls the `dfs` method on that node.

### Complexity Analysis

- **Time Complexity**: O(V + E), where V is the number of vertices and E is the number of edges. In the worst case, all nodes and edges are visited.
- **Space Complexity**: O(V), due to the space used by the recursion stack and the visited list.

This implementation efficiently performs a DFS traversal of the graph, exploring each node's adjacent vertices recursively until all reachable nodes from the starting node (0) are visited.
