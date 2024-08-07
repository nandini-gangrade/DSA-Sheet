# [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)

To flatten a binary tree into a "linked list" in place, we can modify the tree structure so that the right child pointer points to the next node in a pre-order traversal, and the left child pointer is always `null`. This transformation can be achieved by a depth-first traversal of the tree, updating pointers as we go.

### Approach

The idea is to traverse the tree in a pre-order manner and manipulate the pointers such that the left subtree is moved to the right, and then append the original right subtree to the end of the new right subtree.

#### Steps

1. **Pre-order Traversal**: We will process each node in pre-order (node, left, right).
2. **Rightmost Node**: For each node, find the rightmost node of the left subtree.
3. **Re-link Subtrees**: 
   - Link the rightmost node of the left subtree to the original right child.
   - Move the left subtree to the right, making the left `null`.
4. **Recur or Iterate**: Repeat the process for the right child.

### Code Implementation

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def flatten(self, root: TreeNode) -> None:
        current = root
        
        while current:
            if current.left:
                # Find the rightmost node in the left subtree
                rightmost = current.left
                while rightmost.right:
                    rightmost = rightmost.right
                
                # Re-link the rightmost node to the current's right subtree
                rightmost.right = current.right
                
                # Move the left subtree to the right
                current.right = current.left
                current.left = None
            
            # Move to the next node
            current = current.right
```

### Explanation

- **Current Node**: Start with the root and iterate over each node using the `right` pointer.
- **Left Subtree Handling**: For a node with a left child:
  - Find the rightmost node of its left subtree.
  - Connect this node's `right` to the current node's `right`.
  - Move the left subtree to the right, setting the left pointer to `null`.
- **Iterate**: Continue to the next node using the updated `right` pointer.

### Complexity

- **Time Complexity**: **O(N)**, where `N` is the number of nodes in the tree. Each node is visited once.
- **Space Complexity**: **O(1)**, since we are modifying the tree in place without using extra space.

This approach efficiently flattens the binary tree into a linked list in-place by taking advantage of the tree structure and manipulating pointers directly during traversal.
