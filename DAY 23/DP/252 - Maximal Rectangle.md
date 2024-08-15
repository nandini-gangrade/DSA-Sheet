# [85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)

To solve the problem of finding the largest rectangle containing only 1's in a binary matrix, we can break it down into smaller subproblems by leveraging techniques used in solving the largest rectangle in a histogram problem.

### Intuition:

The idea is to treat each row of the matrix as the base of a histogram where each column's height is determined by how many consecutive 1's are stacked vertically in that column. If we can compute the largest rectangle in the histogram for each row, then we can solve the problem for the entire matrix.

### Approach:

1. **Transform the Matrix into Histograms**:
   - For each row in the matrix, consider it as the base of a histogram. The height of each "bar" in the histogram is the number of consecutive 1's in that column up to the current row.
   - If a column contains a 0, then reset the height for that column to 0.

2. **Largest Rectangle in Histogram**:
   - For each row treated as a histogram, we calculate the largest rectangle area that can be formed using the heights of the histogram.
   - This can be efficiently solved using a stack-based approach where we maintain a stack of indices of columns, ensuring that the heights are in non-decreasing order.

3. **Maximize the Rectangle Area**:
   - As we iterate through the rows, we continuously update the heights and compute the maximal rectangle area for each histogram formed.

### Detailed Plan:

1. Iterate through each row of the matrix:
   - Update the `heights` array where each element represents the height of the histogram for the current column up to the current row.
   - For each row, compute the largest rectangle area using the `heights` array.

2. Use a helper function to compute the largest rectangle in a histogram, which can be done in \(O(n)\) time using a stack.

### Algorithm:

```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        
        # Dimensions of the matrix
        rows, cols = len(matrix), len(matrix[0])
        
        # Initialize the heights array
        heights = [0] * cols
        max_area = 0
        
        # Function to calculate the largest rectangle in histogram
        def largestRectangleArea(heights):
            stack = []
            max_area = 0
            heights.append(0)  # Append 0 to make sure we pop all bars
            for i in range(len(heights)):
                while stack and heights[i] < heights[stack[-1]]:
                    h = heights[stack.pop()]
                    w = i if not stack else i - stack[-1] - 1
                    max_area = max(max_area, h * w)
                stack.append(i)
            heights.pop()  # Restore heights array to original
            return max_area
        
        # Process each row
        for row in matrix:
            for i in range(cols):
                # Update the height if the current element is '1'
                if row[i] == '1':
                    heights[i] += 1
                else:
                    heights[i] = 0
            
            # Calculate the largest rectangle for this row's histogram
            max_area = max(max_area, largestRectangleArea(heights))
        
        return max_area
```

### Explanation of the Code:

1. **Initialization**:
   - We initialize a `heights` array to store the heights of the histogram for each column.
   - The variable `max_area` keeps track of the largest rectangle area found so far.

2. **Row-wise Processing**:
   - For each row, we update the `heights` array: if the cell contains a '1', increment the height; otherwise, reset the height to 0.
   - After updating the heights for the current row, we calculate the largest rectangle area that can be formed in this histogram using the helper function `largestRectangleArea`.

3. **Largest Rectangle in Histogram**:
   - This helper function uses a stack to maintain indices of the heights array where the heights are in non-decreasing order.
   - Whenever we encounter a smaller height, we pop the stack and calculate the area of the rectangle that can be formed using the popped height.
   - The width of the rectangle is determined by the difference between the current index and the index of the element on the top of the stack after the pop.

4. **Final Result**:
   - We continuously update the `max_area` with the largest rectangle found for each histogram.

### Time Complexity:
- **Updating Heights**: For each row, updating the heights takes \(O(cols)\), where `cols` is the number of columns in the matrix.
- **Calculating Largest Rectangle**: Calculating the largest rectangle in each histogram also takes \(O(cols)\).
- Since we do this for each row, the total time complexity is \(O(rows \times cols)\).

### Space Complexity:
- The space complexity is \(O(cols)\) for the `heights` array and the stack used in the `largestRectangleArea` function.

### Example Walkthrough:

For the input matrix:

```
matrix = [
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
```

- After processing the first row, the `heights` array is `[1, 0, 1, 0, 0]`.
  - The largest rectangle area is 1.
  
- After processing the second row, the `heights` array is `[2, 0, 2, 1, 1]`.
  - The largest rectangle area becomes 3.

- After processing the third row, the `heights` array is `[3, 1, 3, 2, 2]`.
  - The largest rectangle area becomes 6.

- After processing the fourth row, the `heights` array is `[4, 0, 0, 3, 0]`.
  - The largest rectangle area remains 6.

Thus, the final output is `6`.

### Example:

```python
matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
solution = Solution()
print(solution.maximalRectangle(matrix))  # Output: 6
```
