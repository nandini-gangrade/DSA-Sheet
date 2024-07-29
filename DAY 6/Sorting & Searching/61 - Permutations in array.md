# [Permutations in array](https://www.geeksforgeeks.org/problems/permutations-in-array1747/1)

Given two arrays `a` and `b` of equal size `N`, and an integer `K`, determine if it is possible to permute both arrays such that for every index `i`, the sum of `a[i]` and `b[i]` is greater than or equal to `K`. Return `True` if such a permutation exists, otherwise return `False`.

## Intuition
To ensure that the sum of corresponding elements from the two arrays is always greater than or equal to `K`, we need to match the largest possible values from one array with the smallest values from the other array. By doing so, we maximize the chances that their sums will be sufficient.

## Approach

1. **Sort Array `a` in Ascending Order**: This allows the smallest values of `a` to be tested with the largest values of `b`.
2. **Sort Array `b` in Descending Order**: This maximizes the values in `b` that are paired with the values from `a`.
3. **Check Each Pair**: For each index `i`, verify if the sum of `a[i]` and `b[i]` is at least `K`. If all pairs satisfy this condition, return `True`. If any pair fails, return `False`.

## Code

```python
class Solution:
    def isPossible(self, a, b, n, k):
        # Sort array a in ascending order
        a.sort()
        # Sort array b in descending order
        b.sort(reverse=True)
        
        # Check if each pair meets the condition
        for i in range(n):
            if a[i] + b[i] < k:
                return False
        
        return True
```

## Complexity

- **Time Complexity**: 
  - Sorting both arrays takes \(O(N \log N)\) time.
  - Checking each pair takes \(O(N)\) time.
  - Overall, the time complexity is \(O(N \log N)\).

- **Space Complexity**: 
  - The space complexity is \(O(1)\) for the sorting operation if we consider in-place sorting. No extra space beyond the input arrays is used.
