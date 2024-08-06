# [103. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

To perform a level-order traversal of a binary tree and return the nodes' values level by level, we can use a breadth-first search (BFS) approach, which is naturally implemented using a queue. This will allow us to visit each level of the tree from left to right.

### Approach

1. **Use a Queue**: 
   - Initialize a queue with the root node. 
   - For each level, process all nodes at that level before moving to the next level.
   - Append the values of nodes at each level to a result list.

2. **Edge Case**:
   - If the tree is empty (i.e., the root is `None`), return an empty list.

### Code Implementation

Here's a Python implementation using a queue to achieve the level-order traversal:

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
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)
            level_nodes = []

            for _ in range(level_size):
                node = queue.popleft()
                level_nodes.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            result.append(level_nodes)

        return result
```

### Explanation

- **Initialization**: A queue is initialized with the root node.
- **Level Processing**: For each level, we:
  - Determine the number of nodes at the current level.
  - Dequeue each node at that level, add its value to a temporary list for that level, and enqueue its children (left and right) if they exist.
  - Append the temporary list to the result list after processing all nodes at that level.
  
- **Loop**: Repeat the above process until the queue is empty, indicating that all levels have been processed.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the tree, because each node is processed exactly once.
- **Space Complexity**: \(O(N)\) in the worst case, which occurs when the binary tree is completely balanced, where the queue could hold up to half of the nodes at the last level.
