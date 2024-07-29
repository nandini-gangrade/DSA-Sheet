# [Product array puzzle](https://www.geeksforgeeks.org/problems/product-array-puzzle4525/1)

To solve the problem of constructing a product array `P` such that each element `P[i]` is the product of all elements in the array `nums` except `nums[i]`, we can use a strategy that avoids division. This involves calculating the product of elements before and after each index in a single traversal.

## Approach

1. **Initialization**:
   - Create two arrays `left_products` and `right_products` of size `n` to store the cumulative products of elements to the left and right of each index, respectively.
   - Initialize a result array `result` of size `n` to store the final product values.

2. **Calculate Left Products**:
   - Traverse the `nums` array from left to right.
   - For each index `i`, `left_products[i]` is the product of all elements to the left of `i`. Initialize `left_products[0]` to `1` because there are no elements to the left of the first element.

3. **Calculate Right Products**:
   - Traverse the `nums` array from right to left.
   - For each index `i`, `right_products[i]` is the product of all elements to the right of `i`. Initialize `right_products[n-1]` to `1` because there are no elements to the right of the last element.

4. **Calculate Result**:
   - For each index `i`, the product `P[i]` is the product of `left_products[i]` and `right_products[i]`, which gives the product of all elements except `nums[i]`.

5. **Edge Case**:
   - If the array has only one element, return `[1]` since there are no other elements to consider.

## Code


```python
class Solution:
    def productExceptSelf(self, nums, n):
        # Edge case: if there's only one element
        if n == 1:
            return [1]
        
        # Initialize left and right products
        left_products = [1] * n
        right_products = [1] * n
        result = [0] * n
        
        # Calculate left products
        left_products[0] = 1  # No elements to the left of first element
        for i in range(1, n):
            left_products[i] = left_products[i - 1] * nums[i - 1]
        
        # Calculate right products
        right_products[n - 1] = 1  # No elements to the right of last element
        for i in range(n - 2, -1, -1):
            right_products[i] = right_products[i + 1] * nums[i + 1]
        
        # Calculate the result
        for i in range(n):
            result[i] = left_products[i] * right_products[i]
        
        return result

# Example usage:
solution = Solution()
print(solution.productExceptSelf([10, 3, 5, 6, 2], 5))  # Output: [180, 600, 360, 300, 900]
print(solution.productExceptSelf([12, 0], 2))          # Output: [0, 12]
```

## Complexity

- **Time Complexity**: \(O(n)\)
  - Each of the three passes through the array (`left_products`, `right_products`, and `result`) is linear in time complexity.

- **Space Complexity**: \(O(n)\)
  - We use two additional arrays (`left_products` and `right_products`) of size `n`. The space complexity can be further reduced to \(O(1)\) if we directly modify the `result` array using a single loop, but the clarity might be compromised.

This approach efficiently computes the required product array without using division, handling zeros and ensuring correct output in all cases.
