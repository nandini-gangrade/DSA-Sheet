# [Introduction to Graph Coloring](https://www.geeksforgeeks.org/graph-coloring-applications/)

Graph coloring is a classic problem in computer science and mathematics that involves assigning colors to the vertices of a graph such that no two adjacent vertices share the same color. This problem has practical applications in scheduling, register allocation in compilers, and more. Here's an overview of the concept and a backtracking algorithm to solve it.

### Key Concepts

1. **Graph Coloring**: The objective is to assign colors to the vertices of a graph so that no two adjacent vertices have the same color.

2. **Chromatic Number**: This is the smallest number of colors needed to color a graph according to the rules of graph coloring.

3. **m-Coloring Problem**: Given a graph, determine if it can be colored using at most `m` colors.

4. **NP-Complete Problem**: Determining the chromatic number of a graph is NP-complete, meaning it is computationally intensive and no efficient solution exists for all cases.

### Graph Coloring as a Decision Problem

- **Decision Problem**: Given `m` colors and a graph `G`, determine if it is possible to color `G` using at most `m` colors.

### Graph Coloring as an Optimization Problem

- **Optimization Problem**: Find the minimum number of colors required to color the graph `G`.

### Backtracking Algorithm for Graph Coloring

Backtracking is an algorithmic technique for solving problems incrementally by trying partial solutions and then abandoning them if they do not lead to a valid solution.

#### Algorithm Steps

1. **Initialize Variables**:
   - Define the number of vertices `V`.
   - Initialize a color array to store color assignments for each vertex.

2. **Recursive Function**:
   - Create a recursive function `colorGraph()` that attempts to color the graph starting from the first vertex.
   - If the current index equals the number of vertices, print the color configuration and return `true`.
   - Assign colors from 1 to `m` to the current vertex.
   - Check if the current color assignment is safe (i.e., adjacent vertices do not have the same color).
   - Recursively call `colorGraph()` for the next vertex.
   - If any recursive call returns `true`, return `true`.
   - If no color can be assigned, backtrack and return `false`.

3. **Safety Check**:
   - Implement a helper function `isSafe()` that checks if assigning a color to a vertex violates any constraints.

#### Implementation

Here is the implementation of the graph coloring problem using backtracking:

```python
def isSafe(graph, color, vertex, c):
    """Check if the current color assignment is safe for vertex."""
    for i in range(len(graph)):
        if graph[vertex][i] == 1 and color[i] == c:
            return False
    return True

def graphColoringUtil(graph, m, color, vertex):
    """Utility function to solve m coloring problem."""
    if vertex == len(graph):
        # All vertices are assigned a color
        return True

    for c in range(1, m + 1):
        # Try assigning color c to vertex
        if isSafe(graph, color, vertex, c):
            color[vertex] = c

            # Recur to assign colors to the rest of the vertices
            if graphColoringUtil(graph, m, color, vertex + 1):
                return True

            # If assigning color c doesn't lead to a solution, backtrack
            color[vertex] = 0

    return False

def graphColoring(graph, m):
    """Solve the m coloring problem."""
    color = [0] * len(graph)

    # Start from the first vertex
    if graphColoringUtil(graph, m, color, 0):
        print("Solution exists with the following color assignments:")
        print(color)
    else:
        print("No solution exists.")

# Example graph represented as an adjacency matrix
graph = [
    [0, 1, 1, 1],
    [1, 0, 1, 0],
    [1, 1, 0, 1],
    [1, 0, 1, 0]
]

m = 3  # Number of colors
graphColoring(graph, m)
```

### Explanation

- **`isSafe()` Function**: Checks if assigning a specific color to a vertex is safe.
- **`graphColoringUtil()` Function**: Recursively tries to assign colors to each vertex and backtracks if no safe color is found.
- **`graphColoring()` Function**: Initializes the process and prints the result if a valid coloring exists.

This backtracking solution is effective for small graphs but can be inefficient for larger graphs due to its exponential time complexity. For larger instances, heuristic methods or approximation algorithms are often used to find near-optimal solutions.
