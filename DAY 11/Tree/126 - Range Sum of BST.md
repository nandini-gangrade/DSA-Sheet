# [938. Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst/description/)

To solve the problem of finding the sum of all node values within a given range \([low, high]\) in a binary search tree (BST), we can take advantage of the properties of the BST. In a BST, for any given node:

- The left subtree contains nodes with values less than the node's value.
- The right subtree contains nodes with values greater than the node's value.

### Approach

1. **Recursive In-Order Traversal**:
   - Traverse the tree in an in-order fashion (left, root, right).
   - If the current node's value is greater than `low`, recursively explore the left subtree to find more nodes in the range.
   - If the current node's value is less than `high`, recursively explore the right subtree to find more nodes in the range.
   - If the current node's value is within the range \([low, high]\), add it to the sum.

2. **Pruning**:
   - Since we are using a BST, we can prune the search space effectively:
     - Skip the left subtree if the current node's value is less than `low`.
     - Skip the right subtree if the current node's value is greater than `high`.

### Implementation

Here is a Python implementation of the approach:

```python
# Definition for a binary tree node.
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            total_sum = 0
            if low <= node.val <= high:
                total_sum += node.val
            if node.val > low:
                total_sum += dfs(node.left)
            if node.val < high:
                total_sum += dfs(node.right)
            return total_sum
        
        return dfs(root)
```

### Explanation

- **Function `rangeSumBST`**: This function initializes the recursive depth-first search (DFS) on the tree.
- **Function `dfs`**: A recursive helper function that performs in-order traversal and accumulates the sum of node values that fall within the range \([low, high]\).
  - If `node.val` is within the range, add it to `total_sum`.
  - Recursively explore the left subtree if `node.val` is greater than `low` (since potential values in the range might be there).
  - Recursively explore the right subtree if `node.val` is less than `high`.

### Complexity Analysis

- **Time Complexity**: \(O(n)\) in the worst case, where \(n\) is the number of nodes in the tree. This is because we may visit each node once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree, due to the recursive call stack. For a balanced tree, this is \(O(\log n)\); for a skewed tree, it is \(O(n)\).

This solution efficiently finds the sum of all node values within the specified range by leveraging the properties of the binary search tree.
