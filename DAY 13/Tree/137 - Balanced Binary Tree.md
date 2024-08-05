# [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)

To determine if a binary tree is height-balanced, we need to check if, for every node in the tree, the height difference between its left and right subtrees is no more than one. A height-balanced binary tree is also known as an AVL tree.

### Approach

We can solve this problem using a recursive depth-first search (DFS) approach. The idea is to recursively calculate the height of each subtree and check if the subtrees are balanced as we go up the tree.

1. **Define a Helper Function**: This function will return the height of a subtree if it is balanced, or -1 if it is not.
2. **Recursive Check**:
   - If a subtree is balanced, return its height.
   - If any subtree is not balanced (i.e., the helper function returns -1), propagate this result upwards.
3. **Base Case**: An empty subtree is balanced and has a height of 0.

### Python Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def check_balance(node: TreeNode) -> int:
            if not node:
                return 0
            
            # Recursively check the balance of the left subtree
            left_height = check_balance(node.left)
            if left_height == -1:
                return -1
            
            # Recursively check the balance of the right subtree
            right_height = check_balance(node.right)
            if right_height == -1:
                return -1
            
            # Check the height difference
            if abs(left_height - right_height) > 1:
                return -1
            
            # Return the height of the current subtree
            return max(left_height, right_height) + 1
        
        # Start from the root
        return check_balance(root) != -1

# Example usage
def build_tree_from_list(lst):
    """Helper function to build a tree from a list using level order insertion."""
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
root1 = build_tree_from_list([3,9,20,None,None,15,7])
sol = Solution()
print(sol.isBalanced(root1))  # Output: True

# Example 2
root2 = build_tree_from_list([1,2,2,3,3,None,None,4,4])
print(sol.isBalanced(root2))  # Output: False

# Example 3
root3 = build_tree_from_list([])
print(sol.isBalanced(root3))  # Output: True
```

### Explanation

1. **Helper Function (`check_balance`)**: This function returns the height of the tree rooted at the given node if it is balanced. If the subtree rooted at the node is not balanced, it returns -1.
   - **Base Case**: If the node is `None`, the height is 0.
   - **Recursive Case**: Calculate the height of the left and right subtrees. If any of them is unbalanced, return -1 immediately.
   - Check the difference between the heights of the left and right subtrees. If it is greater than 1, return -1 (indicating the subtree is unbalanced).
   - Otherwise, return the height of the subtree rooted at the current node as `1 + max(left_height, right_height)`.

2. **Checking the Root**: Call the helper function starting from the root node. If the function returns anything other than -1, the tree is balanced.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. Each node is visited exactly once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree due to the recursive stack. In the worst case of an unbalanced tree, this could be \(O(n)\), but in a balanced tree, it is \(O(\log n)\).
