# [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/)

To solve the problem of finding the right side view of a binary tree, we can perform a level-order traversal (also known as a breadth-first traversal) and capture the last node of each level. This approach effectively simulates the view from the right side of the tree.

### Approach

1. **Level-order Traversal**:
   - Use a queue to perform a level-order traversal of the tree.
   - For each level, keep track of the nodes encountered.
   - The last node of each level is the node visible from the right side.

2. **Edge Cases**:
   - If the tree is empty (i.e., `root` is `None`), return an empty list.

### Code Implementation

Here is a Python implementation of the described approach:

```python
from collections import deque
from typing import List, Optional

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        right_side_view = []
        queue = deque([root])

        while queue:
            level_length = len(queue)
            for i in range(level_length):
                node = queue.popleft()

                # If it's the last node in the current level, add to right side view
                if i == level_length - 1:
                    right_side_view.append(node.val)

                # Add left and then right child to the queue
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return right_side_view
```

### Explanation

- **Queue Initialization**: We initialize a queue with the root node of the tree.
- **Level Iteration**: For each level in the tree, we iterate through all nodes at that level.
- **Capture Rightmost Node**: For each level, we capture the value of the last node we encounter and add it to the `right_side_view` list.
- **Children Addition**: As we process each node, we add its left child (if present) and then its right child (if present) to the queue for the next level.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the tree. We visit each node exactly once.
- **Space Complexity**: \(O(D)\), where \(D\) is the maximum number of nodes at any level (width of the tree), which in the worst case is proportional to \(O(N)\).
