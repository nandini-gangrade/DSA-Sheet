# [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)

To populate each `next` pointer in a perfect binary tree, we can take advantage of the tree's perfect structure. Here's a solution that uses a level-order traversal approach to link the `next` pointers without using any extra space beyond the implicit recursive stack.

### Approach

Since the tree is perfect, every parent node has exactly two children, and all leaf nodes are at the same level. This characteristic allows us to link nodes at each level efficiently:

1. **Iterative Level Order Traversal**:
   - Use the `next` pointers to traverse each level, starting from the leftmost node.
   - Connect the left child to the right child for each node.
   - If a node has a `next` pointer, connect its right child to the next node's left child.

2. **Recursive Approach**:
   - For a given node, connect its children and recursively do the same for its children. Use the established `next` pointers to connect across subtree boundaries.

### Code Implementation

```python
class Node:
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next

class Solution:
    def connect(self, root: Node) -> Node:
        if not root:
            return root
        
        # Start with the root node
        leftmost = root
        
        # Traverse the levels
        while leftmost.left:
            # Iterate over the nodes in the current level
            head = leftmost
            while head:
                # Connect the left child to the right child
                head.left.next = head.right
                
                # Connect the right child to the next node's left child, if available
                if head.next:
                    head.right.next = head.next.left
                
                # Move to the next node in the current level
                head = head.next
            
            # Move to the next level
            leftmost = leftmost.left
        
        return root
```

### Explanation

- **Leftmost Pointer**: We start with the `leftmost` pointer at the root of the tree. This pointer helps us track the first node at each level.
  
- **Level Traversal**: For each level, we use a `head` pointer to traverse nodes horizontally. For each node:
  - Link `left` child to `right` child.
  - If the node has a `next`, link the `right` child to the `left` child of the `next` node.
  
- **Move to Next Level**: After processing all nodes at the current level, move `leftmost` to its left child, descending to the next level.

### Complexity

- **Time Complexity**: **O(N)**, where `N` is the number of nodes in the tree. Each node is visited once.
- **Space Complexity**: **O(1)**, as no additional data structures are used except for a few pointers. The space complexity is constant.

This approach efficiently populates each `next` pointer in the tree, leveraging the perfect binary tree structure to achieve constant space complexity.
