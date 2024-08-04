# [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/description/)

To find the sum of all left leaves in a binary tree, you can use a depth-first traversal approach. Specifically, you'll want to traverse the tree and sum up the values of all leaves that are the left children of their parent nodes.

Here’s how you can approach this problem:

1. **Define a Helper Function**: This function will perform a recursive traversal of the tree. It will check if the current node is a left leaf, and if so, add its value to the total sum.
2. **Check for Leaves**: A node is considered a leaf if it does not have left or right children.
3. **Handle Left Child Check**: In addition to checking if the node is a leaf, also ensure that it is the left child of its parent before adding its value to the sum.

### Python Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
        def dfs(node: TreeNode, is_left: bool) -> int:
            if not node:
                return 0

            # Check if the current node is a leaf
            if not node.left and not node.right:
                if is_left:
                    return node.val
                return 0

            # Continue traversing left and right subtrees
            left_sum = dfs(node.left, True)
            right_sum = dfs(node.right, False)
            
            return left_sum + right_sum
        
        return dfs(root, False)  # Start from the root and the root is not a left child

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
print(sol.sumOfLeftLeaves(root1))  # Output: 24

# Example 2
root2 = build_tree_from_list([1])
print(sol.sumOfLeftLeaves(root2))  # Output: 0
```

### Explanation

1. **DFS Function**: The `dfs` function traverses the tree. It takes an additional boolean `is_left` to determine if the current node is a left child of its parent.
   - If the node is a leaf and `is_left` is `True`, the node’s value is added to the sum.
   - If the node is a leaf but `is_left` is `False`, the node’s value is not added.
   - Recursively call the function for the left and right children, updating the `is_left` status accordingly.

2. **Initialization**: The traversal starts with the root node and `is_left` set to `False` because the root is not a left child of any node.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. Every node is visited exactly once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree due to the recursive stack. In the worst case of an unbalanced tree, this could be \(O(n)\), but in a balanced tree, it is \(O(\log n)\).
