# [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

To perform an inorder traversal of a binary tree, we visit the nodes in the following order: left subtree, root, and then the right subtree. Here, I'll provide both recursive and iterative solutions in Python.

### Recursive Solution

The recursive solution is straightforward and involves a helper function to recursively visit each node.

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: TreeNode) -> list[int]:
        result = []
        self._inorderHelper(root, result)
        return result
    
    def _inorderHelper(self, node: TreeNode, result: list[int]):
        if node:
            # Visit the left subtree
            self._inorderHelper(node.left, result)
            # Visit the root
            result.append(node.val)
            # Visit the right subtree
            self._inorderHelper(node.right, result)
```

### Iterative Solution

The iterative solution uses a stack to simulate the recursive call stack.

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: TreeNode) -> list[int]:
        result = []
        stack = []
        current = root
        
        while current or stack:
            # Reach the leftmost node of the current node
            while current:
                stack.append(current)
                current = current.left
                
            # Current must be None at this point
            current = stack.pop()
            result.append(current.val)  # Add the node to the result
            
            # We have visited the node and its left subtree. Now, it's right subtree's turn
            current = current.right
        
        return result
```

### Explanation

- **Recursive Approach**: This approach uses a helper function to perform the traversal. The base case checks if the current node is `None`. It recursively visits the left subtree, then the current node, and finally the right subtree.

- **Iterative Approach**: 
  - Use a stack to keep track of nodes. Start with the root and move to the leftmost node.
  - While traversing, push the nodes onto the stack until you reach a `None`.
  - Pop from the stack, add the node's value to the result, and move to the right subtree.

Both solutions achieve an in-order traversal, but the iterative approach avoids recursion's inherent function call overhead and stack depth limitations. 

### Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. We visit each node exactly once.
- **Space Complexity**: 
  - Recursive: \(O(h)\), where \(h\) is the height of the tree, due to the call stack.
  - Iterative: \(O(h)\), where \(h\) is the height of the tree, due to the stack used in the traversal.
