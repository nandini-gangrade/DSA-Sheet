# [Bipartite Graph](https://www.geeksforgeeks.org/problems/bipartite-graph/1)

To determine whether a given graph is bipartite or not, we can use a graph traversal technique, such as BFS or DFS, to try and color the graph using two colors. A graph is bipartite if we can color the graph such that no two adjacent vertices have the same color.

### Steps to Check If a Graph is Bipartite

1. **Coloring Initialization**:
   - We initialize a `color` array where each element is set to `-1`, indicating that no vertex has been colored yet.
   - The graph can be disconnected, so we need to check each component separately.

2. **BFS/DFS Traversal**:
   - We start coloring the graph from any uncolored node (i.e., nodes with color `-1`).
   - We use BFS (or DFS) to traverse the graph, assigning alternating colors (0 and 1) to adjacent vertices.
   - If at any point, we find an adjacent vertex that already has the same color as the current vertex, the graph is not bipartite.

3. **Final Check**:
   - If we successfully color the entire graph without conflicts, it is bipartite.

### Implementation in C++

Here is the BFS-based implementation for checking if a graph is bipartite:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Solution {
public:
    bool isBipartite(int V, vector<int> adj[]) {
        // Initialize color array with -1 (uncolored)
        vector<int> color(V, -1);

        // Iterate over all vertices to handle disconnected graphs
        for (int i = 0; i < V; i++) {
            if (color[i] == -1) {  // Unvisited vertex
                // BFS starting from vertex i
                queue<int> q;
                q.push(i);
                color[i] = 0;  // Start coloring with color 0

                while (!q.empty()) {
                    int node = q.front();
                    q.pop();

                    // Visit all adjacent vertices
                    for (int neighbor : adj[node]) {
                        if (color[neighbor] == -1) {
                            // If uncolored, color it with opposite color
                            color[neighbor] = 1 - color[node];
                            q.push(neighbor);
                        } else if (color[neighbor] == color[node]) {
                            // If neighbor has the same color, it's not bipartite
                            return false;
                        }
                    }
                }
            }
        }

        // If we colored the entire graph without conflicts, it is bipartite
        return true;
    }
};

int main() {
    Solution solution;

    // Example 1: A bipartite graph
    int V1 = 4;
    vector<int> adj1[] = {
        {1, 3},
        {0, 2},
        {1, 3},
        {0, 2}
    };
    cout << solution.isBipartite(V1, adj1) << endl;  // Output: 1 (true)

    // Example 2: A non-bipartite graph
    int V2 = 3;
    vector<int> adj2[] = {
        {1, 2},
        {0, 2},
        {0, 1}
    };
    cout << solution.isBipartite(V2, adj2) << endl;  // Output: 0 (false)

    return 0;
}
```

### Explanation

- **Initialization**:
  - We create a `color` array of size `V` (number of vertices) initialized to `-1`.

- **BFS Traversal**:
  - For each vertex \(i\) that hasn't been visited, we start a BFS from that vertex.
  - We assign the starting vertex a color (say `0`) and then alternate the colors for each adjacent vertex.

- **Conflict Detection**:
  - If at any point during the BFS, we find an adjacent vertex that has the same color as the current vertex, we conclude that the graph is not bipartite and return `false`.

- **Final Return**:
  - If no conflicts are found after processing all vertices, the graph is bipartite, and we return `true`.

### Time Complexity

- **Time Complexity**: \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges.
- **Space Complexity**: \(O(V)\), due to the storage required for the `color` array and the BFS queue.
