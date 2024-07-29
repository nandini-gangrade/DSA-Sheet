# [Permute two arrays such that sum of every pair is greater or equal to K](https://www.geeksforgeeks.org/permute-two-arrays-sum-every-pair-greater-equal-k/)

To solve the problem of permuting two arrays such that the sum of their corresponding elements is greater than or equal to `k`, we can use a greedy approach. The key idea is to sort one array in ascending order and the other in descending order. This way, the smallest element from one array is paired with the largest element from the other, maximizing the chances of satisfying the condition `a[i] + b[i] >= k`.

## Approach

1. **Sort the Arrays**:
   - Sort the first array `a` in ascending order.
   - Sort the second array `b` in descending order.

2. **Check the Condition**:
   - Iterate through the arrays and check if the sum of the corresponding elements is greater than or equal to `k` for each index.
   - If for any index `i`, the condition `a[i] + b[i] < k` is violated, return "No".
   - If all indices satisfy the condition, return "Yes".

### Proof

- **Optimal Pairing**:
  - Pairing the smallest element of one array with the largest element of the other is optimal because swapping elements to get a larger value in a sorted order will not improve the sum condition.

- **Counter Example**:
  - If we sort `a` in ascending and `b` in descending order and find any index `i` such that `a[i] + b[i] < k`, any permutation involving those elements will also fail because:
    - Swapping larger elements from `a` with smaller elements from `b` or vice versa will only decrease the total sum.

## Implementation

```python
def canPermuteArrays(a, b, k):
    # Sort array a in ascending order
    a.sort()
    # Sort array b in descending order
    b.sort(reverse=True)
    
    # Check the condition for each pair
    for i in range(len(a)):
        if a[i] + b[i] < k:
            return "No"
    
    return "Yes"

# Example usage:
a1 = [2, 1, 3]
b1 = [7, 8, 9]
k1 = 10
print(canPermuteArrays(a1, b1, k1))  # Output: "Yes"

a2 = [1, 2, 2, 1]
b2 = [3, 3, 3, 4]
k2 = 5
print(canPermuteArrays(a2, b2, k2))  # Output: "No"
```

## Complexity Analysis

- **Time Complexity**: \(O(n \log n)\)
  - Sorting each array takes \(O(n \log n)\) time.
  - Checking the condition for each pair takes \(O(n)\) time.

- **Space Complexity**: \(O(1)\)
  - Sorting the arrays can be done in place, so no additional space is used beyond the input arrays.

This solution efficiently determines whether such a permutation exists by leveraging sorting to make optimal pairings, thereby achieving the desired sum condition.
