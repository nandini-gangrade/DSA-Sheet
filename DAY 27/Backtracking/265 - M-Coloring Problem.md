# [M-Coloring Problem](https://www.geeksforgeeks.org/problems/m-coloring-problem-1587115620/1)

To solve the problem of determining whether a given graph can be colored with at most \(M\) colors such that no two adjacent vertices share the same color, we can apply a **backtracking** approach. This problem is essentially the **M-coloring problem**, where we try to assign colors to all vertices of the graph and check if the assignment satisfies the adjacency constraint.

### Approach:

1. **Graph Representation**: The graph is represented by an adjacency matrix. If there is an edge between vertex \(i\) and vertex \(j\), the matrix will have a `1` at `graph[i][j]`, otherwise `0`.

2. **Backtracking**: We attempt to color each vertex starting from the first one. For each vertex, we try to assign a color and check if the assignment violates the adjacency constraint:
   - If the color assignment is valid (no adjacent vertex has the same color), we recursively move on to the next vertex.
   - If at any point we can't assign a valid color to a vertex, we backtrack (try a different color for the previous vertex).
   
3. **Termination**: 
   - If we manage to color all vertices, return `True` (1).
   - If after trying all colors for a vertex we find that no valid color can be assigned, return `False` (0).

### Key Observations:
- The graph can have a maximum of 20 vertices (\(N \leq 20\)), so an exhaustive backtracking approach will work within time limits.
- Each recursive call explores possible colorings for the remaining uncolored vertices.

### Algorithm Steps:

1. **Check Feasibility for Each Vertex**: We define a helper function that checks if it's possible to assign a color to a vertex without causing a conflict (i.e., ensuring no two adjacent vertices have the same color).

2. **Backtracking for Coloring**: Recursively attempt to color each vertex by trying all available colors (up to \(M\)).

3. **Base Case**: If all vertices are colored, return `True`.

### Code Implementation:

```python
# Helper function to check if it's safe to color the vertex with the given color
def isSafe(graph, vertex, color, colors, V):
    # Check adjacent vertices of 'vertex'
    for adj_vertex in range(V):
        if graph[vertex][adj_vertex] == 1 and colors[adj_vertex] == color:
            return False
    return True

# Function to perform backtracking to solve the graph coloring problem
def graphColoringUtil(graph, m, colors, vertex, V):
    # Base case: If all vertices are assigned a color, return True
    if vertex == V:
        return True
    
    # Try assigning different colors to the vertex
    for color in range(1, m+1):
        # Check if assigning this color is safe
        if isSafe(graph, vertex, color, colors, V):
            # Assign the color to the vertex
            colors[vertex] = color
            
            # Recursively try to color the next vertex
            if graphColoringUtil(graph, m, colors, vertex + 1, V):
                return True
            
            # If assigning color doesn't lead to a solution, backtrack
            colors[vertex] = 0
    
    # If no color can be assigned to this vertex, return False
    return False

# Main function to determine if the graph can be colored with at most M colors
def graphColoring(graph, m, V):
    # Create a list to store the colors assigned to each vertex (initially uncolored)
    colors = [0] * V
    
    # Start coloring the graph from the first vertex (vertex 0)
    if graphColoringUtil(graph, m, colors, 0, V):
        return True
    else:
        return False
```

### Explanation:

1. **isSafe()**:
   - This function checks whether assigning a particular color to a vertex would conflict with its adjacent vertices (i.e., whether any adjacent vertex already has the same color).

2. **graphColoringUtil()**:
   - This is the backtracking function that attempts to color each vertex. For each vertex, it tries all colors from `1` to `M`. If a valid coloring is found, it returns `True`. If no valid coloring is possible for a vertex, it backtracks by resetting the vertex color to `0` and trying a different color.

3. **graphColoring()**:
   - This function initializes the `colors` array (which stores the color of each vertex) and starts the backtracking process from vertex `0`.

### Example Walkthrough:

#### Example 1:
```plaintext
Input: N = 4, M = 3, Edges = {(0,1), (1,2), (2,3), (3,0), (0,2)}
```
The graph is represented as:

```plaintext
graph = [
    [0, 1, 1, 1],
    [1, 0, 1, 0],
    [1, 1, 0, 1],
    [1, 0, 1, 0]
]
```

- Start with vertex `0`, assign color `1`.
- Move to vertex `1`, assign color `2`.
- Move to vertex `2`, assign color `3`.
- Move to vertex `3`, assign color `2`.

Since all vertices are colored with different colors, the result is `True` (1).

#### Example 2:
```plaintext
Input: N = 3, M = 2, Edges = {(0,1), (1,2), (0,2)}
```
The graph is represented as:

```plaintext
graph = [
    [0, 1, 1],
    [1, 0, 1],
    [1, 1, 0]
]
```

- Start with vertex `0`, assign color `1`.
- Move to vertex `1`, assign color `2`.
- Move to vertex `2`, no valid color can be assigned (both colors `1` and `2` are used by adjacent vertices).

The result is `False` (0).

### Time Complexity:
- **Worst case**: \(O(M^N)\), where \(N\) is the number of vertices and \(M\) is the number of available colors. This is because for each vertex, we are trying out \(M\) colors.
- **Optimized case**: The pruning (backtracking) reduces the search space.

### Space Complexity:
- **Auxiliary Space**: \(O(N)\) due to the recursion stack and the `colors` array used to store the color of each vertex.

### Conclusion:
This backtracking solution efficiently determines if the graph can be colored with at most \(M\) colors while ensuring no two adjacent vertices share the same color.
