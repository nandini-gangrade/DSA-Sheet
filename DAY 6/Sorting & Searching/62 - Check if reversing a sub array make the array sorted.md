# [Check if reversing a sub array make the array sorted](https://www.geeksforgeeks.org/check-reversing-sub-array-make-array-sorted/)

To solve the problem of determining whether reversing exactly one sub-array can make a given array sorted, we can use the following approach. We will leverage the idea of comparing the given array with its sorted version, and then check if a reversal of the identified sub-array can make the given array sorted.

## Approach

1. **Compare with Sorted Version**: First, we need to compare the given array with its sorted version to identify the discrepancies. This will help us locate the positions where the given array differs from the sorted array.

2. **Identify Mismatch Indices**: Find the first and last indices where the array differs from the sorted array. This will define the bounds of the sub-array that needs to be checked.

3. **Check Sub-array Reversal**: Check if the sub-array between these mismatch indices is in decreasing order. If it is, then reversing this sub-array should make the entire array sorted.

4. **Edge Cases**: If the array is already sorted, then the answer is "Yes" because no reversal is needed.

## Code

Here is the Python implementation of the approach:

```python
class Solution:
    def canBeSortedByReversingOneSubarray(self, arr):
        n = len(arr)
        if n <= 1:
            return "Yes"

        # Get the sorted version of the array
        sorted_arr = sorted(arr)
        
        # Find the first index where arr and sorted_arr differ
        start = 0
        while start < n and arr[start] == sorted_arr[start]:
            start += 1
        
        # If no such index is found, the array is already sorted
        if start == n:
            return "Yes"
        
        # Find the last index where arr and sorted_arr differ
        end = n - 1
        while end >= 0 and arr[end] == sorted_arr[end]:
            end -= 1
        
        # Check if the sub-array between start and end is in decreasing order
        if start < end:
            # Reverse the sub-array and check if it matches the sorted array
            reversed_subarray = arr[start:end + 1][::-1]
            if arr[:start] + reversed_subarray + arr[end + 1:] == sorted_arr:
                return "Yes"
        
        return "No"
```

## Complexity

- **Time Complexity**: 
  - Sorting the array takes \(O(n \log n)\).
  - Finding the mismatch indices takes \(O(n)\).
  - Checking if the sub-array is in decreasing order takes \(O(n)\).
  - Overall, the time complexity is \(O(n \log n)\).

- **Space Complexity**: 
  - Space complexity is \(O(n)\) due to the storage required for the sorted array and intermediate operations.
