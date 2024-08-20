# 37. Sudoku Solver

To solve a Sudoku puzzle programmatically, we can use a backtracking algorithm. The idea is to try placing digits in empty cells one by one and recursively attempt to solve the puzzle. If a placement leads to an invalid board, we backtrack by removing the digit and trying the next possibility.

Here is the Python implementation:

```python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        def is_valid(board, row, col, num):
            # Check if the number exists in the current row
            for i in range(9):
                if board[row][i] == num:
                    return False
            # Check if the number exists in the current column
            for i in range(9):
                if board[i][col] == num:
                    return False
            # Check if the number exists in the current 3x3 box
            start_row, start_col = 3 * (row // 3), 3 * (col // 3)
            for i in range(3):
                for j in range(3):
                    if board[start_row + i][start_col + j] == num:
                        return False
            return True

        def solve(board):
            for row in range(9):
                for col in range(9):
                    if board[row][col] == '.':
                        for num in map(str, range(1, 10)):
                            if is_valid(board, row, col, num):
                                board[row][col] = num
                                if solve(board):  # Recurse
                                    return True
                                board[row][col] = '.'  # Backtrack
                        return False
            return True

        solve(board)
```

### Explanation:

1. **`is_valid(board, row, col, num)`**:
   - Checks if placing the number `num` at position `(row, col)` is valid according to Sudoku rules.
   - It verifies that `num` does not already exist in the same row, column, or 3x3 sub-box.

2. **`solve(board)`**:
   - This is the core recursive function that attempts to solve the Sudoku board.
   - It iterates through each cell on the board. When it finds an empty cell (denoted by `'.'`), it tries all possible digits (`'1'` to `'9'`).
   - If placing a digit is valid, it places the digit and recursively calls `solve` to attempt to solve the rest of the board.
   - If placing the digit leads to an invalid board, it backtracks by removing the digit (setting the cell back to `'.'`) and trying the next possibility.
   - The function returns `True` when the board is completely solved and `False` if it is impossible to fill a particular cell.

3. **Main Execution**:
   - The `solveSudoku` method starts the backtracking process by calling `solve(board)`. Since the problem guarantees that there is exactly one solution, the method directly modifies the `board` in place to solve the puzzle.

### Example Usage:

```python
board = [["5","3",".",".","7",".",".",".","."],
         ["6",".",".","1","9","5",".",".","."],
         [".","9","8",".",".",".",".","6","."],
         ["8",".",".",".","6",".",".",".","3"],
         ["4",".",".","8",".","3",".",".","1"],
         ["7",".",".",".","2",".",".",".","6"],
         [".","6",".",".",".",".","2","8","."],
         [".",".",".","4","1","9",".",".","5"],
         [".",".",".",".","8",".",".","7","9"]]

solution = Solution()
solution.solveSudoku(board)

for row in board:
    print(row)
```

### Output:
```python
['5', '3', '4', '6', '7', '8', '9', '1', '2']
['6', '7', '2', '1', '9', '5', '3', '4', '8']
['1', '9', '8', '3', '4', '2', '5', '6', '7']
['8', '5', '9', '7', '6', '1', '4', '2', '3']
['4', '2', '6', '8', '5', '3', '7', '9', '1']
['7', '1', '3', '9', '2', '4', '8', '5', '6']
['9', '6', '1', '5', '3', '7', '2', '8', '4']
['2', '8', '7', '4', '1', '9', '6', '3', '5']
['3', '4', '5', '2', '8', '6', '1', '7', '9']
```

This solution effectively solves the given Sudoku puzzle by filling in the empty cells according to Sudoku rules, ensuring each row, column, and 3x3 sub-grid contains all digits from 1 to 9 without repetition.
