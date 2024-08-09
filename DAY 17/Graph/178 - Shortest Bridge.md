# [934. Shortest Bridge](https://leetcode.com/problems/shortest-bridge/description/)

Here’s a detailed approach and implementation for solving the problem of finding the shortest bridge between two islands in a binary matrix:

### Approach and Intuition

1. **Find the First Island Using DFS:**
   - Use Depth-First Search (DFS) to locate and mark all the cells of the first island.
   - Mark these cells as visited to avoid revisiting them during the next steps. You can use a `unordered_set` to store these visited cells efficiently.
   - Convert the 2D coordinates to a single integer representation for ease of use in the BFS phase.

2. **Perform BFS to Find the Shortest Bridge:**
   - Use Breadth-First Search (BFS) starting from the cells of the first island to explore the shortest path to the second island.
   - For each cell, check its 4 possible neighbors (up, down, left, right).
   - Track the distance from the first island to the second island using the BFS level.

3. **Calculate Minimum Steps:**
   - During the BFS, if you encounter a cell that belongs to the second island, return the current BFS level. This level represents the shortest number of flips required to connect the two islands.

### Complexity

- **Time Complexity:** \(O(V + E)\), where \(V\) is the number of cells (in this case, \(m \times n\)) and \(E\) is the number of edges. DFS and BFS each run in \(O(V + E)\) time.
- **Space Complexity:** \(O(V)\) for storing visited cells and the BFS queue.

### Code Implementation

Here’s the code implementation based on the approach described:

```cpp
#include <vector>
#include <unordered_set>
#include <queue>

using namespace std;

class Solution {
public:
    int shortestBridge(vector<vector<int>>& A) {
        int m = A.size();
        int n = A[0].size();
        
        // Step 1: Find the first island using DFS and mark its cells as visited
        bool found = false;
        unordered_set<int> visited;
        for (int i = 0; i < m; i++) {
            if (found) {
                break;
            }
            for (int j = 0; j < n; j++) {
                if (A[i][j] == 1) {
                    dfs(A, i, j, visited);
                    found = true;
                    break;
                }
            }
        }
        
        // Step 2: Perform BFS to find the shortest bridge to the second island
        queue<int> q;
        for (int cell : visited) {
            q.push(cell);
        }
        
        vector<vector<int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int level = 0;
        
        while (!q.empty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int curr = q.front();
                q.pop();
                
                int currI = curr / n;
                int currJ = curr % n;
                
                for (auto dir : directions) {
                    int ni = currI + dir[0];
                    int nj = currJ + dir[1];
                    int neighbor = ni * n + nj;
                    
                    if (ni >= 0 && ni < m && nj >= 0 && nj < n && visited.find(neighbor) == visited.end()) {
                        if (A[ni][nj] == 1) {
                            return level;
                        }
                        q.push(neighbor);
                        visited.insert(neighbor);
                    }
                }
            }
            level++;
        }
        
        return -1; // No bridge found
    }

private:
    void dfs(vector<vector<int>>& A, int i, int j, unordered_set<int>& visited) {
        int m = A.size();
        int n = A[0].size();
        
        if (i < 0 || i >= m || j < 0 || j >= n || A[i][j] != 1 || visited.find(i * n + j) != visited.end()) {
            return;
        }
        
        visited.insert(i * n + j);
        vector<vector<int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        
        for (auto dir : directions) {
            int ni = i + dir[0];
            int nj = j + dir[1];
            dfs(A, ni, nj, visited);
        }
    }
};
```

### Explanation

1. **DFS Function:** 
   - Marks all the cells of the first island and stores them in a `unordered_set`.

2. **BFS Function:** 
   - Uses a queue to explore the minimum number of steps from the cells of the first island to the cells of the second island.
   - Each level in BFS represents the number of flips required to connect the two islands.

3. **Edge Cases:**
   - If no connection is found, the function returns `-1`.

This implementation ensures efficient exploration of both islands and correctly computes the shortest bridge to connect them.
