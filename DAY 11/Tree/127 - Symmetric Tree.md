# [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

To determine if a binary tree is symmetric (i.e., it is a mirror of itself around its center), we can use either a recursive or an iterative approach. Let's explore both methods.

### Recursive Approach

In a recursive approach, we can define a helper function that checks whether two subtrees are mirrors of each other. The tree is symmetric if the left subtree is a mirror reflection of the right subtree.

#### Steps

1. **Base Case**: If both subtrees are `null`, they are mirrors of each other.
2. **Recursive Case**:
   - Check if the values of the current nodes are equal.
   - Recursively check if the left subtree of the left tree is a mirror of the right subtree of the right tree and vice versa.

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
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        def isMirror(left: Optional[TreeNode], right: Optional[TreeNode]) -> bool:
            if not left and not right:
                return True
            if not left or not right:
                return False
            return (left.val == right.val and
                    isMirror(left.left, right.right) and
                    isMirror(left.right, right.left))
        
        return isMirror(root.left, root.right) if root else True

# Example usage
# Constructing the tree: root = [1,2,2,3,4,4,3]
root = TreeNode(1)
root.left = TreeNode(2, TreeNode(3), TreeNode(4))
root.right = TreeNode(2, TreeNode(4), TreeNode(3))

sol = Solution()
print(sol.isSymmetric(root))  # Output: True
```

### Iterative Approach

In an iterative approach, we use a queue (or a stack) to perform a breadth-first search (BFS). We enqueue nodes in pairs to check for symmetry.

#### Steps

1. Use a queue to store pairs of nodes.
2. Initially, enqueue the root's left and right children.
3. While the queue is not empty, dequeue two nodes at a time and:
   - If both nodes are `null`, continue.
   - If only one is `null`, return `False`.
   - Check if their values are equal.
   - Enqueue their children in a mirrored order: left's left with right's right, and left's right with right's left.

Here is the implementation:

```python
from collections import deque

class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True

        queue = deque([(root.left, root.right)])

        while queue:
            left, right = queue.popleft()
            if not left and not right:
                continue
            if not left or not right:
                return False
            if left.val != right.val:
                return False

            queue.append((left.left, right.right))
            queue.append((left.right, right.left))

        return True
```

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree, since we may need to visit each node once.
- **Space Complexity**: 
  - Recursive approach: \(O(h)\), where \(h\) is the height of the tree due to the recursive call stack. This is \(O(\log n)\) for a balanced tree and \(O(n)\) for a skewed tree.
  - Iterative approach: \(O(w)\), where \(w\) is the maximum width of the tree, as we store nodes in the queue. For a balanced tree, this is \(O(n)\) in the worst case.

Both approaches effectively determine whether a binary tree is symmetric using the properties of mirror images.
