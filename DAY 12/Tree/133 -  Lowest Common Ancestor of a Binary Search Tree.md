# [235.  Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

To find the lowest common ancestor (LCA) of two nodes in a binary search tree (BST), we can leverage the properties of a BST. In a BST, for any node `N`, the left subtree contains nodes with values less than `N.val`, and the right subtree contains nodes with values greater than `N.val`. Using this property, we can determine the LCA by comparing the values of `p` and `q` with the current node's value.

Here's how we can implement this in Python:

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        # Start from the root node of the BST
        current = root

        while current:
            # If both p and q are greater than the current node, move to the right subtree
            if p.val > current.val and q.val > current.val:
                current = current.right
            # If both p and q are less than the current node, move to the left subtree
            elif p.val < current.val and q.val < current.val:
                current = current.left
            else:
                # If the current node is between p and q, then it's the LCA
                return current

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

# Example 1
root1 = build_tree_from_list([6, 2, 8, 0, 4, 7, 9, None, None, 3, 5])
p1 = TreeNode(2)
q1 = TreeNode(8)
sol = Solution()
print(sol.lowestCommonAncestor(root1, p1, q1).val)  # Output: 6

# Example 2
root2 = build_tree_from_list([6, 2, 8, 0, 4, 7, 9, None, None, 3, 5])
p2 = TreeNode(2)
q2 = TreeNode(4)
print(sol.lowestCommonAncestor(root2, p2, q2).val)  # Output: 2

# Example 3
root3 = build_tree_from_list([2, 1])
p3 = TreeNode(2)
q3 = TreeNode(1)
print(sol.lowestCommonAncestor(root3, p3, q3).val)  # Output: 2
```

### Explanation

- **Traverse the Tree**: Start at the root of the BST and traverse the tree based on the values of `p` and `q`.
- **Move Right**: If both `p` and `q` have values greater than the current node's value, move to the right child.
- **Move Left**: If both `p` and `q` have values less than the current node's value, move to the left child.
- **Found LCA**: If one of `p` or `q` is less than or equal to the current node and the other is greater than or equal, the current node is the LCA.

### Complexity Analysis

- **Time Complexity**: \(O(h)\), where \(h\) is the height of the tree. In the worst case, this is \(O(n)\) for a skewed tree, but \(O(\log n)\) for a balanced tree.
- **Space Complexity**: \(O(1)\), since we are using a constant amount of space, not counting the stack space in case of a recursive approach. Here, we use an iterative approach that doesn't involve recursion.
