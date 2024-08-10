# [Detect a negative cycle in a Graph (Bellman Ford)](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/)

To determine whether a directed weighted graph contains any negative-weight cycles, we can use the **Bellman-Ford Algorithm**. This algorithm is particularly well-suited for graphs with negative weights, as it can detect the presence of negative-weight cycles.

### Bellman-Ford Algorithm Overview

The Bellman-Ford algorithm works by iteratively relaxing all edges in the graph. It repeats this process \(V-1\) times, where \(V\) is the number of vertices in the graph. The key idea is that after \(V-1\) iterations, all shortest paths in the graph (in terms of edge weights) will have been found. If, after an additional iteration, any edge can still be relaxed, then the graph contains a negative-weight cycle.

### Steps to Detect a Negative-Weight Cycle

1. **Initialization**:
   - Initialize a distance array `dist[]` of size \(V\) (number of vertices). Set all distances to infinity (`INF`), except for the source vertex, which is set to `0`.

2. **Relax Edges**:
   - Iterate over all edges \(V-1\) times. For each edge \((u, v, \text{weight})\), update the distance to vertex \(v\) if the current known distance to \(v\) is greater than the distance to \(u\) plus the edge's weight:
     \[
     \text{dist}[v] = \min(\text{dist}[v], \text{dist}[u] + \text{weight})
     \]

3. **Check for Negative-Weight Cycles**:
   - After completing the \(V-1\) iterations, perform one more iteration over all edges. If any distance can still be updated, it indicates the presence of a negative-weight cycle.

### Example Implementation in C++

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

class Solution {
public:
    bool isNegativeWeightCycle(int n, vector<vector<int>>& edges) {
        // Step 1: Initialize distance array
        vector<int> dist(n, INT_MAX);
        dist[0] = 0; // Assuming vertex 0 as the source
        
        // Step 2: Relax edges V-1 times
        for (int i = 1; i <= n - 1; i++) {
            for (auto edge : edges) {
                int u = edge[0];
                int v = edge[1];
                int weight = edge[2];
                if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                }
            }
        }
        
        // Step 3: Check for negative-weight cycles
        for (auto edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];
            if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
                return true; // Negative cycle found
            }
        }
        
        return false; // No negative cycle found
    }
};

int main() {
    Solution solution;
    
    // Example 1
    vector<vector<int>> edges1 = {{0, 1, -1}, {1, 2, -2}, {2, 0, -3}};
    cout << (solution.isNegativeWeightCycle(3, edges1) ? "Yes" : "No") << endl; // Output: Yes
    
    // Example 2
    vector<vector<int>> edges2 = {{0, 1, 4}, {1, 2, 1}, {2, 3, 2}};
    cout << (solution.isNegativeWeightCycle(4, edges2) ? "Yes" : "No") << endl; // Output: No
    
    return 0;
}
```

### Explanation of the Code

1. **Initialization**:
   - We create a distance array `dist[]` with all values set to `INT_MAX` (representing infinity). We set the distance from the source vertex (assumed to be vertex `0`) to `0`.

2. **Relaxation**:
   - We iterate over all edges \(V-1\) times, updating the distance to each vertex if a shorter path is found via any edge.

3. **Cycle Detection**:
   - After the \(V-1\) iterations, we check if we can still relax any edge. If yes, it means there's a cycle that can decrease the distance further, which implies a negative-weight cycle.

### Time Complexity

- **Time Complexity**: \(O(V \times E)\), where \(V\) is the number of vertices and \(E\) is the number of edges.
- **Space Complexity**: \(O(V)\), for the distance array.
