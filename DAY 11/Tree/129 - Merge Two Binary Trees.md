# [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/)

To solve the problem of merging two binary trees, we need to traverse both trees simultaneously. When nodes overlap, we sum their values. If a node exists in one tree but not in the other, we simply take the existing node.

Here's a step-by-step approach to implement the solution:

1. **Recursively traverse both trees**:
   - If both nodes exist, create a new node with the sum of their values.
   - Recursively merge the left and right children.
   - If only one node exists (either from `root1` or `root2`), use that node directly.
   - If both nodes are `None`, return `None`.

2. **Base cases**:
   - If both `root1` and `root2` are `None`, return `None`.
   - If `root1` is `None`, return `root2`.
   - If `root2` is `None`, return `root1`.

## Code

```python
# Definition for a binary tree node.
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 and not root2:
            return None
        
        # If one of the roots is None, return the other
        if not root1:
            return root2
        if not root2:
            return root1
        
        # Create a new root node with the sum of both nodes
        new_root = TreeNode(root1.val + root2.val)
        
        # Recursively merge left and right subtrees
        new_root.left = self.mergeTrees(root1.left, root2.left)
        new_root.right = self.mergeTrees(root1.right, root2.right)
        
        return new_root
```

### Explanation:

- **Recursive Merging**:
  - If both nodes exist, sum their values and recursively merge their children.
  - If one node is `None`, return the other node to maintain the existing structure.
  
- **Base Cases**:
  - Handles scenarios where one or both input nodes are `None`.

### Complexity Analysis:

- **Time Complexity**: \(O(n)\), where \(n\) is the total number of nodes in both trees. We visit each node once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree. This space is used for the recursion stack.

This approach effectively merges two binary trees into one, following the rules provided.
