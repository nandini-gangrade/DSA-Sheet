# [628. Maximum Product of Three Numbers](https://leetcode.com/problems/maximum-product-of-three-numbers/description/)

To find the maximum product of three numbers in an integer array `nums`, we need to consider the possible combinations of numbers that can produce the maximum product. This involves taking into account both positive and negative numbers, as the product of two negative numbers is positive.

## Intuition

1. **Sorted Array Considerations**:
   - If all numbers are positive, the maximum product is simply the product of the three largest numbers.
   - If there are negative numbers, the maximum product could also be the product of the two smallest (most negative) numbers and the largest positive number. This is because multiplying two negative numbers gives a positive product.

2. **Key Observations**:
   - The product of the last three numbers in a sorted array (i.e., the three largest numbers) can be a candidate for the maximum product.
   - The product of the first two numbers (i.e., the two smallest numbers) and the largest number is another candidate.

## Approach

1. **Sort the Array**:
   - Sort the array in ascending order.

2. **Calculate Two Potential Maximum Products**:
   - Calculate the product of the last three elements.
   - Calculate the product of the first two elements and the last element.

3. **Return the Maximum**:
   - Return the maximum of the two products calculated.

## Code

```python
class Solution:
    def maximumProduct(self, nums):
        # Sort the array to find the candidates for maximum product
        nums.sort()

        # Calculate the two possible maximum products
        max_product_end = nums[-1] * nums[-2] * nums[-3]  # Product of three largest numbers
        max_product_start = nums[0] * nums[1] * nums[-1]  # Product of two smallest and largest number

        # Return the maximum of the two products
        return max(max_product_end, max_product_start)
```

## Complexity Analysis

- **Time Complexity**: \(O(n \log n)\), where \(n\) is the length of the array `nums`, due to the sorting operation.
- **Space Complexity**: \(O(1)\), if we ignore the space used by the sorting algorithm (or \(O(n)\) if the sorting algorithm's space is considered).

This approach efficiently handles the problem by leveraging sorting to identify the best candidates for the maximum product, taking into account both positive and negative numbers.
