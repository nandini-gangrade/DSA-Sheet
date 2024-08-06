# [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

To determine if a binary tree is a valid Binary Search Tree (BST), we can use a recursive approach. The key idea is to ensure that for each node, all values in the left subtree are less than the node's value, and all values in the right subtree are greater than the node's value. Additionally, this property must hold for every subtree in the tree.

### Approach

1. **Recursive Function with Bounds**:
   - We define a recursive function that takes the current node and the allowable value range for the node's value (bounded by `low` and `high`).
   - Initially, the whole tree's value range is from negative infinity to positive infinity.
   - For each node, we check if its value falls within the allowable range. If it doesn't, the tree is not a valid BST.
   - Recursively apply the same logic to the left and right subtrees, updating the allowable range accordingly:
     - The left child's value must be less than the current node's value.
     - The right child's value must be greater than the current node's value.

2. **Base Cases**:
   - An empty subtree is a valid BST by definition.

### Code Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def validate(node, low=-float('inf'), high=float('inf')):
            # An empty tree is a valid BST
            if not node:
                return True
            
            # The current node's value must be within the range
            if not (low < node.val < high):
                return False
            
            # The left subtree must be valid and all its values must be < node.val
            # The right subtree must be valid and all its values must be > node.val
            return (validate(node.left, low, node.val) and
                    validate(node.right, node.val, high))
        
        return validate(root)

# Example usage:
root1 = TreeNode(2)
root1.left = TreeNode(1)
root1.right = TreeNode(3)

root2 = TreeNode(5)
root2.left = TreeNode(1)
root2.right = TreeNode(4)
root2.right.left = TreeNode(3)
root2.right.right = TreeNode(6)

solution = Solution()
print(solution.isValidBST(root1))  # Output: True
print(solution.isValidBST(root2))  # Output: False
```

### Explanation

- **Base Case**: If the node is `None`, we return `True` since an empty tree is always a valid BST.
- **Value Check**: For each node, we check if its value is between the specified `low` and `high` bounds.
- **Recursive Calls**:
  - For the left subtree, we update the upper bound to be the current node's value.
  - For the right subtree, we update the lower bound to be the current node's value.
- **Return Result**: The tree is a valid BST if and only if both the left and right subtrees are valid BSTs under their respective bounds.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the tree. Each node is visited once.
- **Space Complexity**: \(O(N)\) in the worst case due to the recursion stack, which occurs if the tree is highly unbalanced. In the best case (a balanced tree), the space complexity is \(O(\log N)\).
