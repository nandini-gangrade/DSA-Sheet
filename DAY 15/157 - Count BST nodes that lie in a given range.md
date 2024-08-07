# [Count BST nodes that lie in a given range](https://www.geeksforgeeks.org/problems/count-bst-nodes-that-lie-in-a-given-range/1)

To count the number of nodes in a Binary Search Tree (BST) that lie within a given range \([l, h]\), we can use a recursive approach to traverse the tree and check each node's value against the specified range. Since a BST has the property that left children are smaller and right children are greater or equal, we can leverage this to optimize the traversal.

### Approach

1. **Base Case**:
   - If the current node is `None`, return 0 as there are no nodes to count.

2. **Current Node Value within Range**:
   - If the current node's value lies within the range \([l, h]\), increment the count and recursively check both left and right subtrees because nodes in both subtrees might also fall within the range.

3. **Current Node Value Less Than Range**:
   - If the current node's value is less than \(l\), we only need to consider the right subtree because all values in the left subtree are guaranteed to be less than \(l\) (given the properties of a BST).

4. **Current Node Value Greater Than Range**:
   - If the current node's value is greater than \(h\), only the left subtree needs to be considered for the same reason: all values in the right subtree will be greater than \(h\).

This approach ensures that we only traverse necessary parts of the tree, leveraging the BST properties to skip irrelevant nodes, making it efficient.

### Code

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def getCountOfNode(self, root: TreeNode, l: int, h: int) -> int:
        if root is None:
            return 0

        # Initialize the count
        count = 0

        # If current node's value is in range, increment count
        if l <= root.val <= h:
            count = 1

        # If current node's value is greater than `l`, explore left subtree
        if root.val > l:
            count += self.getCountOfNode(root.left, l, h)

        # If current node's value is less than `h`, explore right subtree
        if root.val < h:
            count += self.getCountOfNode(root.right, l, h)

        return count
```

### Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. In the worst case, we may need to visit all nodes (e.g., if all nodes fall within the range).
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree, due to the recursive call stack. In the worst case (skewed tree), the height could be \(O(n)\), but it is \(O(\log n)\) on average for a balanced tree.

This solution efficiently counts the nodes within the specified range by utilizing the BST properties to skip unnecessary branches, thereby reducing unnecessary recursive calls and checks.
