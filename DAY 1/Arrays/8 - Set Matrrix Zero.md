# 73. Set Matrix Zeroes 
[Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/solutions/5527966/best-solution-challenge-day-1-revisewitharsh)

Given an \( m \times n \) integer matrix `matrix`, modify it such that if any element is `0`, its entire row and column are set to zeroes. The changes must be made in-place.

### Examples

**Example 1:**

- **Input:**  
  `matrix = [[1,1,1],[1,0,1],[1,1,1]]`
  
- **Output:**  
  `[[1,0,1],[0,0,0],[1,0,1]]`

- **Explanation:**  
  The zero in the second row and second column causes the entire second row and second column to be set to zeroes.

**Example 2:**

- **Input:**  
  `matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]`
  
- **Output:**  
  `[[0,0,0,0],[0,4,5,0],[0,3,1,0]]`

- **Explanation:**  
  The zeroes in the first row cause the entire first row and their respective columns to be set to zeroes.

### Constraints

- \( m == \text{matrix.length} \)
- \( n == \text{matrix}[0].\text{length} \)
- \( 1 \leq m, n \leq 200 \)
- \( -2^{31} \leq \text{matrix}[i][j] \leq 2^{31} - 1 \)

## Intuition

The problem requires setting the entire row and column to zero whenever a zero is found in the matrix. The most straightforward solution would be to keep track of all zero positions and then update the matrix accordingly. However, this approach could use \( O(m \times n) \) space, which is inefficient.

We can improve this to \( O(m + n) \) space by using two auxiliary arrays to mark the rows and columns that need to be zeroed. However, we aim to solve this problem with constant space complexity. To achieve this, we can use the first row and column of the matrix itself as markers.

## Approach

1. **Identify Zeroes Using First Row and Column:**
   - Traverse the matrix to find zeroes. Use the first row to mark which columns should be zeroed, and the first column to mark which rows should be zeroed.
   - Use two additional variables to check if the first row and column themselves need to be zeroed.

2. **Mark the Rows and Columns:**
   - For each element in the matrix that is zero, mark its corresponding row and column in the first row and first column.

3. **Zero the Marked Rows and Columns:**
   - Iterate through the matrix, and for each element, check the first row and column to see if its row or column should be zeroed.

4. **Zero the First Row and Column if Needed:**
   - Based on the additional variables, zero the first row and column if they were initially marked.

## Code

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        if not matrix or not matrix[0]:
            return
        
        m, n = len(matrix), len(matrix[0])
        first_row_has_zero = any(matrix[0][j] == 0 for j in range(n))
        first_col_has_zero = any(matrix[i][0] == 0 for i in range(m))

        # Use the first row and column as markers
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0

        # Zero out cells based on markers
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

        # Zero out the first row if needed
        if first_row_has_zero:
            for j in range(n):
                matrix[0][j] = 0

        # Zero out the first column if needed
        if first_col_has_zero:
            for i in range(m):
                matrix[i][0] = 0
```

### Complexity Analysis

- **Time Complexity:** \( O(m \times n) \)  
  The algorithm makes a constant number of passes over the matrix, resulting in linear time complexity relative to the number of elements.

- **Space Complexity:** \( O(1) \)  
  The solution uses only a fixed amount of additional space, regardless of the size of the input matrix.

This approach efficiently marks the necessary rows and columns without using extra space, meeting the problem's requirements.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/set-matrix-zeroes/solutions/5527966/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
