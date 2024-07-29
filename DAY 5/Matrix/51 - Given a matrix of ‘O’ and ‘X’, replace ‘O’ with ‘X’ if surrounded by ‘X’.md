# [Given a matrix of ‘O’ and ‘X’, replace ‘O’ with ‘X’ if surrounded by ‘X’](https://www.geeksforgeeks.org/given-matrix-o-x-replace-o-x-surrounded-x/)

To solve the problem of replacing 'O's with 'X's if they are completely surrounded by 'X's, we can utilize a flood-fill algorithm with a depth-first search (DFS) approach. The key idea is to identify the 'O's on the boundary of the matrix and any 'O's connected to them. These 'O's should not be replaced, as they are not surrounded entirely by 'X's. We can mark these 'O's temporarily, then replace all remaining 'O's with 'X's, and finally, convert the temporary markers back to 'O's.

## Approach

1. **Mark Boundary 'O's and Connected 'O's**: Traverse the boundary of the matrix to find 'O's. For each boundary 'O', use DFS to mark it and any 'O's connected to it (change 'O' to a temporary marker, such as '-'). This step identifies 'O's that should not be replaced.

2. **Replace Internal 'O's**: Traverse the matrix again, replacing any 'O' that has not been marked with 'X'. These 'O's are entirely surrounded by 'X's.

3. **Restore Boundary 'O's**: Change the temporary markers back to 'O' to restore the boundary and connected 'O's.

## Implementation

```python
def flood_fill(matrix, i, j, target, replacement):
    # Base conditions
    if i < 0 or i >= len(matrix) or j < 0 or j >= len(matrix[0]) or matrix[i][j] != target:
        return
    
    # Replace the target character with the replacement character
    matrix[i][j] = replacement

    # Recursively apply flood fill in all 4 directions
    flood_fill(matrix, i + 1, j, target, replacement)
    flood_fill(matrix, i - 1, j, target, replacement)
    flood_fill(matrix, i, j + 1, target, replacement)
    flood_fill(matrix, i, j - 1, target, replacement)

def replace_surrounded(matrix):
    if not matrix:
        return
    
    rows, cols = len(matrix), len(matrix[0])

    # Step 1: Mark all 'O's on the boundary and connected 'O's
    for i in range(rows):
        for j in range(cols):
            if (i in [0, rows - 1] or j in [0, cols - 1]) and matrix[i][j] == 'O':
                flood_fill(matrix, i, j, 'O', '-')

    # Step 2: Replace all remaining 'O's with 'X'
    for i in range(rows):
        for j in range(cols):
            if matrix[i][j] == 'O':
                matrix[i][j] = 'X'

    # Step 3: Restore the marked 'O's
    for i in range(rows):
        for j in range(cols):
            if matrix[i][j] == '-':
                matrix[i][j] = 'O'

# Example usage
matrix = [
    ['X', 'O', 'X', 'X', 'X', 'X'],
    ['X', 'O', 'X', 'X', 'O', 'X'],
    ['X', 'X', 'X', 'O', 'O', 'X'],
    ['O', 'X', 'X', 'X', 'X', 'X'],
    ['X', 'X', 'X', 'O', 'X', 'O'],
    ['O', 'O', 'X', 'O', 'O', 'O']
]

replace_surrounded(matrix)

for row in matrix:
    print(' '.join(row))
```

### Explanation of the Code

- **Flood Fill Function**: The `flood_fill` function marks the connected 'O's starting from a boundary 'O' using a temporary marker ('-'). It recursively explores all four directions from the current cell.

- **Step 1**: We loop through the boundary rows and columns of the matrix and apply flood fill to mark all connected 'O's.

- **Step 2**: We replace any remaining 'O' with 'X' since they are surrounded entirely by 'X'.

- **Step 3**: We restore the temporarily marked 'O's back to 'O'.

## Complexity Analysis

- **Time Complexity**: \(O(M \times N)\), where \(M\) is the number of rows and \(N\) is the number of columns in the matrix. Each cell is processed at most twice (once for marking and once for restoration).

- **Space Complexity**: \(O(M \times N)\) for the recursion stack in the worst-case scenario where the flood fill algorithm could fill the entire matrix.

This approach efficiently identifies and replaces 'O's surrounded by 'X's, using DFS to ensure all connected components are appropriately marked.
