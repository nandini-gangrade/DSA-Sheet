# [Topological sort](https://www.geeksforgeeks.org/problems/topological-sort/1)

### Topological Sorting of a Directed Acyclic Graph (DAG)

Topological sorting of a Directed Acyclic Graph (DAG) is a linear ordering of its vertices such that for every directed edge `u -> v`, vertex `u` comes before `v` in the ordering. This is particularly useful in scenarios like task scheduling, course prerequisites, and other dependency resolution problems.

### Approach

To perform a topological sort, we can use two primary methods:

1. **Depth-First Search (DFS)-based approach**:
   - This method involves performing a DFS on the graph and pushing the vertices onto a stack after visiting all their adjacent vertices (i.e., when they are "finished"). The topological sort is then obtained by popping elements from the stack.

2. **Kahn’s Algorithm (BFS-based approach)**:
   - This method involves using BFS, where vertices with no incoming edges (i.e., in-degree 0) are processed first. As each vertex is processed, its neighbors’ in-degree is reduced, and if any neighbor's in-degree becomes 0, it is added to the processing queue.

Here, we will implement the **DFS-based approach** to perform the topological sort.

### DFS-Based Topological Sort Implementation

```cpp
class Solution {
public:
    // A recursive function to perform DFS and store the topological order
    void dfs(int vertex, vector<bool> &visited, stack<int> &st, vector<int> adj[]) {
        // Mark the current node as visited
        visited[vertex] = true;

        // Recur for all the vertices adjacent to this vertex
        for (int neighbor : adj[vertex]) {
            if (!visited[neighbor]) {
                dfs(neighbor, visited, st, adj);
            }
        }

        // Push current vertex to stack which stores the result
        st.push(vertex);
    }

    // Function to return the topological sort of the given graph
    vector<int> topoSort(int V, vector<int> adj[]) {
        vector<bool> visited(V, false);
        stack<int> st;

        // Perform DFS from all unvisited nodes
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(i, visited, st, adj);
            }
        }

        // Collect the vertices from the stack and store them in the result vector
        vector<int> result;
        while (!st.empty()) {
            result.push_back(st.top());
            st.pop();
        }

        return result;
    }
};
```

### Explanation

1. **DFS Function (`dfs`)**:
   - For each vertex, if it hasn't been visited, we recursively visit all its neighbors.
   - After visiting all neighbors, we push the current vertex onto the stack, indicating that it is "finished" (all dependencies are resolved).

2. **Topological Sort Function (`topoSort`)**:
   - We initialize a `visited` array to keep track of visited vertices.
   - For each vertex in the graph, if it hasn't been visited, we call the `dfs` function.
   - After processing all vertices, we pop vertices from the stack to form the topological sort.

3. **Result**:
   - The vertices are collected in reverse order from the stack to give a valid topological sort.

### Time and Space Complexity

- **Time Complexity**: `O(V + E)`, where `V` is the number of vertices and `E` is the number of edges. This is because we process each vertex and each edge once.
- **Space Complexity**: `O(V)`, due to the space required for the `visited` array and the recursion stack.

### Example

For a graph with the following adjacency list:

```cpp
int V = 6;
vector<int> adj[] = {
    {},     // Vertex 0
    {0},    // Vertex 1 -> 0
    {1},    // Vertex 2 -> 1
    {2},    // Vertex 3 -> 2
    {1, 3}, // Vertex 4 -> 1, 3
    {4}     // Vertex 5 -> 4
};
```

A valid topological sort might be: `[5, 4, 3, 2, 1, 0]`.

### Conclusion

The DFS-based topological sorting is a powerful tool in scenarios involving directed acyclic graphs (DAGs) and ensures that all dependencies are processed in the correct order.
