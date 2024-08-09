# [947. Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/)

To solve the problem of removing the largest possible number of stones from a 2D plane, we can leverage the idea of finding connected components in a graph. Each stone can be considered as a node, and an edge exists between two nodes if they share the same row or column. The key insight is that in any connected component of the graph, we can remove all stones except one.

Here is a step-by-step solution using Depth-First Search (DFS):

1. **Model the Problem as a Graph**: 
   - Each stone is a node.
   - An edge exists between two nodes if they share the same row or column.

2. **Find Connected Components**:
   - Use DFS or BFS to explore all stones connected to a given stone.
   - Count the number of connected components.

3. **Count Removable Stones**:
   - For each connected component of size `k`, we can remove `k - 1` stones.

### Implementation

Below is the Python code that implements the above idea using DFS:

```python
class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:
        from collections import defaultdict
        
        # Graph to store edges
        graph = defaultdict(list)
        
        # Create the graph
        for i, (x1, y1) in enumerate(stones):
            for j, (x2, y2) in enumerate(stones):
                if i != j and (x1 == x2 or y1 == y2):
                    graph[i].append(j)
                    graph[j].append(i)
        
        # Set to keep track of visited nodes
        visited = set()
        
        def dfs(node):
            stack = [node]
            while stack:
                curr = stack.pop()
                for neighbor in graph[curr]:
                    if neighbor not in visited:
                        visited.add(neighbor)
                        stack.append(neighbor)
        
        # Number of connected components
        num_connected_components = 0
        
        # Perform DFS for each stone
        for i in range(len(stones)):
            if i not in visited:
                visited.add(i)
                dfs(i)
                num_connected_components += 1
        
        # The maximum number of stones that can be removed
        return len(stones) - num_connected_components

# Example Usage
stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
sol = Solution()
print(sol.removeStones(stones))  # Output: 5
```

### Explanation:

1. **Graph Construction**:
   - We construct a graph where each stone is a node and edges exist between nodes if they share the same row or column.

2. **DFS Function**:
   - The `dfs` function uses a stack to perform depth-first search. It starts from a given node, explores all its connected nodes, and marks them as visited.

3. **Counting Connected Components**:
   - We iterate over all stones and use the `dfs` function to count the number of connected components. Each time we start a new DFS from an unvisited stone, we increment the count of connected components.

4. **Calculating Removable Stones**:
   - The maximum number of stones that can be removed is the total number of stones minus the number of connected components (`len(stones) - num_connected_components`).

This approach ensures that we efficiently find and count connected components, allowing us to determine the maximum number of stones that can be removed.
