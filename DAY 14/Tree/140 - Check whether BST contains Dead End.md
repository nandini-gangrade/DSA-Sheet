# [Check whether BST contains Dead End](https://www.geeksforgeeks.org/problems/check-whether-bst-contains-dead-end/1)

To solve the problem of determining whether a Binary Search Tree (BST) contains a dead end, we can utilize a recursive approach. A dead end in a BST occurs when there is a leaf node such that no new node can be inserted at or below it while maintaining the BST property. Specifically, this happens when the range for valid node values at a leaf node becomes a single point. In this case, we can identify a dead end if the range of possible values for inserting nodes becomes the same as the current node's value.

### Problem Analysis

1. **Dead End Condition**:
   - In a BST, each node's left subtree has values less than the node, and the right subtree has values greater than the node.
   - A dead end occurs at a leaf node when there is no space to insert new nodes, meaning both potential child positions (left and right) are blocked by BST rules.
   - Specifically, a dead end occurs when the valid range of insertion at a node becomes a single point, i.e., `mini == maxi`.

2. **Node Value Ranges**:
   - At each node, maintain a range `[mini, maxi]` of valid values that could be inserted in the subtree rooted at that node.
   - For a node with value `v`, the valid range for its left child is `[mini, v-1]` and for its right child is `[v+1, maxi]`.

### Approach

- **Recursive Function**:
  - Implement a recursive helper function `solve(node, mini, maxi)` to check for dead ends.
  - Base Case: If the node is `None`, return `False` since there's no node to consider as a dead end.
  - Check Condition: If `mini` equals `maxi`, a dead end is detected, and the function returns `True`.
  - Recursive Calls:
    - Recursively call the function for the left child with an updated range `[mini, node.val - 1]`.
    - Recursively call the function for the right child with an updated range `[node.val + 1, maxi]`.
  - Return `True` if either the left or right recursive call finds a dead end, otherwise return `False`.

### Intuition

The intuition behind the solution is to track the valid range of values for each subtree. If the range at any leaf node reduces to a single value, it means no further insertions are possible, indicating a dead end.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the BST, because each node is visited once.
- **Space Complexity**: \(O(H)\), where \(H\) is the height of the BST, due to the recursion stack. In the worst case, \(H\) could be \(O(N)\) for a skewed tree.

### Code

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def solve(self, root, mini, maxi):
        # Base case: if the node is null, return False (no dead end)
        if root is None:
            return False

        # If the range of possible values becomes a single point, it's a dead end
        if mini == maxi:
            return True

        # Recursively check the left subtree with updated range
        left_side = self.solve(root.left, mini, root.val - 1)
        
        # Recursively check the right subtree with updated range
        right_side = self.solve(root.right, root.val + 1, maxi)

        # Return True if either side contains a dead end
        return left_side or right_side

    def isDeadEnd(self, root):
        # Start checking from the root with initial range [1, infinity]
        return self.solve(root, 1, float('inf'))
```

This implementation efficiently checks each node in the BST for the dead end condition and returns whether any such condition exists in the tree.
