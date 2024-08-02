# [Maximum of minimum for every window size](https://www.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size3453/1)

To solve this problem, we need to find the maximum of minimums for every possible window size in the array. This means for each window size \( k \) (ranging from 1 to \( N \)), we need to determine the minimum value of all possible subarrays of that size and then find the maximum of these minimum values.

### Approach

1. **Calculate Previous and Next Smaller Elements:**
   - For each element in the array, determine the index of the previous smaller element (`left_array`) and the next smaller element (`right_array`). This allows us to determine the maximum window size for which the element is the minimum.
   - Use a stack to efficiently compute these indices in linear time.

2. **Determine the Maximum of Minimums:**
   - For each element, calculate the length of the window where it is the minimum. Update the result array where the index represents the window size, storing the maximum minimum value for each window size.
   - Traverse the result array to fill any missing values by propagating maximum values backward to ensure that smaller window sizes have the maximum minimum value possible.

### Implementation

```python
def maxOfMin(arr, n):
    # Initialize arrays to store the previous and next smaller elements for each element in the array.
    left_array = [-1] * n
    right_array = [n] * n

    # Create a stack to store indices of elements in the array.
    stack = []

    # Calculate the previous smaller element for each element in the array.
    for i in range(n):
        while stack and arr[stack[-1]] >= arr[i]:
            stack.pop()
        if stack:
            left_array[i] = stack[-1]
        stack.append(i)

    # Clear the stack for the next round.
    stack = []

    # Calculate the next smaller element for each element in the array.
    for i in range(n-1, -1, -1):
        while stack and arr[stack[-1]] >= arr[i]:
            stack.pop()
        if stack:
            right_array[i] = stack[-1]
        stack.append(i)

    # Initialize the result array with zeros.
    result = [0] * (n + 1)

    # Calculate the maximum of the minimums for each window size.
    for i in range(n):
        window_size = right_array[i] - left_array[i] - 1
        result[window_size] = max(result[window_size], arr[i])

    # Fill in the gaps in the result array with larger values.
    for i in range(n-1, 0, -1):
        result[i] = max(result[i], result[i+1])

    # Return the final result array.
    return result[1:]

# Example usage:
arr1 = [10, 20, 30, 50, 10, 70, 30]
n1 = len(arr1)
print(maxOfMin(arr1, n1))  # Output: [70, 30, 20, 10, 10, 10, 10]

arr2 = [10, 20, 30]
n2 = len(arr2)
print(maxOfMin(arr2, n2))  # Output: [30, 20, 10]
```

### Complexity Analysis

- **Time Complexity:** \(O(N)\) for processing the previous and next smaller elements and constructing the result array.
- **Space Complexity:** \(O(N)\) for the auxiliary arrays (`left_array`, `right_array`, `result`) and the stack.

This approach efficiently determines the maximum of minimums for each window size using a combination of stack-based techniques for processing the array elements and direct manipulation of indices for result computation.
