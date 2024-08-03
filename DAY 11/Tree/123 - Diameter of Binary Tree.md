# [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)

To find the diameter of a binary tree, we need to determine the longest path between any two nodes in the tree. This path can pass through or be contained within any subtree of the tree. A common approach is to use depth-first search (DFS) to traverse the tree while maintaining the maximum diameter found during the traversal.

### Steps to Solve the Problem

1. **Use DFS Traversal:**
   - Traverse the tree using a recursive function that calculates the depth (or height) of each subtree.
   
2. **Calculate the Diameter at Each Node:**
   - For each node, calculate the longest path that passes through the node. This is the sum of the depths of the left and right subtrees of the node.
   
3. **Update the Maximum Diameter:**
   - Maintain a global variable to store the maximum diameter encountered during the traversal.

4. **Return the Maximum Diameter:**
   - The final value of the global variable will be the diameter of the binary tree.

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
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.max_diameter = 0
        
        def depth(node):
            if not node:
                return 0
            
            # Get the depth of the left and right subtrees
            left_depth = depth(node.left)
            right_depth = depth(node.right)
            
            # The diameter passing through this node is left_depth + right_depth
            self.max_diameter = max(self.max_diameter, left_depth + right_depth)
            
            # Return the height of the subtree rooted at this node
            return 1 + max(left_depth, right_depth)
        
        depth(root)
        return self.max_diameter
```

### Explanation

- **Depth Calculation:** The `depth` function recursively calculates the height of each subtree. It returns the height, which is `1 + max(left_depth, right_depth)`.
- **Diameter Calculation:** At each node, the potential diameter is the sum of the depths of the left and right subtrees. We update the `max_diameter` with the maximum of the current `max_diameter` and this value.
- **Global Variable:** `self.max_diameter` is used to track the maximum diameter encountered during the DFS traversal.
- **Time Complexity:** The solution has a time complexity of \(O(n)\), where \(n\) is the number of nodes in the tree, since each node is visited once.
- **Space Complexity:** The space complexity is \(O(h)\), where \(h\) is the height of the tree, due to the recursive call stack.

This approach efficiently computes the diameter by leveraging a post-order traversal to gather the necessary information at each node.
