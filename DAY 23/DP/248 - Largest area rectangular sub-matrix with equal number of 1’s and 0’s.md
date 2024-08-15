# [Largest area rectangular sub-matrix with equal number of 1’s and 0’s](https://www.geeksforgeeks.org/largest-area-rectangular-sub-matrix-equal-number-1s-0s/)

The problem you're describing is about finding the largest area rectangular sub-matrix within a given binary matrix where the number of `1`s and `0`s are equal. The solution involves transforming the problem into one of finding the largest subarray with a sum of zero in a reduced 1D array, which allows us to apply efficient algorithms like the prefix sum and hashing to find the solution in \(O(n^3)\) time complexity.

### Steps to Solve:

1. **Transform the Matrix:**
   - Convert the binary matrix into a matrix where all `0`s are replaced by `-1`s. This transformation allows us to utilize the concept of finding subarrays with a sum of `0`.

2. **Iterate Over Pairs of Columns:**
   - For each pair of columns, we collapse the 2D problem into a 1D problem by considering the sum of rows between these two columns. This gives us a 1D array where we need to find the largest subarray with a sum of `0`.

3. **Find the Largest Subarray with Sum 0:**
   - Using a hash map, you can efficiently find the largest subarray with sum `0` in the reduced 1D array. The size of this subarray gives the number of rows, and the difference between the current pair of columns gives the number of columns, allowing you to compute the area of the rectangular sub-matrix.

4. **Track the Maximum Area:**
   - Keep track of the maximum area found during the iterations.

### Implementation in Python:

```python
def largestRectangle(matrix):
    if not matrix or not matrix[0]:
        return 0

    # Dimensions of the matrix
    rows = len(matrix)
    cols = len(matrix[0])

    # Initialize maximum area
    max_area = 0

    # Iterate over all pairs of columns
    for left in range(cols):
        # Create an auxiliary array to store the sum of elements
        # for each row between the current pair of columns
        temp = [0] * rows

        for right in range(left, cols):
            # Update the temp array with the sum of elements between
            # columns left and right
            for i in range(rows):
                temp[i] += 1 if matrix[i][right] == 1 else -1

            # Find the largest subarray with sum 0 in temp array
            sum_to_index = {}
            current_sum = 0
            start_index = -1
            area = 0

            for i in range(rows):
                current_sum += temp[i]

                if current_sum == 0:
                    area = (i + 1) * (right - left + 1)
                    max_area = max(max_area, area)

                if current_sum in sum_to_index:
                    area = (i - sum_to_index[current_sum]) * (right - left + 1)
                    max_area = max(max_area, area)
                else:
                    sum_to_index[current_sum] = i

    return max_area

# Example usage:
matrix = [
    [0, 0, 1, 1],
    [0, 1, 1, 0],
    [1, 1, 1, 0],
    [1, 0, 0, 1]
]

print(largestRectangle(matrix))  # Output should be 8
```

### Explanation:

1. **Transformation:** Each `0` in the matrix is treated as `-1` to make it easier to identify subarrays where the sum is `0` (which corresponds to equal numbers of `1`s and `0`s).

2. **Column Pairing:** We iterate over all possible pairs of columns `(left, right)` and reduce the matrix into a 1D array `temp` representing the sum of elements between these two columns for each row.

3. **Hash Map for Sum:** For each row's sum array `temp`, we use a hash map to find the longest subarray where the cumulative sum is `0`. If the cumulative sum is found again at a later index, it indicates that the sum between these indices is `0`.

4. **Calculate Area:** The area is calculated as the number of rows (length of subarray with sum `0`) times the number of columns (difference between the current `left` and `right` indices plus 1).

### Time Complexity:

- **O(n^3)**: We have three nested loops—two for selecting pairs of columns and one for calculating subarray sums and checking conditions. Each of these steps is optimized using hashing to keep the overall complexity manageable.

This approach efficiently solves the problem of finding the largest rectangular sub-matrix with equal numbers of `1`s and `0`s.
