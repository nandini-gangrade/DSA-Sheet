# [Find paths from corner cell to middle cell in maze](https://www.geeksforgeeks.org/find-paths-from-corner-cell-to-middle-cell-in-maze/)

The problem involves finding all possible paths from any of the four corner cells of a square maze to the middle cell, where you can move exactly `n` steps in the four cardinal directions, determined by the value at the current cell. The solution can be implemented using a backtracking approach, which explores each path and checks if it leads to the middle cell.

### Problem Breakdown
- **Input**: A square maze represented as a 2D matrix, where each cell contains a positive integer.
- **Output**: All paths from any corner of the maze to the middle cell.
- **Movement**: From a cell `(i, j)` with value `n`, you can move to `(i+n, j)`, `(i-n, j)`, `(i, j+n)`, or `(i, j-n)`.

### Approach
1. **Backtracking**:
   - Start from any of the four corners of the maze.
   - Recursively try moving in the four possible directions (up, down, left, right).
   - If you reach the middle cell, print the path.
   - Use a visited matrix to avoid revisiting cells.

2. **Base Case**:
   - If the current cell is the middle cell, record the path.

3. **Recursive Case**:
   - For each direction, check if moving `n` steps (where `n` is the value in the current cell) stays within bounds and leads to a non-visited cell. If it does, recursively explore from that new cell.

### Implementation

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to check if a cell is within the maze boundaries and not visited
bool isSafe(int x, int y, int n, vector<vector<bool>>& visited) {
    return (x >= 0 && x < n && y >= 0 && y < n && !visited[x][y]);
}

// Backtracking function to find all paths from (x, y) to the middle of the maze
void findPaths(vector<vector<int>>& maze, int x, int y, int n, vector<pair<int, int>>& path, vector<vector<bool>>& visited) {
    // Middle cell coordinates
    int mid = n / 2;

    // If we have reached the middle cell
    if (x == mid && y == mid) {
        for (auto p : path) {
            cout << "(" << p.first << ", " << p.second << ") -> ";
        }
        cout << "MID" << endl;
        return;
    }

    // Possible movements in the 4 directions
    int move = maze[x][y];

    // Mark this cell as visited
    visited[x][y] = true;
    path.push_back({x, y});

    // Move Down
    if (isSafe(x + move, y, n, visited)) {
        findPaths(maze, x + move, y, n, path, visited);
    }

    // Move Up
    if (isSafe(x - move, y, n, visited)) {
        findPaths(maze, x - move, y, n, path, visited);
    }

    // Move Right
    if (isSafe(x, y + move, n, visited)) {
        findPaths(maze, x, y + move, n, path, visited);
    }

    // Move Left
    if (isSafe(x, y - move, n, visited)) {
        findPaths(maze, x, y - move, n, path, visited);
    }

    // Backtrack: unmark this cell as visited and remove it from the path
    visited[x][y] = false;
    path.pop_back();
}

int main() {
    vector<vector<int>> maze = {
        {3, 5, 4, 4, 7, 3, 4, 6, 3},
        {6, 7, 5, 6, 6, 2, 6, 6, 2},
        {3, 3, 4, 3, 2, 5, 4, 7, 2},
        {6, 5, 5, 1, 2, 3, 6, 5, 6},
        {3, 3, 4, 3, 0, 1, 4, 3, 4},
        {3, 5, 4, 3, 2, 2, 3, 3, 5},
        {3, 5, 4, 3, 2, 6, 4, 4, 3},
        {3, 5, 1, 3, 7, 5, 3, 6, 4},
        {6, 2, 4, 3, 4, 5, 4, 5, 1}
    };

    int n = maze.size();
    vector<vector<bool>> visited(n, vector<bool>(n, false));
    vector<pair<int, int>> path;

    // Start from all four corners
    findPaths(maze, 0, 0, n, path, visited);     // Top-left corner
    findPaths(maze, 0, n-1, n, path, visited);   // Top-right corner
    findPaths(maze, n-1, 0, n, path, visited);   // Bottom-left corner
    findPaths(maze, n-1, n-1, n, path, visited); // Bottom-right corner

    return 0;
}
```

### Explanation:
- **isSafe Function**: This checks if the next cell is within bounds and hasn't been visited yet.
- **findPaths Function**: This is the backtracking function that tries to explore all possible paths from the current cell to the middle cell.
- **Main Function**: This initializes the maze, starts the backtracking from all four corners, and prints all valid paths to the middle.

### Output:
For the provided example, the program will output all valid paths from any of the four corners to the middle cell.

### Complexity:
- **Time Complexity**: The worst-case time complexity is exponential \(O(4^N)\), where \(N\) is the total number of cells in the maze. However, this is typically reduced by the constraints and pruning.
- **Space Complexity**: The space complexity is \(O(N^2)\) due to the visited matrix and the path stack.
