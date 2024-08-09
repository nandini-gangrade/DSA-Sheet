# [Directed Graph Cycle](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

To detect cycles in a directed graph, you can use **Kahn's Algorithm** for Topological Sorting or a DFS-based approach using a recursion stack. Here, I'll explain the code you've provided using Kahn's Algorithm, which relies on the concept of in-degrees and is well-suited for detecting cycles in directed graphs.

### Explanation:

1. **Kahn's Algorithm**: This algorithm is used for topological sorting of a directed graph. If the graph has a topological sort, it is acyclic. If not, it contains a cycle.

2. **In-Degree**: The in-degree of a vertex is the number of edges directed towards it. We calculate the in-degree for each vertex.

3. **Queue**: We use a queue to keep track of all vertices with an in-degree of zero. These vertices can be visited first in the topological sort.

4. **Process Vertices**: 
   - Dequeue a vertex from the queue and process it by decreasing the in-degree of its neighbors.
   - If any neighbor's in-degree becomes zero, enqueue it.

5. **Cycle Detection**: If the number of vertices processed equals the number of vertices in the graph, the graph is acyclic. Otherwise, it contains a cycle.

### Implementation:

Here's the implementation of the cycle detection in a directed graph using Kahn's Algorithm:

```cpp
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    bool isCyclic(int V, vector<int> adj[]) {
        vector<int> InDeg(V, 0);  // Array to store in-degrees of vertices
        
        // Calculate in-degrees of all vertices
        for (int i = 0; i < V; i++) {
            for (int neighbor : adj[i]) {
                InDeg[neighbor]++;
            }
        }

        queue<int> q;  // Queue to process vertices with zero in-degree
        int count = 0;  // Count of vertices processed

        // Enqueue all vertices with zero in-degree
        for (int i = 0; i < V; i++) {
            if (InDeg[i] == 0) {
                q.push(i);
            }
        }

        // Process each vertex in the queue
        while (!q.empty()) {
            int Node = q.front();
            q.pop();
            count++;

            // Decrease the in-degree of all neighbors of the current node
            for (int neighbor : adj[Node]) {
                InDeg[neighbor]--;
                
                // If in-degree becomes zero, add to the queue
                if (InDeg[neighbor] == 0) {
                    q.push(neighbor);
                }
            }
        }

        // If count of processed vertices equals V, the graph is acyclic
        return count != V;
    }
};
```

### Complexity Analysis:

- **Time Complexity**: \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges. We process each vertex and each edge once.

- **Space Complexity**: \(O(V)\), due to the storage of the in-degree array and the queue.

### Conclusion:

This approach efficiently detects cycles in a directed graph by leveraging the properties of topological sorting. If all vertices can be sorted topologically, the graph is acyclic. Otherwise, the graph contains at least one cycle. This method is particularly useful for large graphs due to its linear complexity.
