# [Preorder to BST](https://www.geeksforgeeks.org/problems/preorder-to-postorder4423/1)

Here's a detailed approach, intuition, and Python code for constructing a Binary Search Tree (BST) from its preorder traversal:

### Approach and Intuition

1. **Understanding the Problem**:
   - You are given a preorder traversal of a BST. In preorder traversal, the root node is visited first, followed by the left subtree and then the right subtree.
   - Your task is to reconstruct the BST from this preorder traversal.

2. **Key Observations**:
   - In preorder traversal, the first element is always the root of the tree (or subtree).
   - Elements following the root in the preorder array can be divided into left and right subtrees based on their values. 
   - For a given node, all elements smaller than the node's value are in the left subtree, and elements larger are in the right subtree.

3. **Recursive Approach**:
   - **Base Case**: If the index exceeds the length of the preorder array or if the current value exceeds the upper bound (which means it's out of the valid range for the current subtree), return `None`.
   - **Recursive Case**:
     - Create a new node with the current value.
     - Recursively construct the left subtree with an updated bound (the value of the current node).
     - Recursively construct the right subtree with the original bound.
   - **Initialization**: Start with the entire range of valid values (`-inf` to `inf`) for the root node.

### Python Code

Here's the Python implementation of the above approach:

```python
class Node:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def bst(self, pre, bound, index):
        # Base case: If index is out of range or the current value is greater than the bound
        if index[0] == len(pre) or pre[index[0]] > bound:
            return None
        
        # Create the root node with the current value
        root_val = pre[index[0]]
        index[0] += 1
        root = Node(root_val)
        
        # Recursively build the left subtree with the updated bound
        root.left = self.bst(pre, root_val, index)
        # Recursively build the right subtree with the original bound
        root.right = self.bst(pre, bound, index)
        
        return root
    
    def Bst(self, pre):
        # Initialize the index array and call the helper function
        return self.bst(pre, float('inf'), [0])
```

### Complexity Analysis

1. **Time Complexity**:
   - The time complexity is \(O(N)\), where \(N\) is the number of nodes. Each node is processed once to create a tree node, and the recursive traversal ensures that each node is visited only once.

2. **Space Complexity**:
   - The space complexity is \(O(H)\), where \(H\) is the height of the BST. This space is used by the recursion stack. In the worst case (a completely unbalanced tree), this could be \(O(N)\), but for a balanced BST, it would be \(O(\log N)\).

### Usage Example

Here's how you might use the `Solution` class to construct a BST from a preorder list and print the postorder traversal:

```python
# Example Usage
solution = Solution()
preorder = [40, 30, 35, 80, 100]
root = solution.Bst(preorder)

# Helper function to print the tree in postorder traversal
def postOrderTraversal(root):
    if root is None:
        return []
    return postOrderTraversal(root.left) + postOrderTraversal(root.right) + [root.val]

print(postOrderTraversal(root))  # Output: [35, 30, 100, 80, 40]
```

This approach efficiently reconstructs the BST using preorder traversal and adheres to the constraints of time and space complexity.
