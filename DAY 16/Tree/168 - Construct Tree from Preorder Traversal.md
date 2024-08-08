# [Construct Tree from Preorder Traversal](https://www.geeksforgeeks.org/problems/construct-tree-from-preorder-traversal/1)

To construct a binary tree from the given preorder traversal and a leaf/non-leaf indicator array, we can take advantage of the properties of preorder traversal. Preorder traversal visits nodes in the order: root, left subtree, right subtree. Given that we have an additional array that tells us whether a node is a leaf (`L`) or a non-leaf (`N`), we can construct the tree recursively.

### Approach

1. **Preorder and PreLN Arrays**:
   - Use the `pre` array to create nodes.
   - Use the `preLN` array to determine whether the created node should have children or not.

2. **Recursive Construction**:
   - Start from the first element of `pre` and `preLN` (the root node).
   - If the current node is marked as `L` in `preLN`, it's a leaf, so return it as is.
   - If it's marked as `N`, recursively construct the left and right subtrees.
   - Keep track of the current position in the arrays with a global or a reference parameter.

3. **Index Tracking**:
   - Use an index to track the current position in the preorder and preLN arrays, and pass it by reference to update it as nodes are processed.

4. **Construct Function**:
   - The function will return the constructed tree's root node after processing all elements.

### Code

Here's the implementation in Python:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def constructTree(n, pre, preLN):
    index = [0]  # Use a list to hold the index so it can be modified inside the function

    def build(index):
        # Base case: If the index is out of bounds, return None
        if index[0] >= n:
            return None
        
        # Create the current node with the current pre[index] value
        current_value = pre[index[0]]
        current_node = Node(current_value)
        
        # If the current node is a leaf, return it
        if preLN[index[0]] == 'L':
            return current_node
        
        # Move to the next index for constructing left subtree
        index[0] += 1
        current_node.left = build(index)
        
        # Move to the next index for constructing right subtree
        index[0] += 1
        current_node.right = build(index)
        
        return current_node
    
    # Construct the tree starting from index 0
    return build(index)

# Function to print inorder traversal of the tree for validation
def inorderTraversal(root):
    if root is not None:
        inorderTraversal(root.left)
        print(root.data, end=' ')
        inorderTraversal(root.right)

# Example usage:
N = 5
pre = [10, 30, 20, 5, 15]
preLN = ['N', 'N', 'L', 'L', 'L']

root = constructTree(N, pre, preLN)

# Print the inorder traversal of the constructed tree
inorderTraversal(root)  # Output should reflect the inorder traversal of the constructed tree
```

### Complexity Analysis

- **Time Complexity**: O(N), where N is the number of nodes. Each node is visited exactly once to construct the tree.

- **Space Complexity**: O(N), which accounts for the recursive stack space in the worst case (skewed tree) and the space used for storing the nodes.

This approach ensures that we efficiently construct the tree while adhering to the preorder traversal order and utilizing the provided leaf/non-leaf information.
