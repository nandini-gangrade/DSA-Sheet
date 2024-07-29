# [Minimum Swaps to Sort](https://www.geeksforgeeks.org/problems/minimum-swaps/1)

Given an array of distinct integers, find the minimum number of swaps required to sort the array in strictly increasing order.

## Approach

1. **Map Elements to Original Indices**:
   - Use a dictionary to map each element to its original index.
   
2. **Sort the Array**:
   - Sort the array and compare with the original to determine where each element should go.

3. **Cycle Detection**:
   - Traverse each element and determine the minimum number of swaps required using permutation cycles.

## Code

```python
class Solution:
    def minSwaps(self, nums):
        n = len(nums)
        if n <= 1:
            return 0
        
        # Create a list of tuples (element, index) and sort it by element
        sorted_nums = sorted((num, i) for i, num in enumerate(nums))
        
        # Create a dictionary to keep track of the original indices
        index_map = {num: i for i, num in enumerate(nums)}
        
        visited = [False] * n
        swaps = 0
        
        for i in range(n):
            # If already visited or already in the correct place
            if visited[i] or sorted_nums[i][1] == i:
                continue
            
            # Calculate the cycle size
            cycle_size = 0
            x = i
            
            while not visited[x]:
                visited[x] = True
                x = sorted_nums[x][1]
                cycle_size += 1
            
            # If there is a cycle of size `cycle_size`, it takes `cycle_size - 1` swaps
            if cycle_size > 0:
                swaps += (cycle_size - 1)
        
        return swaps
```

## Explanation

1. **Mapping Original Indices**:
   - Create a dictionary to map each element to its original index.

2. **Sorting**:
   - Sort the array and create a list of tuples where each tuple is `(element, original_index)`.

3. **Cycle Detection**:
   - Traverse the array to detect cycles in the permutation of indices.
   - For each cycle, count the number of swaps needed to sort the elements in that cycle.

## Complexity

- **Time Complexity**:
  - **Sorting**: \(O(n \log n)\)
  - **Cycle Detection**: \(O(n)\)
  - Overall: \(O(n \log n)\)

- **Space Complexity**:
  - **Auxiliary Space**: \(O(n)\) for the dictionary and visited list.

This Python code is functionally equivalent to the provided Java code and efficiently computes the minimum number of swaps required to sort the array.
