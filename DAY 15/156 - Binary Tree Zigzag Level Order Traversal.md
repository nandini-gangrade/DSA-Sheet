# [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/)

To solve the problem of zigzag level order traversal of a binary tree, we need to traverse the tree in a level-wise manner, but alternate the order of traversal for each level. This means traversing the first level from left to right, the second level from right to left, the third level from left to right again, and so on.

### Approach

1. **Level Order Traversal with Zigzag**:
   - We will perform a level order traversal using a queue.
   - For each level, we will maintain a list to store the values of nodes at that level.
   - We will alternate the order of adding node values to this list. For even-indexed levels (0, 2, 4,...), we add nodes from left to right, and for odd-indexed levels (1, 3, 5,...), we add nodes from right to left.

2. **Use a Flag to Track Order**:
   - Use a boolean flag to keep track of the order in which we should add node values at each level. Flip this flag at the end of processing each level.

3. **Queue Operations**:
   - Use a queue to facilitate the level order traversal.
   - For each node, enqueue its children (left and right) into the queue.

4. **Edge Case**:
   - If the root is null, simply return an empty list.

### Code

```python
from collections import deque

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def zigzagLevelOrder(self, root: TreeNode):
        if not root:
            return []
        
        results = []
        queue = deque([root])
        left_to_right = True
        
        while queue:
            level_size = len(queue)
            level_nodes = deque()
            
            for _ in range(level_size):
                node = queue.popleft()
                if left_to_right:
                    level_nodes.append(node.val)
                else:
                    level_nodes.appendleft(node.val)
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            results.append(list(level_nodes))
            left_to_right = not left_to_right
        
        return results
```

### Explanation

- **Initialization**: 
  - Start with the root node in the queue. 
  - `left_to_right` is set to `True` initially to indicate the traversal direction for the first level.

- **Traversal**:
  - For each level, determine the number of nodes at that level (`level_size`).
  - Use a deque (`level_nodes`) to store node values, allowing easy appending to the front or back depending on the current direction (`left_to_right`).

- **Direction Control**:
  - After processing each level, toggle the `left_to_right` flag to change the traversal direction for the next level.

- **Return the Results**:
  - Append the list representation of `level_nodes` to `results` after processing each level.

### Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree, because each node is processed exactly once.
- **Space Complexity**: \(O(n)\), for storing the results and the queue, which in the worst case (a complete binary tree) can store about half of the nodes at the last level.
