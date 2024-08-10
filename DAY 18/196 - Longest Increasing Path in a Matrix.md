# [329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/description/)

To solve the problem of finding the length of the longest increasing path in a matrix, we can use dynamic programming with memoization combined with Depth-First Search (DFS). The idea is to explore each cell in the matrix as the starting point of a potential path and recursively search for the longest increasing path from that cell.

### Steps to Approach the Problem:

1. **DFS with Memoization**:
   - For each cell in the matrix, use DFS to explore all four possible directions (up, down, left, right).
   - To avoid recalculating the longest path starting from a cell, use a memoization table (`dp`) to store the results.
   - If the current cell has already been computed in `dp`, return the stored result instead of recalculating.

2. **Direction Arrays**:
   - Use two arrays, `dx` and `dy`, to simplify moving in the four directions. For example, moving right would correspond to `dx[1] = 0` and `dy[1] = 1`.

3. **Base Case**:
   - If moving in a direction leads to an out-of-bound index or a smaller value than the current cell's value, the path can't continue in that direction.

4. **Optimization**:
   - The memoization table helps in reducing the time complexity by preventing redundant calculations, which would otherwise lead to exponential time complexity.

5. **Final Result**:
   - Compute the maximum length by checking all cells and taking the maximum of all possible increasing paths.

### Implementation in C++:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<int>> dp;
    int rows, cols;
    vector<int> dx = {0, 0, 1, -1};
    vector<int> dy = {1, -1, 0, 0};

    int dfs(vector<vector<int>>& matrix, int x, int y) {
        if (dp[x][y] != -1) {
            return dp[x][y];
        }
        
        int maxPath = 1; // minimum path length is the cell itself
        for (int i = 0; i < 4; i++) {
            int newX = x + dx[i];
            int newY = y + dy[i];
            
            if (newX >= 0 && newX < rows && newY >= 0 && newY < cols && matrix[newX][newY] > matrix[x][y]) {
                maxPath = max(maxPath, 1 + dfs(matrix, newX, newY));
            }
        }
        
        dp[x][y] = maxPath;
        return dp[x][y];
    }

    int longestIncreasingPath(vector<vector<int>>& matrix) {
        if (matrix.empty()) return 0;

        rows = matrix.size();
        cols = matrix[0].size();
        dp = vector<vector<int>>(rows, vector<int>(cols, -1));
        
        int longestPath = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                longestPath = max(longestPath, dfs(matrix, i, j));
            }
        }
        
        return longestPath;
    }
};
```

### Explanation:

1. **Initialization**:
   - `dp` is a 2D array initialized to `-1` to denote that no cell has been computed yet.
   - `dx` and `dy` arrays are used for moving in the four directions (right, left, down, up).

2. **DFS Function**:
   - For each cell `(x, y)`, the DFS function recursively checks all four directions to find the longest path starting from that cell.
   - If a valid longer path is found, it updates the `maxPath` for that cell.
   - The result is stored in `dp[x][y]` to avoid recomputation.

3. **Final Computation**:
   - The function `longestIncreasingPath` iterates over all cells in the matrix and computes the longest path starting from each cell using the `dfs` function.
   - The maximum of these paths is returned as the final result.

### Time and Space Complexity:

- **Time Complexity**: \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns. Each cell is visited once and the result is stored.
- **Space Complexity**: \(O(m \times n)\) for the `dp` array used to store intermediate results.

This solution efficiently finds the longest increasing path in the matrix using DFS with memoization, ensuring that each cell is processed only once.
