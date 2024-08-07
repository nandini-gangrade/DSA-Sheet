# [662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/description/)


### Python Code

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    class TreeNodePair:
        def __init__(self, node, value):
            self.node = node
            self.value = value

    def widthOfBinaryTree(self, root: TreeNode) -> int:
        if not root:
            return 0

        dq = deque([self.TreeNodePair(root, 1)])
        ans = 0

        while dq:
            max_width = dq[-1].value - dq[0].value + 1
            ans = max(ans, max_width)
            size = len(dq)

            for _ in range(size):
                tp = dq.popleft()
                temp = tp.node
                val = tp.value

                if temp.left:
                    dq.append(self.TreeNodePair(temp.left, val * 2))

                if temp.right:
                    dq.append(self.TreeNodePair(temp.right, val * 2 + 1))

        return ans
```

### Explanation

- **TreeNode Class**: Defines a basic tree node with left and right pointers.
- **TreeNodePair Class**: Helper class to store each node with its associated position index in the hypothetical complete binary tree.
- **widthOfBinaryTree Method**:
  - Checks if the root is `None` and returns `0` if so.
  - Uses a deque to perform a level-order traversal of the tree, storing `TreeNodePair` instances.
  - For each level, calculates the width using the position indices of the first and last nodes in the deque.
  - Updates the maximum width (`ans`) found so far.
  - Processes each node, adding its children to the deque with updated position indices.
  
### Complexity

- **Time Complexity**: **O(N)**, where `N` is the number of nodes in the tree, as we visit each node once.
- **Space Complexity**: **O(N)**, for the deque that holds nodes at each level, which in the worst case is proportional to the maximum width of the tree. 

This implementation should efficiently calculate the maximum width of a binary tree using a similar approach to the provided Java code.
