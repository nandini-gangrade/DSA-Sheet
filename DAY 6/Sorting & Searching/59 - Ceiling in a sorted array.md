# [Ceiling in a sorted array](https://www.geeksforgeeks.org/ceiling-in-a-sorted-array/)

To find the ceiling and floor of a value `x` in a sorted array, we can use both linear search and binary search approaches. Since the array is sorted, using binary search is more efficient with a time complexity of \(O(\log n)\), whereas linear search has a time complexity of \(O(n)\).

### Method 1: Linear Search

In this method, we iterate through the array to find the floor and ceiling of `x`.

#### Algorithm

- **Ceiling**:
  1. If `x` is less than or equal to the first element, the ceiling is the first element.
  2. Iterate through the array to find the smallest element that is greater than or equal to `x`.
  3. If no such element is found, the ceiling does not exist.

- **Floor**:
  1. If `x` is greater than or equal to the last element, the floor is the last element.
  2. Iterate through the array to find the greatest element that is less than or equal to `x`.
  3. If no such element is found, the floor does not exist.

#### Implementation

Here's how you can implement this:

```python
def findCeilAndFloorLinear(arr, x):
    n = len(arr)
    
    # Initialize floor and ceiling as None
    floor = None
    ceil = None
    
    # Linear search to find floor and ceiling
    for i in range(n):
        if arr[i] >= x:
            ceil = arr[i]
            if i > 0:
                floor = arr[i-1]
            else:
                floor = None
            break
    
    # If no ceil found, set floor as the last element
    if ceil is None:
        floor = arr[-1]
    
    return floor, ceil

# Example usage
arr = [1, 2, 8, 10, 10, 12, 19]
print(findCeilAndFloorLinear(arr, 0))  # Output: (None, 1)
print(findCeilAndFloorLinear(arr, 1))  # Output: (1, 1)
print(findCeilAndFloorLinear(arr, 5))  # Output: (2, 8)
print(findCeilAndFloorLinear(arr, 20)) # Output: (19, None)
```

### Method 2: Binary Search

This method is more efficient for large arrays due to its logarithmic time complexity.

#### Algorithm

- **Ceiling**:
  1. Use binary search to find the smallest element greater than or equal to `x`.
  2. Adjust the search boundaries based on comparisons to narrow down the position.

- **Floor**:
  1. Use binary search to find the greatest element less than or equal to `x`.
  2. Adjust the search boundaries similarly to the ceiling.

#### Implementation

```python
def findCeilAndFloorBinary(arr, x):
    n = len(arr)
    
    # Initialize floor and ceiling as None
    floor = None
    ceil = None
    
    # Binary search for ceiling
    low, high = 0, n - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == x:
            floor = arr[mid]
            ceil = arr[mid]
            break
        elif arr[mid] < x:
            floor = arr[mid]
            low = mid + 1
        else:
            ceil = arr[mid]
            high = mid - 1
    
    return floor, ceil

# Example usage
arr = [1, 2, 8, 10, 10, 12, 19]
print(findCeilAndFloorBinary(arr, 0))  # Output: (None, 1)
print(findCeilAndFloorBinary(arr, 1))  # Output: (1, 1)
print(findCeilAndFloorBinary(arr, 5))  # Output: (2, 8)
print(findCeilAndFloorBinary(arr, 20)) # Output: (19, None)
```

## Complexity Analysis

- **Linear Search**:
  - Time Complexity: \(O(n)\)
  - Space Complexity: \(O(1)\)

- **Binary Search**:
  - Time Complexity: \(O(\log n)\)
  - Space Complexity: \(O(1)\)

Binary search is preferred for larger arrays as it is much faster than linear search. It efficiently finds the positions of floor and ceiling by leveraging the sorted nature of the array.
