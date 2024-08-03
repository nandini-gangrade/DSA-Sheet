# [572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/description/)

To solve the problem of determining whether a binary tree `subRoot` is a subtree of another binary tree `root`, we need to check if there exists a node in `root` such that the subtree starting from that node matches `subRoot` in both structure and node values.

### Approach

1. **Check Subtree**: At each node in `root`, check if the subtree rooted at that node matches `subRoot`. We do this by using a helper function that compares the two trees starting from the given nodes.

2. **Recursive Traversal**: Traverse each node in the `root` tree recursively and invoke the subtree check function. If any node's subtree matches `subRoot`, return `True`.

3. **Helper Function**: Create a helper function that checks whether two trees are identical. This function compares the node values and recursively checks the left and right subtrees.

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
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False
        if self.isSameTree(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
    
    def isSameTree(self, s: Optional[TreeNode], t: Optional[TreeNode]) -> bool:
        if not s and not t:
            return True
        if not s or not t:
            return False
        if s.val != t.val:
            return False
        return self.isSameTree(s.left, t.left) and self.isSameTree(s.right, t.right)
```

### Explanation

- **`isSubtree` Function**: This function checks if `subRoot` is a subtree of `root` by recursively calling itself on the left and right children of `root`. If `root` is `None`, it returns `False`.

- **`isSameTree` Helper Function**: This function checks if two trees are identical by comparing the current nodes' values and recursively checking the left and right subtrees. It returns `True` if both trees are `None`, indicating the end of both trees simultaneously, otherwise checks for value equality and structure recursively.

### Complexity Analysis

- **Time Complexity**: \(O(m \times n)\), where \(m\) is the number of nodes in `root` and \(n\) is the number of nodes in `subRoot`. In the worst case, for each node in `root`, we may need to check if `subRoot` is identical to a subtree of `root`.

- **Space Complexity**: \(O(h)\), where \(h\) is the height of the `root` tree, due to the recursion stack. In the worst case (unbalanced tree), this could be \(O(m)\), but for a balanced tree, it is \(O(\log m)\).

This approach efficiently determines if `subRoot` is a subtree of `root` by leveraging recursive tree traversal and comparison.
