# [99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/description/)

To recover a binary search tree (BST) where exactly two nodes were swapped, you need to identify the swapped nodes and then correct their positions. Here's a step-by-step approach to solve the problem:

### Approach

1. **In-Order Traversal**:
   - Perform an in-order traversal of the BST. For a valid BST, the in-order traversal should produce a sorted sequence of node values. The presence of swapped nodes will disrupt this sequence.

2. **Identify Swapped Nodes**:
   - Traverse the in-order sequence and identify where the order is not strictly increasing. You will find two anomalies:
     - The first anomaly where a node's value is greater than the next node's value.
     - The second anomaly where a node's value is greater than or equal to the next node's value (if the second swapped node is found after the first anomaly).

3. **Correct the Swapped Nodes**:
   - Once the swapped nodes are identified, swap their values to recover the BST.

### Code Implementation

Here's the Python code to implement the above approach:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def recoverTree(self, root: TreeNode) -> None:
        # Initialize variables to keep track of the nodes
        self.first = self.second = self.prev = None
        
        # Perform in-order traversal and find the two nodes
        def in_order_traverse(node: TreeNode):
            if not node:
                return
            
            # Traverse the left subtree
            in_order_traverse(node.left)
            
            # Identify the swapped nodes
            if self.prev and node.val < self.prev.val:
                if not self.first:
                    self.first = self.prev
                self.second = node
            
            # Update the previous node
            self.prev = node
            
            # Traverse the right subtree
            in_order_traverse(node.right)
        
        # Start in-order traversal
        in_order_traverse(root)
        
        # Swap the values of the first and second nodes
        if self.first and self.second:
            self.first.val, self.second.val = self.second.val, self.first.val
```

### Explanation

1. **In-Order Traversal**:
   - We use an in-order traversal to examine each node. If a node's value is less than the previous node's value, we identify a swap anomaly.

2. **Detect Swapped Nodes**:
   - When the order is violated (i.e., `node.val < self.prev.val`), the nodes involved in this violation are potential candidates for swapping.

3. **Correct the Tree**:
   - After identifying the two nodes that need to be swapped (`self.first` and `self.second`), we simply swap their values to correct the BST.

### Complexity

- **Time Complexity**: **O(N)**, where `N` is the number of nodes in the BST. The in-order traversal takes linear time.
- **Space Complexity**: **O(H)**, where `H` is the height of the tree, due to the recursion stack. In the worst case, this is O(N) for a skewed tree.

This approach ensures that you can recover the BST efficiently by correcting only the values of the swapped nodes without altering the tree structure.
