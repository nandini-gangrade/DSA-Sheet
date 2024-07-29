# [Find Pair Given Difference](https://www.geeksforgeeks.org/problems/find-pair-given-difference1559/1)

Given an array `arr` of size `n` and an integer `x`, return `1` if there exists a pair of elements in the array whose absolute difference is `x`. Otherwise, return `-1`.

## Intuition

1. **Absolute Difference**:
   - We need to find if there exists a pair `(a, b)` in the array such that `|a - b| = x`.

2. **Optimal Search**:
   - Using a brute-force approach to check each pair in the array would be too slow, especially for large arrays. Thus, we need a more efficient approach.

## Approach

1. **Use a Hash Map**:
   - **Hash Map for Tracking**:
     - Create a hash map (or dictionary) to keep track of the elements that have been seen so far. This will allow us to quickly check if a required element exists.
   
2. **Handling Special Case**:
   - **When `x = 0`**:
     - We need to find if there are any duplicate elements in the array, as the absolute difference between two same numbers is zero.

3. **Finding the Pair**:
   - For each element in the array, calculate the required value (`key + x`).
   - Check if this required value exists in the hash map. If it does, return `1`.

## Code

```python
from typing import List

class Solution:
    def findPair(self, n: int, x: int, arr: List[int]) -> int:
        # Step 1: Create a dictionary to count occurrences of each element
        count_map = {}
        for num in arr:
            if num in count_map:
                count_map[num] += 1
            else:
                count_map[num] = 1
        
        # Step 2: Check for pairs
        # Special case when x is 0, check for duplicates
        if x == 0:
            for key, value in count_map.items():
                if value > 1:
                    return 1
            return -1
        
        # Step 3: Find if there exists a pair with the absolute difference x
        for key in count_map:
            required_val = key + x
            # Check if the required value exists in the map
            if required_val in count_map:
                return 1
        
        # If no such pair is found, return -1
        return -1

# Example usage
sol = Solution()
print(sol.findPair(6, 78, [5, 20, 3, 2, 5, 80]))  # Output: 1
print(sol.findPair(5, 45, [90, 70, 20, 80, 50])) # Output: -1
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\)
  - Building the hash map takes \(O(n)\) time.
  - Checking each element and its required pair also takes \(O(n)\) time.

- **Space Complexity**: \(O(n)\)
  - We use additional space to store the elements in the hash map.

This approach ensures that we efficiently find whether a pair with the given absolute difference exists in the array, handling large inputs effectively.
