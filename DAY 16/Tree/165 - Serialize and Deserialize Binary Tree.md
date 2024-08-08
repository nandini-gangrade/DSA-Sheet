# [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

**Serialization** is the process of converting a binary tree into a string format so that it can be stored or transmitted easily. **Deserialization** is the reverse process of converting the string back into the original binary tree structure.

Given the root of a binary tree, you need to design an algorithm to serialize the tree into a string and then deserialize it back to the same tree structure. The tree nodes have integer values, and the tree can be empty.

### Intuition

- **Serialization**: The goal is to encode the tree structure into a single string, including both node values and the structure of null nodes, so we can later recreate the same tree.

- **Deserialization**: The aim is to decode the string back into the original tree structure, accurately reconstructing both the node values and their connections.

### Approach

The given approach uses **preorder traversal** (root-left-right) to serialize the binary tree into a string and the same traversal pattern to deserialize the string back into a tree.

#### Serialization

1. **Preorder Traversal**: Visit the root node, then recursively serialize the left subtree, followed by the right subtree.
2. **Null Nodes**: Represent null nodes with a unique marker (e.g., "N") to indicate where a node does not exist.
3. **String Construction**: Concatenate node values with a delimiter (e.g., ",") to create a single string that represents the tree.

#### Deserialization

1. **Iterator**: Split the serialized string into a list of node values and use an iterator to process them sequentially.
2. **Recursive Reconstruction**: Use a helper function that reads values from the iterator:
   - If the value is "N", return `None` to represent a null node.
   - Otherwise, create a new `TreeNode` with the integer value, and recursively reconstruct its left and right subtrees.

### Code Implementation

Here is the complete implementation:

```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Codec:
    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        def helper(node):
            if not node:
                return "N,"
            return str(node.val) + "," + helper(node.left) + helper(node.right)

        return helper(root)
        
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        values = iter(data.split(","))  # Split data into a list of node values
        
        def helper(values):
            val = next(values)  # Get the next value from the iterator
            if val == "N":
                return None  # If the value is "N", return None to represent a null node
            node = TreeNode(int(val))  # Create a new TreeNode with the integer value
            node.left = helper(values)  # Recursively build the left subtree
            node.right = helper(values)  # Recursively build the right subtree
            return node

        return helper(values)
        
# Example usage:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

### Complexity Analysis

- **Time Complexity**:
  - **Serialization**: \(O(n)\), where \(n\) is the number of nodes in the tree. Each node is visited once.
  - **Deserialization**: \(O(n)\), since each node value is processed once to reconstruct the tree.

- **Space Complexity**:
  - **Serialization**: \(O(n)\), to store the serialized string, which includes all nodes and null markers.
  - **Deserialization**: \(O(n)\), for the recursion stack in the worst case, which is the height of the tree, and for storing the split node values.
