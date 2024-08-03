# [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)

To invert a binary tree, we need to swap the left and right children of each node in the tree. This operation can be done recursively by traversing the tree in a depth-first manner and swapping the children at each node. The inversion process will transform the tree such that the left and right subtrees of every node are interchanged.

### Steps to Invert the Binary Tree

1. **Traverse the Tree:**
   - Use a recursive function to visit each node in the tree.

2. **Swap the Children:**
   - For each node, swap its left and right child.

3. **Recurse on Subtrees:**
   - Recursively apply the inversion to the left and right subtrees.

4. **Return the Inverted Tree:**
   - The root node after the entire tree has been processed is returned as the inverted tree.

### Implementation

```python
# Definition for a binary tree node.
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        
        # Swap the left and right subtrees
        root.left, root.right = root.right, root.left
        
        # Recurse on the left and right subtrees
        self.invertTree(root.left)
        self.invertTree(root.right)
        
        return root
```

### Explanation

- **Base Case:** If the current node is `None`, return `None` since there is nothing to invert.
- **Recursive Step:** For each node, swap its left and right children. Then recursively call the `invertTree` function on both the left and right children to ensure the entire subtree is inverted.
- **Return the Root:** Finally, return the root of the tree, which now represents the root of the inverted tree.

### Complexity Analysis

- **Time Complexity:** \(O(n)\), where \(n\) is the number of nodes in the tree. We visit each node exactly once.
- **Space Complexity:** \(O(h)\), where \(h\) is the height of the tree, due to the recursion stack. In the worst case (unbalanced tree), this could be \(O(n)\), but for a balanced tree, it is \(O(\log n)\).

This solution effectively inverts the binary tree by leveraging a simple recursive strategy, swapping children at each node as it traverses the tree.
