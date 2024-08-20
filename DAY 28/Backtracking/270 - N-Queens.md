# [51. N-Queens](https://leetcode.com/problems/n-queens/description/)

To solve the N-Queens problem, we need to place `n` queens on an `n x n` chessboard such that no two queens can attack each other. This means that no two queens can share the same row, column, or diagonal.

We can approach this problem using backtracking. Here is the Python code for solving the N-Queens problem:

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        def is_safe(row, col):
            # Check if it's safe to place the queen at board[row][col]
            for i in range(row):
                if board[i][col] == 'Q':  # Check column
                    return False
                if col - (row - i) >= 0 and board[i][col - (row - i)] == 'Q':  # Check left diagonal
                    return False
                if col + (row - i) < n and board[i][col + (row - i)] == 'Q':  # Check right diagonal
                    return False
            return True
        
        def solve(row):
            if row == n:
                result.append([''.join(row) for row in board])
                return
            
            for col in range(n):
                if is_safe(row, col):
                    board[row][col] = 'Q'  # Place the queen
                    solve(row + 1)  # Move on to the next row
                    board[row][col] = '.'  # Backtrack
        
        result = []
        board = [['.' for _ in range(n)] for _ in range(n)]  # Initialize the board with empty spaces
        solve(0)  # Start solving from the first row
        return result
```

### Explanation:
1. **Initialization**: We initialize an `n x n` board with all positions marked as `.` (empty). We also create an empty list `result` to store the solutions.

2. **Safety Check (`is_safe`)**: This function checks if placing a queen at position `(row, col)` is safe by ensuring no other queens are present in the same column or on the two diagonals that pass through `(row, col)`.

3. **Backtracking (`solve`)**: 
    - We place queens row by row, starting from the first row (`row = 0`).
    - For each column in the current row, we check if it's safe to place a queen. 
    - If it is safe, we place the queen and recursively move to the next row.
    - If we reach the last row and successfully place a queen, we add the current board configuration to the result.
    - We then backtrack by removing the queen and trying the next possible column in the current row.

4. **Return the Result**: After the backtracking process is complete, `result` will contain all valid board configurations.

### Example Usage:
```python
solution = Solution()
n = 4
print(solution.solveNQueens(n))
```

### Output:
For `n = 4`, the output will be:
```python
[
 [".Q..", "...Q", "Q...", "..Q."],
 ["..Q.", "Q...", "...Q", ".Q.."]
]
```

### Complexity:
- **Time Complexity**: The time complexity is approximately \(O(N!)\), where \(N\) is the number of queens, because we are placing `N` queens on an `N x N` board.
- **Space Complexity**: The space complexity is \(O(N^2)\) due to the board and result storage.

This solution efficiently finds all distinct ways to place `n` queens on an `n x n` chessboard such that no two queens threaten each other.
