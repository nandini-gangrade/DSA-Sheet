# [399. Evaluate Division](https://leetcode.com/problems/evaluate-division/description/)

To solve the problem of evaluating the results of queries based on given equations and values, we can model this problem using a graph where:

- Each variable (e.g., `a`, `b`, `c`) represents a node.
- Each equation (e.g., `a / b = 2.0`) represents a directed edge between two nodes with the corresponding weight (e.g., edge `a -> b` with weight `2.0`).

We need to find the shortest path (in terms of product of weights) between nodes for each query. This problem can be efficiently solved using the **Floyd-Warshall algorithm** for finding shortest paths in weighted graphs, but given the constraints, a more tailored approach using **Depth-First Search (DFS)** or **Breadth-First Search (BFS)** with **graph traversal** would be more practical.

Here’s how we can approach the problem:

### Approach

1. **Build the Graph**:
   - Create an adjacency list where each variable points to other variables with a given weight.

2. **DFS for Query Evaluation**:
   - For each query, use DFS to find a path from the start variable to the end variable. If a path exists, compute the product of the weights along the path. If no path exists, return `-1.0`.

### Implementation Steps

1. **Graph Construction**:
   - Use a dictionary to store the adjacency list where keys are variables and values are dictionaries mapping adjacent variables to their corresponding weights.

2. **DFS for Queries**:
   - Implement a DFS function to search for the path from the start variable to the end variable while keeping track of the product of weights.

### Python Code

Here's the Python code implementing the above approach:

```python
from typing import List, Dict

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        # Build the graph
        graph = {}
        for (u, v), value in zip(equations, values):
            if u not in graph:
                graph[u] = {}
            if v not in graph:
                graph[v] = {}
            graph[u][v] = value
            graph[v][u] = 1 / value

        def dfs(start: str, end: str, visited: set) -> float:
            if start == end:
                return 1.0
            visited.add(start)
            if start not in graph:
                return -1.0
            for neighbor, weight in graph[start].items():
                if neighbor not in visited:
                    result = dfs(neighbor, end, visited)
                    if result != -1.0:
                        return result * weight
            return -1.0
        
        # Answer the queries
        result = []
        for u, v in queries:
            if u in graph and v in graph:
                result.append(dfs(u, v, set()))
            else:
                result.append(-1.0)
        
        return result
```

### Explanation

1. **Graph Construction**:
   - The adjacency list `graph` is built such that `graph[u][v]` holds the weight of the edge from `u` to `v`, and `graph[v][u]` is its reciprocal.

2. **DFS Function**:
   - The `dfs` function performs a depth-first search to find a path from `start` to `end`. It recursively explores neighbors and multiplies the weights of edges along the path. If no path is found, it returns `-1.0`.

3. **Query Processing**:
   - For each query, the function checks if both variables are present in the graph. If they are, it calls `dfs` to compute the result; otherwise, it returns `-1.0`.

This approach ensures that we handle all the given constraints efficiently and correctly compute the results for all queries.
