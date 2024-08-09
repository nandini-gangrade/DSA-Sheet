# [Strongly Connected Components (Kosaraju's Algo)](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1)

To solve the problem of finding the number of strongly connected components (SCCs) in a directed graph, we can use **Kosaraju's algorithm**. This algorithm is efficient with a time complexity of \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges. Here's a step-by-step breakdown of the approach:

### Kosaraju's Algorithm Approach

1. **Perform a DFS to Get Finish Order:**
   - Conduct a Depth First Search (DFS) on the original graph to determine the finish order of vertices. This will give us an ordering based on which we should explore nodes in the transposed graph.
   - Use a stack to record the order of completion of nodes. Nodes are pushed onto the stack when they have finished processing.

2. **Transpose the Graph:**
   - Reverse the direction of all edges in the graph. This is called the transposed graph.
   - Transposing helps in identifying the SCCs when processing nodes in the finish order derived in step 1.

3. **DFS on Transposed Graph:**
   - Use the stack from step 1 to process nodes in reverse order of completion. This is equivalent to processing nodes in decreasing order of their finish time in the original DFS.
   - Perform DFS in the transposed graph, starting from each unvisited node. Each DFS traversal in this step will identify one SCC.

4. **Count SCCs:**
   - Each DFS in the transposed graph identifies one SCC. Count these traversals to determine the number of SCCs.

### Complexity

- **Time Complexity:** \(O(V + E)\) because each node and edge is visited at most twice (once in the original graph and once in the transposed graph).
- **Space Complexity:** \(O(V + E)\) due to the storage of the graph and its transpose.

### Code Implementation

Here's how you can implement Kosaraju's algorithm in Python:

```python
class Solution:
    
    # Function to find the number of strongly connected components in the graph.
    def kosaraju(self, V, adj):
        # Step 1: Perform DFS to get the finish order
        stack = []
        visited = [False] * V
        
        def dfs(v):
            visited[v] = True
            for neighbor in adj[v]:
                if not visited[neighbor]:
                    dfs(neighbor)
            stack.append(v)
        
        for i in range(V):
            if not visited[i]:
                dfs(i)
        
        # Step 2: Transpose the graph
        transposed_adj = [[] for _ in range(V)]
        for v in range(V):
            for neighbor in adj[v]:
                transposed_adj[neighbor].append(v)
        
        # Step 3: Perform DFS on the transposed graph
        visited = [False] * V
        scc_count = 0
        
        def dfs_transposed(v):
            visited[v] = True
            for neighbor in transposed_adj[v]:
                if not visited[neighbor]:
                    dfs_transposed(neighbor)
        
        # Step 4: Process nodes in order of decreasing finish time
        while stack:
            v = stack.pop()
            if not visited[v]:
                dfs_transposed(v)
                scc_count += 1
        
        return scc_count
```

### Explanation of the Code

1. **DFS for Finish Order:**
   - The `dfs` function records the order of completion of each node by pushing nodes onto a stack after exploring all reachable nodes.

2. **Transpose Graph:**
   - We create `transposed_adj` to store the reversed edges of the graph.

3. **DFS on Transposed Graph:**
   - The `dfs_transposed` function is used to explore nodes in the transposed graph.
   - We process nodes based on the order in the stack, which ensures that we discover SCCs correctly.

4. **Counting SCCs:**
   - Each time a DFS is initiated from an unvisited node in the transposed graph, we increment the `scc_count`, which represents a new strongly connected component.

This implementation efficiently computes the number of SCCs using Kosaraju's algorithm, adhering to the problem's constraints and expected complexities.
