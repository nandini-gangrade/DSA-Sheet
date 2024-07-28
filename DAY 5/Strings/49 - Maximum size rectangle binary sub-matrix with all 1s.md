# [Maximum size rectangle binary sub-matrix with all 1s](https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/)

To find the maximum size rectangle binary sub-matrix with all 1s, we can leverage a well-known algorithm that involves using the concept of the "largest rectangle in histogram" problem as a subroutine. Here is a detailed explanation of how to solve this problem:

## Approach

1. **Convert the Problem**: We treat each row of the matrix as the base of a histogram, where the height of each column is the number of consecutive 1s from the row up to that point. For each row, this will give us a histogram, and the problem then reduces to finding the largest rectangle in this histogram.

2. **Use Histogram Technique**: For each row, calculate the largest rectangle that can be formed using the heights calculated from the previous rows.

3. **Iterate Through Rows**: As we iterate through each row of the matrix, update the histogram heights and use a function to calculate the largest rectangle for the current histogram.

### Steps

1. **Initialize a Height Array**: Initialize an array `heights` of the same size as the number of columns in the matrix, and fill it with zeros.

2. **Iterate Over Each Row**:
   - Update the `heights` array: For each cell in the row, if the cell contains `1`, increment the corresponding entry in `heights` by 1; otherwise, reset it to zero.
   - Use the largest rectangle in histogram algorithm to find the largest area for the current histogram represented by `heights`.

3. **Calculate Maximum Area**: Keep track of the maximum area encountered during the iterations.

### Largest Rectangle in Histogram

To find the largest rectangle in the histogram for each row, use a stack-based approach:

- Iterate through each bar in the histogram:
  - If the current bar is higher than the bar at the stack's top, push it onto the stack.
  - If the current bar is lower, pop bars from the stack until a lower height is found or the stack is empty. For each popped bar, calculate the area with the popped height as the smallest height.

## Code Implementation

```python
class Solution:
    def maximalRectangle(self, matrix):
        if not matrix:
            return 0
        
        # Number of columns
        n = len(matrix[0])
        
        # Initialize the heights array
        heights = [0] * n
        max_area = 0
        
        for row in matrix:
            for j in range(n):
                # Update the heights array
                if row[j] == '1':
                    heights[j] += 1
                else:
                    heights[j] = 0
            
            # Calculate the max area for the current histogram
            max_area = max(max_area, self.largestRectangleArea(heights))
        
        return max_area
    
    def largestRectangleArea(self, heights):
        # Add a sentinel zero at the end of heights
        heights.append(0)
        stack = [-1]
        max_area = 0
        
        for i in range(len(heights)):
            while heights[i] < heights[stack[-1]]:
                h = heights[stack.pop()]
                w = i - stack[-1] - 1
                max_area = max(max_area, h * w)
            stack.append(i)
        
        # Remove the sentinel
        heights.pop()
        
        return max_area

# Example usage:
matrix1 = [
    ["0", "1", "1", "0"],
    ["1", "1", "1", "1"],
    ["1", "1", "1", "1"],
    ["1", "1", "0", "0"]
]
matrix2 = [
    ["0", "1", "1"],
    ["1", "1", "1"],
    ["0", "1", "1"]
]

solution = Solution()
print(solution.maximalRectangle(matrix1))  # Output: 8
print(solution.maximalRectangle(matrix2))  # Output: 6
```

### Explanation of the Code

1. **maximalRectangle Method**: This method initializes the `heights` array and iterates over each row to update the histogram heights. It then calculates the maximum rectangle area for the current histogram.

2. **largestRectangleArea Method**: This method computes the largest rectangle in the histogram using a stack. It appends a sentinel value (0) to the heights array to ensure all bars are processed.

## Complexity Analysis

- **Time Complexity**: \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns. This is because we process each cell once and use the stack operations efficiently for each row.

- **Space Complexity**: \(O(n)\), where \(n\) is the number of columns, for the `heights` array and the stack used in the histogram algorithm.

This approach efficiently calculates the maximum rectangle of 1s in a binary matrix by leveraging the histogram concept and using a stack-based solution to determine the largest rectangle at each step.
