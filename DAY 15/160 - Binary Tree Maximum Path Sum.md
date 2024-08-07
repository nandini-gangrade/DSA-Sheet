# [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)

To find the maximum path sum of any non-empty path in a binary tree, you need to consider paths that may pass through any node, not necessarily starting or ending at the root. Here’s a structured approach to solve this problem:

### Approach

1. **Recursive Traversal**:
   - Use a depth-first search (DFS) approach to traverse the binary tree.
   - At each node, calculate the maximum path sum that can be extended from this node to its left and right children.

2. **Path Sum Calculation**:
   - For each node, compute:
     - The maximum path sum including the node and extending to the left subtree.
     - The maximum path sum including the node and extending to the right subtree.
     - The maximum path sum that includes the node itself and extends through both subtrees (i.e., a path that includes both left and right children).

3. **Global Maximum**:
   - Maintain a global variable to keep track of the maximum path sum found during the traversal.

### Intuition and Explanation

1. **Max Path Sum at Node**:
   - At each node, the maximum sum can be one of the following:
     - The node’s value itself.
     - The node’s value plus the maximum path sum extending from the left child.
     - The node’s value plus the maximum path sum extending from the right child.
     - The node’s value plus the maximum path sum extending through both children (i.e., including both left and right).

2. **Global Maximum**:
   - Update the global maximum path sum whenever a higher sum is found during the traversal.

### Python Code

Here is the Python code implementing the approach:

```python
class TreeNode:
    def __init__(self, value=0, left=None, right=None):
        self.val = value
        self.left = left
        self.right = right

class Solution:
    def __init__(self):
        self.max_sum = float('-inf')
    
    def maxPathSumHelper(self, node):
        if not node:
            return 0
        
        # Compute the maximum path sum on the left and right
        left_sum = max(self.maxPathSumHelper(node.left), 0)
        right_sum = max(self.maxPathSumHelper(node.right), 0)
        
        # Calculate the maximum path sum that includes the current node
        current_sum = node.val + left_sum + right_sum
        
        # Update the global maximum path sum
        self.max_sum = max(self.max_sum, current_sum)
        
        # Return the maximum sum that can be extended to the parent
        return node.val + max(left_sum, right_sum)
    
    def maxPathSum(self, root):
        self.maxPathSumHelper(root)
        return self.max_sum

# Example Usage:
# Construct the binary tree
#       -10
#       /  \
#      9   20
#          /  \
#         15   7

root = TreeNode(-10)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)

solution = Solution()
print(solution.maxPathSum(root))  # Output: 42
```

### Explanation

1. **`maxPathSumHelper` Function**:
   - This function computes the maximum path sum that can be extended from the current node to its parent and updates the global maximum path sum.
   - It returns the maximum sum that can be extended to the parent node.

2. **`maxPathSum` Function**:
   - This function initializes the `max_sum` and starts the recursive traversal using `maxPathSumHelper`.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the tree. Each node is visited exactly once.
- **Space Complexity**: \(O(H)\), where \(H\) is the height of the tree, due to the recursion stack.

This approach efficiently computes the maximum path sum for any non-empty path in the binary tree.
