# [112. Path Sum](https://leetcode.com/problems/path-sum/description/)

To solve the problem of finding a root-to-leaf path in a binary tree that sums to a given `targetSum`, we can use a recursive depth-first search (DFS) approach. The idea is to traverse the tree while maintaining a running sum of the values along the path. When we reach a leaf node, we check if the accumulated sum equals `targetSum`.

Here's a Python implementation:

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def hasPathSum(self, root: TreeNode, targetSum: int) -> bool:
        # Base case: if the root is None, there's no path
        if not root:
            return False
        
        # Subtract the current node's value from the target sum
        targetSum -= root.val

        # If we reach a leaf node, check if the path sum equals targetSum
        if not root.left and not root.right:
            return targetSum == 0

        # Recursively check left and right subtrees
        return self.hasPathSum(root.left, targetSum) or self.hasPathSum(root.right, targetSum)

# Helper function to build a tree from a list using level order insertion
def build_tree_from_list(lst):
    if not lst:
        return None

    root = TreeNode(lst[0])
    queue = [root]
    i = 1

    while queue and i < len(lst):
        current = queue.pop(0)

        if i < len(lst) and lst[i] is not None:
            current.left = TreeNode(lst[i])
            queue.append(current.left)
        i += 1

        if i < len(lst) and lst[i] is not None:
            current.right = TreeNode(lst[i])
            queue.append(current.right)
        i += 1

    return root
```

### Explanation

- **Base Case**: If the current node is `None`, we return `False` since there's no path.
- **Leaf Node Check**: If the current node is a leaf (no left or right children), we check if the remaining `targetSum` equals the current node's value. If it does, we've found a valid path, and we return `True`.
- **Recursive Check**: We subtract the current node's value from the `targetSum` and recursively check the left and right subtrees.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. In the worst case, we might need to visit all nodes.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree, which accounts for the recursion stack. In the worst case of an unbalanced tree, the space complexity could be \(O(n)\). In a balanced tree, the space complexity would be \(O(\log n)\).
