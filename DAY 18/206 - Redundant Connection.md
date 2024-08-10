# [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/description/)

To solve the problem of finding a redundant connection in a graph that started as a tree and has one additional edge, we need to identify an edge that, if removed, would convert the graph back into a tree. A tree is a connected acyclic graph, so the redundant edge will be the one that forms a cycle in the graph.

### Approach

1. **Union-Find Data Structure**:
   - We'll use the Union-Find (Disjoint Set Union, DSU) data structure to efficiently determine if adding an edge creates a cycle. The Union-Find structure helps in managing and merging disjoint sets efficiently and can quickly determine if two nodes are in the same component.

2. **Processing Edges**:
   - Iterate through each edge and use Union-Find to check if adding the edge would form a cycle.
   - If the edge forms a cycle, it is the redundant edge. We need to ensure that if multiple edges could be redundant, we return the last one in the input order.

3. **Union-Find Operations**:
   - **Find**: Determine the root of the set that a particular element belongs to.
   - **Union**: Merge two sets if they are different. If they are already in the same set, it means adding the edge will create a cycle.

### Python Implementation

Here's the implementation using the Union-Find data structure:

```python
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        # Union-Find data structure
        parent = {}
        rank = {}

        def find(node):
            if parent[node] != node:
                parent[node] = find(parent[node])  # Path compression
            return parent[node]
        
        def union(node1, node2):
            root1 = find(node1)
            root2 = find(node2)
            
            if root1 != root2:
                # Union by rank
                if rank[root1] > rank[root2]:
                    parent[root2] = root1
                elif rank[root1] < rank[root2]:
                    parent[root1] = root2
                else:
                    parent[root2] = root1
                    rank[root1] += 1
                return True
            return False

        # Initialize Union-Find structure
        for edge in edges:
            for node in edge:
                if node not in parent:
                    parent[node] = node
                    rank[node] = 0
        
        # Process each edge
        for edge in edges:
            u, v = edge
            if not union(u, v):
                # If union fails, it means u and v are already connected and the edge is redundant
                return edge

# Example usage
solution = Solution()
print(solution.findRedundantConnection([[1,2],[1,3],[2,3]]))  # Output: [2,3]
print(solution.findRedundantConnection([[1,2],[2,3],[3,4],[1,4],[1,5]]))  # Output: [1,4]
```

### Explanation

1. **Union-Find Initialization**:
   - We initialize `parent` and `rank` dictionaries. Each node starts as its own parent, and rank is set to 0.

2. **Find Operation**:
   - A recursive function with path compression to keep the tree flat.

3. **Union Operation**:
   - This function merges two subsets. If the nodes are already connected (i.e., they have the same root), it means adding the current edge would create a cycle.

4. **Processing Edges**:
   - For each edge, we try to union the two nodes. If the union operation returns `False`, it indicates a cycle, and thus the edge is redundant.

5. **Returning the Result**:
   - The edge causing the cycle is returned as the redundant connection.

### Time Complexity

- **Time Complexity**: O(n * α(n)), where α is the Inverse Ackermann function, which is very slow-growing and practically constant. Given the constraints, this is efficient.

- **Space Complexity**: O(n), primarily for storing parent and rank information.

This approach efficiently finds the redundant edge and handles the constraints provided.
