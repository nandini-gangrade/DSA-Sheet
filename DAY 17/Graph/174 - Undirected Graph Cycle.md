# [Undirected Graph Cycle](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

To determine if an undirected graph contains a cycle, we can use Depth First Search (DFS). The basic idea is to traverse each node and its neighbors recursively. If we encounter a node that has already been visited and is not the parent of the current node, it indicates the presence of a cycle.

Here's a step-by-step breakdown of how to implement the solution:

1. **Initialize a visited array** to keep track of the nodes we have already visited during our DFS traversal.

2. **Perform DFS traversal**:
   - For each unvisited node, initiate a DFS.
   - For each neighbor of the current node:
     - If it hasn't been visited, recursively visit it.
     - If it has been visited and is not the parent of the current node, a cycle exists.

3. **Edge Cases**:
   - If the graph is disconnected, ensure to check all connected components by starting a DFS from each unvisited node.
   
4. **Return the result**:
   - If a cycle is detected during any DFS, return `1`.
   - If no cycles are found after checking all nodes, return `0`.

Here is the complete code for checking cycles in an undirected graph:

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    // Function to detect a cycle in an undirected graph using DFS
    bool detectCycle(int node, int parent, vector<int> adj[], vector<bool> &visited) {
        // Mark the current node as visited
        visited[node] = true;

        // Iterate through all adjacent nodes
        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                // Recursively visit the unvisited neighbor
                if (detectCycle(neighbor, node, adj, visited)) {
                    return true;
                }
            } else if (neighbor != parent) {
                // If an adjacent node is visited and not the parent, cycle exists
                return true;
            }
        }
        return false;
    }

    // Main function to check for a cycle in the graph
    bool isCycle(int V, vector<int> adj[]) {
        vector<bool> visited(V, false);

        // Check each vertex for a cycle
        for (int i = 0; i < V; ++i) {
            if (!visited[i]) {
                if (detectCycle(i, -1, adj, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

### Explanation:

- **detectCycle Function**: This recursive function checks each node's neighbors and uses the `visited` array to determine if a cycle exists by identifying back edges (edges that connect a vertex to an ancestor in the DFS tree).

- **isCycle Function**: This function initializes the `visited` array and iterates through each vertex. It calls `detectCycle` to check for cycles in each unvisited component.

- **DFS Approach**: The algorithm uses DFS, which naturally suits this problem due to its ability to traverse all nodes and backtrack efficiently.

### Complexity:

- **Time Complexity**: \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges. Each vertex and edge is visited once during the DFS traversal.
- **Space Complexity**: \(O(V)\) for the `visited` array and the recursion stack in the worst case.

This approach efficiently determines if an undirected graph contains any cycles, leveraging DFS for a clear and concise implementation.
