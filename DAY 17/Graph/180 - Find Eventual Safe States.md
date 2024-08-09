# [802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/description/)

To solve the problem of finding all the safe nodes in a directed graph, we can use a strategy that involves reversing the graph and identifying terminal nodes. Here’s a detailed explanation and the solution:

### Approach and Intuition

1. **Understanding Safe Nodes**:
   - A node is considered safe if every path starting from that node eventually leads to a terminal node (a node with no outgoing edges) or another safe node.
   - Terminal nodes are inherently safe because they have no outgoing paths.

2. **Graph Reversal**:
   - To determine safe nodes, it helps to reverse the direction of the graph. In the reversed graph, a node will be part of the final safe set if it is reachable from terminal nodes.

3. **Topological Sort**:
   - Use a topological sort to process nodes. In the reversed graph, nodes with zero out-degrees (nodes with no neighbors) are processed first. This helps in identifying which nodes lead to terminal nodes in the original graph.

4. **Using BFS/Queue**:
   - Initialize a queue with terminal nodes (nodes with zero out-degrees).
   - Perform BFS to traverse and mark nodes. Nodes that can reach terminal nodes (or already marked as safe) are added to the result.

### Complexity
- **Time Complexity**: \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges. This is because we process each node and edge once.
- **Space Complexity**: \(O(V + E)\), due to the storage for the graph, reversed graph, and BFS queue.

### Code Implementation

Here’s how you can implement this approach in Python:

```python
from typing import List
from collections import deque, defaultdict

class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        n = len(graph)
        
        # Step 1: Create the reversed graph and in-degrees of each node in the reversed graph
        reversed_graph = defaultdict(list)
        out_degrees = [0] * n
        
        for node in range(n):
            for neighbor in graph[node]:
                reversed_graph[neighbor].append(node)
                out_degrees[node] += 1
        
        # Step 2: Initialize the queue with terminal nodes (nodes with 0 out-degree in reversed graph)
        queue = deque()
        for node in range(n):
            if out_degrees[node] == 0:
                queue.append(node)
        
        # Step 3: Perform BFS to find all nodes that are eventually safe
        safe_nodes = set()
        while queue:
            node = queue.popleft()
            safe_nodes.add(node)
            for neighbor in reversed_graph[node]:
                out_degrees[neighbor] -= 1
                if out_degrees[neighbor] == 0:
                    queue.append(neighbor)
        
        # Step 4: Return the sorted list of safe nodes
        return sorted(safe_nodes)
```

### Explanation of the Code

1. **Graph Reversal**:
   - Construct `reversed_graph` where for each edge `u -> v` in the original graph, `v -> u` is added in the reversed graph.
   - Calculate out-degrees for each node in the reversed graph, which represents the number of outgoing edges.

2. **Initialization**:
   - Nodes with zero out-degrees in the reversed graph are terminal nodes and are added to the BFS queue.

3. **BFS Traversal**:
   - Process nodes from the queue and mark them as safe. For each processed node, decrement the out-degree of its neighbors. If a neighbor's out-degree reaches zero, it is added to the queue.

4. **Result**:
   - Collect all safe nodes and return them in sorted order.

This approach ensures that all safe nodes are identified efficiently while respecting the problem's constraints.
