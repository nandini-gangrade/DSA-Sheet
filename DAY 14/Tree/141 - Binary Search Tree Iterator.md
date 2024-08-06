# [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/description/)

To implement the `BSTIterator` class, we need to create an iterator over the in-order traversal of a Binary Search Tree (BST). The challenge is to do this with `next()` and `hasNext()` operations in average \(O(1)\) time complexity, using \(O(h)\) space complexity, where \(h\) is the height of the tree.

### Approach

The in-order traversal of a BST visits nodes in ascending order of their values. To efficiently achieve this traversal with limited space, we can use a stack to simulate the recursive traversal process iteratively:

1. **Stack**: We use a stack to keep track of nodes. This allows us to traverse the tree iteratively in in-order.
2. **Push Left Nodes**: For the current node, we push all its left children onto the stack. This ensures that the smallest available node is on top of the stack.
3. **Next Node**: The `next()` function pops the top node from the stack (the smallest element not yet visited) and processes its right subtree by pushing all left children of the right child onto the stack.
4. **Has Next**: The `hasNext()` function checks if there are more nodes to visit by verifying if the stack is non-empty.

### Code Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class BSTIterator:
    def __init__(self, root: TreeNode):
        # Initialize the stack and push all left children of the root
        self.stack = []
        self._push_left_children(root)
        
    def _push_left_children(self, node: TreeNode):
        # Push all left children onto the stack
        while node:
            self.stack.append(node)
            node = node.left

    def next(self) -> int:
        # Pop the top node from the stack, which is the next in in-order traversal
        if self.hasNext():
            node = self.stack.pop()
            # If the node has a right child, push all its left children onto the stack
            if node.right:
                self._push_left_children(node.right)
            # Return the value of the current node
            return node.val
        raise Exception("No next element")

    def hasNext(self) -> bool:
        # Check if the stack is not empty
        return len(self.stack) > 0

# Example usage
# Constructing the tree: [7, 3, 15, null, null, 9, 20]
root = TreeNode(7)
root.left = TreeNode(3)
root.right = TreeNode(15)
root.right.left = TreeNode(9)
root.right.right = TreeNode(20)

# Initialize iterator
iterator = BSTIterator(root)
# Iterate over the BST
output = []
while iterator.hasNext():
    output.append(iterator.next())

print(output)  # Output: [3, 7, 9, 15, 20]
```

### Explanation

1. **Initialization**:
   - The constructor initializes the stack and populates it with all left children starting from the root. This setup ensures that the smallest node is at the top of the stack.

2. **Next Operation**:
   - The `next()` method pops the top node from the stack, which corresponds to the next smallest element in the BST. If this node has a right child, we push all its left children onto the stack to maintain the in-order traversal sequence.

3. **HasNext Operation**:
   - The `hasNext()` method simply checks if there are any nodes left to visit by checking if the stack is empty or not.

### Complexity

- **Time Complexity**: Both `next()` and `hasNext()` operations run in average \(O(1)\) time because each node is pushed and popped from the stack exactly once.
- **Space Complexity**: The space complexity is \(O(h)\), where \(h\) is the height of the tree, due to the stack used to store the nodes for the in-order traversal. In the worst case, the height of the tree could be \(O(n)\), but on average, for a balanced tree, it will be \(O(\log n)\).
