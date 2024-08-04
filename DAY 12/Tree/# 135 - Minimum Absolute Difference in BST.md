# [530. Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/)

To find the minimum absolute difference between the values of any two different nodes in a Binary Search Tree (BST), we can leverage the property of BSTs where an in-order traversal yields node values in ascending order. The minimum difference will always be found between two consecutive nodes in this in-order traversal.

Here’s a step-by-step approach in Python to solve the problem:

1. **Perform an In-Order Traversal**: This will give us the values of the BST in ascending order.
2. **Calculate Differences**: Compute the differences between consecutive values during the traversal to find the minimum difference.

### Python Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def getMinimumDifference(self, root: TreeNode) -> int:
        # Initialize variables to track the previous value and the minimum difference
        self.prev = None
        self.min_diff = float('inf')
        
        # Define the in-order traversal helper function
        def in_order(node: TreeNode):
            if not node:
                return
            
            # Traverse the left subtree
            in_order(node.left)
            
            # Process the current node
            if self.prev is not None:
                self.min_diff = min(self.min_diff, node.val - self.prev)
            self.prev = node.val
            
            # Traverse the right subtree
            in_order(node.right)
        
        # Start in-order traversal from the root
        in_order(root)
        
        return self.min_diff

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
root1 = build_tree_from_list([4,2,6,1,3])
sol = Solution()
print(sol.getMinimumDifference(root1))  # Output: 1

# Example 2
root2 = build_tree_from_list([1,0,48,None,None,12,49])
print(sol.getMinimumDifference(root2))  # Output: 1
```

### Explanation

1. **In-Order Traversal**: This traversal visits nodes in ascending order. We track the previous node's value and compare it with the current node’s value to determine the difference.
2. **Calculating Minimum Difference**: By comparing each current node's value with the previous node's value, we find the smallest difference between consecutive nodes.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. We visit each node exactly once during the in-order traversal.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree. This is due to the recursion stack used during the in-order traversal. In the worst case of an unbalanced tree, it could be \(O(n)\), but in a balanced tree, it is \(O(\log n)\).
