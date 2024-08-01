# [1130. Minimum Cost Tree From Leaf Values](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/description/)

1. **Binary Tree Constraints**:
   - Each node has either 0 or 2 children.
   - The leaves of the tree are given by the `arr` array, in that exact order, when performing an in-order traversal.

2. **Node Values**:
   - Each non-leaf node's value is the product of the largest leaf value in its left and right subtree.

3. **Objective**:
   - Minimize the sum of values of all non-leaf nodes in the tree.

## Greedy Approach

The idea is to iteratively choose the smallest product possible at each step by pairing adjacent values in the array. By continuously merging smaller adjacent values, we aim to minimize the overall sum of non-leaf nodes.

## Intuition

1. **Stack Usage**: Use a stack to maintain a decreasing order of elements. This helps in determining the nearest smaller values to pair for calculating products.
2. **Merge Leaves**: Whenever two adjacent leaves (values in the array) are merged, choose the smaller of the two as one leaf to minimize the product value when combined with adjacent larger numbers.

### Steps

1. **Initialize a Stack**: Start with an empty stack and a result variable initialized to 0.
2. **Iterate through the Array**: 
   - For each value, while the stack is not empty and the current value is greater than or equal to the top of the stack:
     - Pop the top of the stack and calculate the product of this value with the minimum of the current stack top and the current value.
     - Add this product to the result.
   - Push the current value onto the stack.
3. **Finalize Stack**: If there are remaining values in the stack, they need to be paired. Continue popping from the stack and calculating the product with the next top value until one element remains.

This approach ensures that at each merge step, the smallest product is added to the result, thereby minimizing the total non-leaf node sum.

## Code Implementation

```python
class Solution:
    def mctFromLeafValues(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
        stack = []
        result = 0
        
        for value in arr:
            while stack and stack[-1] <= value:
                mid = stack.pop()
                if stack:
                    result += mid * min(stack[-1], value)
                else:
                    result += mid * value
            stack.append(value)
        
        # Finalize any remaining pairs in the stack
        while len(stack) > 1:
            result += stack.pop() * stack[-1]
        
        return result

# Example usage
sol = Solution()
print(sol.mctFromLeafValues([6, 2, 4]))  # Output: 32
print(sol.mctFromLeafValues([4, 11]))    # Output: 44
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of `arr`. Each element is pushed and popped from the stack at most once.
- **Space Complexity**: \(O(n)\), due to the stack storage.

This solution efficiently finds the minimum possible sum of non-leaf node values by cleverly pairing values in a way that minimizes the product at each step, thus ensuring the smallest possible sum overall.
