# [100. Same Tree](https://leetcode.com/problems/same-tree/description/)

To check if two binary trees are the same, we can use a recursive approach. We'll compare the root values of both trees and then recursively check if the left and right subtrees are identical. Here's the implementation in Python:

```python
# Definition for a binary tree node.
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # If both trees are empty, they are the same
        if not p and not q:
            return True
        # If one of the trees is empty and the other is not, they are not the same
        if not p or not q:
            return False
        # If the current nodes have different values, they are not the same
        if p.val != q.val:
            return False
        # Recursively check left and right subtrees
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

# Helper function to build a tree from a list using level order insertion
def build_tree_from_list(lst):
    if not lst:
        return None

    root = TreeNode(lst[0])
    queue = [root]
    i = 1

    while queue and i < len(lst):
        current = queue.pop(0)

        if i < len(lst) and lst[i] is not None:
            current.left = TreeNode(lst[i])
            queue.append(current.left)
        i += 1

        if i < len(lst) and lst[i] is not None:
            current.right = TreeNode(lst[i])
            queue.append(current.right)
        i += 1

    return root

# Example 1
p1 = build_tree_from_list([1, 2, 3])
q1 = build_tree_from_list([1, 2, 3])
sol = Solution()
print(sol.isSameTree(p1, q1))  # Output: True

# Example 2
p2 = build_tree_from_list([1, 2])
q2 = build_tree_from_list([1, None, 2])
print(sol.isSameTree(p2, q2))  # Output: False

# Example 3
p3 = build_tree_from_list([1, 2, 1])
q3 = build_tree_from_list([1, 1, 2])
print(sol.isSameTree(p3, q3))  # Output: False
```

### Explanation

- **Base Cases**:
  - If both `p` and `q` are `None`, the trees are identical.
  - If one is `None` and the other is not, they are not identical.
  - If the values of `p` and `q` are different, they are not identical.

- **Recursive Check**: We recursively check if the left subtree of `p` is identical to the left subtree of `q` and if the right subtree of `p` is identical to the right subtree of `q`.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the minimum number of nodes in the two trees, as we must visit each node once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree, due to the recursion stack. In the worst case, this could be \(O(n)\) if the tree is unbalanced.
