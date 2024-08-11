# [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

To solve the problem of finding the kth smallest element in a sorted `n x n` matrix, where both rows and columns are sorted in ascending order, there are a few approaches we can consider. We'll focus on an efficient method using a binary search approach, which offers a good balance between time and space complexity.

### Approach: Binary Search on the Matrix Values

#### Steps:

1. **Binary Search on Values**:
   - We use binary search on the value range within the matrix rather than the indices. The smallest element is at the top-left corner (`matrix[0][0]`), and the largest element is at the bottom-right corner (`matrix[n-1][n-1]`).
   - The idea is to guess a value `mid` and then count how many elements in the matrix are less than or equal to `mid`.

2. **Counting Elements Less Than or Equal to Mid**:
   - We traverse the matrix and count how many elements are less than or equal to `mid`. This can be done efficiently by starting from the bottom-left corner of the matrix and moving rightwards or upwards based on comparisons with `mid`.

3. **Adjust the Search Space**:
   - Depending on the count of elements less than or equal to `mid`, adjust the binary search range:
     - If the count is less than `k`, move the search space to the right (`low = mid + 1`).
     - If the count is greater than or equal to `k`, move the search space to the left (`high = mid`).

4. **Termination**:
   - The loop continues until `low` converges to the correct kth smallest element.

### Python Implementation:

```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        n = len(matrix)
        low, high = matrix[0][0], matrix[-1][-1]
        
        def countLessEqual(mid):
            count = 0
            row, col = n - 1, 0
            
            while row >= 0 and col < n:
                if matrix[row][col] <= mid:
                    # All elements in the current row up to `col` are <= mid
                    count += (row + 1)
                    col += 1
                else:
                    row -= 1
            
            return count
        
        while low < high:
            mid = (low + high) // 2
            if countLessEqual(mid) < k:
                low = mid + 1
            else:
                high = mid
        
        return low
```

### Explanation:

1. **Binary Search on Matrix Values**:
   - The `low` and `high` pointers represent the range of potential values in the matrix. The binary search is performed within this range.
   
2. **Counting Function (`countLessEqual`)**:
   - This function counts how many numbers in the matrix are less than or equal to `mid`. It starts at the bottom-left of the matrix and works its way right and up, efficiently counting elements.

3. **Binary Search Logic**:
   - The binary search narrows down the range until `low` equals `high`, which will be the kth smallest element.

### Time and Space Complexity:

- **Time Complexity**: \(O(n \log(\text{max} - \text{min}))\), where `max` is the maximum element in the matrix and `min` is the minimum. The counting operation within each binary search iteration takes \(O(n)\).
- **Space Complexity**: \(O(1)\) — constant space is used beyond the input matrix.

### Example:

- **Input**: `matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8`
- **Process**:
  - Initial guess (`mid`) values progressively narrow down from the full range of values.
  - The algorithm identifies that 13 is the 8th smallest element by counting elements ≤ 13 and adjusting the search accordingly.

- **Output**: The output is `13`, which is the correct 8th smallest element in the matrix.

This approach efficiently finds the kth smallest element with a time complexity that is better than sorting the entire matrix, and it uses constant extra space.
