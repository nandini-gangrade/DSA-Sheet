# [907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/)

To solve the problem of finding the sum of the minimum values for every contiguous subarray of a given array, we can use an efficient algorithm leveraging the concept of "Next Greater Element" (NGE) and "Previous Greater Element" (PGE). This approach allows us to calculate the contribution of each element to the overall sum of minimums in all subarrays efficiently.

## Approach

1. **Understanding the Contribution of Each Element**:
   - For each element in the array, determine the number of subarrays for which this element is the minimum.
   - Use stacks to find out how many subarrays an element is part of where it is the minimum.

2. **Key Insight**:
   - For an element at index `i` to be the minimum in a subarray, it should be the smallest element in that subarray.
   - The element can be the minimum in several subarrays that are formed by extending to the left and right.

3. **Compute Using Stacks**:
   - Use stacks to compute the nearest smaller element to the left and right for each element.
   - The number of subarrays in which a given element is the minimum can be derived from these nearest smaller elements.

4. **Steps**:
   - Compute the distance to the nearest smaller element to the left (`left`).
   - Compute the distance to the nearest smaller element to the right (`right`).
   - For each element, its contribution to the sum is given by `arr[i] * left[i] * right[i]`.

## Implementation

```python
class Solution(object):
    def sumSubarrayMins(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
        MOD = 10**9 + 7
        n = len(arr)
        
        # Initialize stacks and arrays
        stack = []
        left = [0] * n
        right = [0] * n
        
        # Compute left boundaries for each element
        for i in range(n):
            while stack and arr[stack[-1]] >= arr[i]:
                stack.pop()
            left[i] = i + 1 if not stack else i - stack[-1]
            stack.append(i)
        
        # Clear stack for next computation
        stack = []
        
        # Compute right boundaries for each element
        for i in range(n - 1, -1, -1):
            while stack and arr[stack[-1]] > arr[i]:
                stack.pop()
            right[i] = n - i if not stack else stack[-1] - i
            stack.append(i)
        
        # Calculate the result
        result = 0
        for i in range(n):
            result = (result + arr[i] * left[i] * right[i]) % MOD
        
        return result
```

### Explanation

1. **Compute Left Boundaries**:
   - For each element, determine the number of contiguous elements on the left for which the current element is the minimum. This is done using a stack to keep track of elements and their indices.

2. **Compute Right Boundaries**:
   - Similarly, compute the number of contiguous elements on the right for which the current element is the minimum.

3. **Calculate Contribution**:
   - For each element, calculate its total contribution as the product of the element value, its left boundary, and its right boundary. Sum these contributions and take modulo \(10^9 + 7\) to handle large numbers.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the array. Each element is pushed and popped from the stack exactly once.
- **Space Complexity**: \(O(n)\) for the auxiliary arrays and stack.

This approach ensures that we handle large inputs efficiently and provide the correct result modulo \(10^9 + 7\).
