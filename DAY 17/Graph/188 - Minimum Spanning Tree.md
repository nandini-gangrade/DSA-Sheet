# [Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

To find the sum of the weights of the edges in the Minimum Spanning Tree (MST) of a weighted, undirected, and connected graph, we can use Prim's algorithm. The problem involves constructing the MST and calculating its total weight. Let's walk through the solution using Prim's algorithm, which is well-suited for this task due to its efficiency in handling dense graphs.

### Prim's Algorithm Overview

Prim's algorithm constructs an MST by iteratively adding the smallest edge that connects a vertex in the MST to a vertex outside of the MST. It maintains a priority queue to always fetch the smallest edge connecting the MST to the remaining vertices.

### Steps for Prim's Algorithm

1. **Initialization**:
   - Use a priority queue to store edges and their weights. The priority queue helps in efficiently fetching the minimum weight edge.
   - Initialize an array to keep track of the minimum edge weight for each vertex and a boolean array to mark vertices that are already included in the MST.

2. **Process**:
   - Start from any vertex and add it to the MST.
   - Update the priority queue with all edges that connect the vertex just added to vertices not yet included in the MST.
   - Continue adding the smallest edge that connects a new vertex to the MST until all vertices are included.

3. **Result**:
   - The sum of the weights of the edges added to the MST is the final result.

Here's the Python implementation of Prim's algorithm based on the problem statement:

```python
import heapq

def spanningTree(V, adj):
    # Priority queue to fetch the minimum weight edge efficiently
    pq = []
    
    # Array to keep track of the minimum weight edge for each vertex
    min_edge = [float('inf')] * V
    min_edge[0] = 0  # Start with vertex 0
    
    # Array to check if a vertex is included in the MST
    in_mst = [False] * V
    
    # Sum of the weights of the edges in the MST
    total_weight = 0
    
    # Push the initial vertex with 0 weight to the priority queue
    heapq.heappush(pq, (0, 0))  # (weight, vertex)
    
    while pq:
        weight, u = heapq.heappop(pq)
        
        # If the vertex is already in the MST, skip it
        if in_mst[u]:
            continue
        
        # Add the weight of the edge to the MST total weight
        total_weight += weight
        in_mst[u] = True
        
        # Process all adjacent vertices
        for v, w in adj[u]:
            if not in_mst[v] and w < min_edge[v]:
                min_edge[v] = w
                heapq.heappush(pq, (w, v))
    
    return total_weight
```

### Explanation

1. **Initialization**:
   - `pq` is a priority queue (min-heap) to store edges with their weights.
   - `min_edge` keeps track of the minimum weight edge connecting each vertex to the MST.
   - `in_mst` tracks whether a vertex is included in the MST or not.

2. **Processing**:
   - The vertex with the smallest edge weight is added to the MST.
   - The edge weights for its adjacent vertices are updated in the priority queue.
   - The process continues until all vertices are included in the MST.

3. **Result Calculation**:
   - The `total_weight` accumulates the weight of each edge added to the MST, which is the answer.

This implementation ensures that the MST is constructed efficiently, with a time complexity of \(O(E \log V)\), where \(E\) is the number of edges and \(V\) is the number of vertices, making it suitable for the given constraints.
