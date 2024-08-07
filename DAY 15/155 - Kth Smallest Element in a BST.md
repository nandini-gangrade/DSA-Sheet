# [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)

To find the kth smallest value in a Binary Search Tree (BST), we can leverage the properties of the BST. In a BST, an in-order traversal yields the nodes in sorted order. By performing an in-order traversal, we can count the nodes until we reach the kth node, which will be our answer.

### Approach

1. **In-order Traversal**:
   - Perform an in-order traversal of the BST.
   - Maintain a counter to count nodes visited.
   - When the counter reaches k, record the node's value and terminate the traversal.

2. **Optimization for Frequent Modifications**:
   - If the BST is modified often, we can enhance our approach using additional data structures:
     - **Augmented BST**: Store the size of the subtree at each node. This allows us to find the kth smallest element in \(O(\log n)\) time.
     - **Order Statistic Tree**: A balanced BST that supports finding the kth smallest element efficiently.

### Implementation

We'll first focus on the simple approach using in-order traversal:

#### Python Implementation

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        def inOrderTraversal(node):
            if not node:
                return []
            return inOrderTraversal(node.left) + [node.val] + inOrderTraversal(node.right)
        
        # Perform in-order traversal to get the nodes in sorted order
        sorted_nodes = inOrderTraversal(root)
        # Return the k-1 element as the list is 0-indexed but k is 1-indexed
        return sorted_nodes[k - 1]
```

#### Efficient Approach with O(k) Traversal

To avoid the need to store all nodes, we can stop traversal once we find the kth smallest element.

```python
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        def inOrderTraversal(node):
            if not node:
                return []
            left = inOrderTraversal(node.left)
            if len(left) >= k:
                return left
            left.append(node.val)
            if len(left) >= k:
                return left
            right = inOrderTraversal(node.right)
            return left + right
        
        # Perform in-order traversal to get nodes up to the kth element
        sorted_nodes = inOrderTraversal(root)
        # Return the k-1 element as the list is 0-indexed but k is 1-indexed
        return sorted_nodes[k - 1]
```

#### Optimized Approach for Frequent Modifications (Augmented BST)

Here is an outline of the optimized approach using an augmented BST with subtree sizes.

```python
class AugmentedTreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
        self.size = 1  # size of the subtree rooted at this node

class AugmentedBST:
    def insert(self, root, key):
        if not root:
            return AugmentedTreeNode(key)
        if key < root.val:
            root.left = self.insert(root.left, key)
        else:
            root.right = self.insert(root.right, key)
        root.size = 1 + self._size(root.left) + self._size(root.right)
        return root

    def kthSmallest(self, root, k):
        left_size = self._size(root.left)
        if k <= left_size:
            return self.kthSmallest(root.left, k)
        elif k > left_size + 1:
            return self.kthSmallest(root.right, k - left_size - 1)
        return root.val

    def _size(self, node):
        return node.size if node else 0
```

### Complexity Analysis

- **Time Complexity**: 
  - For the simple in-order traversal approach, the time complexity is \(O(n)\) where \(n\) is the number of nodes in the BST.
  - For the optimized augmented BST, the time complexity is \(O(\log n)\) for both insertion and finding the kth smallest element.

- **Space Complexity**:
  - The in-order traversal approach uses \(O(n)\) space due to the recursion stack and the list to store node values.
  - The augmented BST approach uses \(O(h)\) space for the recursion stack, where \(h\) is the height of the tree.

This solution provides a clear method to find the kth smallest element in a BST, with optimizations available for scenarios with frequent modifications.
