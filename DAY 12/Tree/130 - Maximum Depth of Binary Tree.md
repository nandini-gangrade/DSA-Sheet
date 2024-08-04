# [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

To find the maximum depth of a binary tree, we need to traverse the tree and determine the longest path from the root node to a leaf node. We can achieve this using a recursive approach (depth-first search) or an iterative approach (using a queue for breadth-first search).

### Recursive Approach (Depth-First Search)

In the recursive approach, we can traverse the tree using depth-first search and keep track of the depth at each node. The maximum depth is the larger value between the depths of the left and right subtrees, plus one for the current node.

Here's the implementation:

```python
# Definition for a binary tree node.
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        
        return max(left_depth, right_depth) + 1

# Example usage:
def build_tree_from_list(lst):
    """Helper function to build a binary tree from a list using level order insertion."""
    if not lst:
        return None

    root = TreeNode(lst[0])
    queue = [root]
    i = 1

    while queue and i < len(lst):
        current = queue.pop(0)
        
        if lst[i] is not None:
            current.left = TreeNode(lst[i])
            queue.append(current.left)
        i += 1

        if i < len(lst) and lst[i] is not None:
            current.right = TreeNode(lst[i])
            queue.append(current.right)
        i += 1

    return root

# Example 1:
root1 = build_tree_from_list([3, 9, 20, None, None, 15, 7])
sol = Solution()
print(sol.maxDepth(root1))  # Output: 3

# Example 2:
root2 = build_tree_from_list([1, None, 2])
print(sol.maxDepth(root2))  # Output: 2
```

### Iterative Approach (Breadth-First Search)

Alternatively, we can use an iterative approach with breadth-first search (BFS). This involves using a queue to traverse each level of the tree and keeping track of the depth.

Here's how you can implement it:

```python
from collections import deque

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        queue = deque([root])
        depth = 0
        
        while queue:
            level_size = len(queue)
            for _ in range(level_size):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            depth += 1
        
        return depth

# Example usage:
# Using the same `build_tree_from_list` function to construct the trees

# Example 1:
root1 = build_tree_from_list([3, 9, 20, None, None, 15, 7])
sol = Solution()
print(sol.maxDepth(root1))  # Output: 3

# Example 2:
root2 = build_tree_from_list([1, None, 2])
print(sol.maxDepth(root2))  # Output: 2
```

### Explanation:

- **Recursive Approach**:
  - We recursively calculate the maximum depth of the left and right subtrees and add 1 for the current node.
  - The base case is when the current node is `None`, in which case the depth is 0.

- **Iterative Approach**:
  - We use a queue to perform level-order traversal, incrementing the depth for each level processed.
  - For each node, we add its non-null children to the queue.

### Complexity Analysis:

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. We visit each node once.
- **Space Complexity**: 
  - Recursive approach: \(O(h)\), where \(h\) is the height of the tree, due to the recursion stack.
  - Iterative approach: \(O(w)\), where \(w\) is the maximum width of the tree (maximum number of nodes at any level), due to the queue.

Both approaches effectively determine the maximum depth of a binary tree. You can choose either method based on preference or constraints of the environment you're working in.
