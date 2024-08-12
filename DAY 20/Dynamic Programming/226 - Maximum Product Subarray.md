# [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)

To find the subarray with the largest product in a given array of integers `nums`, we can employ an approach that keeps track of both the maximum and minimum products at each position. This is necessary because a negative number multiplied by the minimum product (which could be negative) might result in the maximum product.

### Approach

1. **Initialization:**
   - Initialize three variables:
     - `max_product`: the maximum product up to the current position.
     - `min_product`: the minimum product up to the current position.
     - `result`: the maximum product found so far.

2. **Iterate Through the Array:**
   - For each element in the array:
     - If the current element is negative, it can turn a minimum product into a maximum product (and vice versa), so swap `max_product` and `min_product`.
     - Update `max_product` to be the maximum of the current element itself or the product of `max_product` and the current element.
     - Update `min_product` similarly, but take the minimum.
     - Update `result` to be the maximum of `result` and `max_product`.

3. **Return the Result:**
   - After iterating through the array, `result` will contain the largest product of any subarray.

### Implementation

Here’s the Python code to implement this approach:

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        # Initialize variables
        max_product = min_product = result = nums[0]
        
        # Iterate through the array starting from the second element
        for i in range(1, len(nums)):
            # If the current number is negative, swap max_product and min_product
            if nums[i] < 0:
                max_product, min_product = min_product, max_product
            
            # Calculate max_product and min_product for the current position
            max_product = max(nums[i], max_product * nums[i])
            min_product = min(nums[i], min_product * nums[i])
            
            # Update the result with the maximum product found so far
            result = max(result, max_product)
        
        return result
```

### Explanation

- **Handling Negative Numbers:**
  - When encountering a negative number, swapping the `max_product` and `min_product` ensures that multiplying the current number by the smallest negative product might yield the largest product.
  
- **Dynamic Update:**
  - The `max_product` and `min_product` are dynamically updated to reflect the maximum and minimum products achievable at each index, which ensures that we consider every possible subarray.

### Complexity

- **Time Complexity:** O(n), where `n` is the length of the input array `nums`, because we iterate through the array only once.
- **Space Complexity:** O(1), since we are using only a constant amount of extra space.

This approach efficiently finds the maximum product subarray in linear time.
