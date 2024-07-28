# [48. Rotate Image](https://leetcode.com/problems/rotate-image/description/)

To rotate a given \(n \times n\) 2D matrix by 90 degrees clockwise in-place, we can follow a two-step process: **transpose** the matrix and then **reverse** each row. This method works efficiently and meets the requirement of modifying the matrix in-place without using additional space for another matrix.

## Intuition

1. **Transpose the Matrix**: Transposing a matrix involves swapping elements at positions \((i, j)\) with those at positions \((j, i)\). This step converts rows of the matrix into columns.

2. **Reverse Each Row**: Once the matrix is transposed, we reverse each row to achieve the 90-degree clockwise rotation.

## Approach

1. **Transpose the Matrix**:
   - Loop through the matrix using two indices \(i\) and \(j\), where \(i\) is the row index and \(j\) is the column index.
   - For each element, swap it with the element at the transposed position \((j, i)\).

2. **Reverse Each Row**:
   - Iterate over each row in the matrix and reverse the elements in that row.

### Example

Let's illustrate this with an example.

#### Example 1:

- **Input**: 

  ```
  [[1, 2, 3],
   [4, 5, 6],
   [7, 8, 9]]
  ```

- **Transpose the Matrix**:

  ```
  [[1, 4, 7],
   [2, 5, 8],
   [3, 6, 9]]
  ```

- **Reverse Each Row**:

  ```
  [[7, 4, 1],
   [8, 5, 2],
   [9, 6, 3]]
  ```

- **Output**: 

  ```
  [[7, 4, 1],
   [8, 5, 2],
   [9, 6, 3]]
  ```

## Code

Here's the Python implementation:

```python
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        
        # Transpose the matrix
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        
        # Reverse each row
        for i in range(n):
            matrix[i].reverse()
```

## Complexity Analysis

- **Time Complexity**: \(O(n^2)\), where \(n\) is the number of rows (or columns) of the matrix. We need to visit each element twice: once for transposing and once for reversing.
  
- **Space Complexity**: \(O(1)\), as we are modifying the matrix in place and not using any additional data structures.

This solution efficiently rotates the matrix by 90 degrees clockwise in place using the described approach.
