# [257. Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/description/)

To find all root-to-leaf paths in a binary tree, we can perform a depth-first search (DFS) traversal, keeping track of the current path from the root to each leaf node. When we reach a leaf node, we add the current path to the result list.

### Solution

Here is the implementation of this approach:

```python
# Definition for a binary tree node.
from typing import Optional, List

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        def dfs(node, path, result):
            if not node:
                return

            # Append the current node value to the path
            path.append(str(node.val))

            # If it's a leaf node, append the path to the result
            if not node.left and not node.right:
                result.append("->".join(path))
            else:
                # Recurse on left and right children
                if node.left:
                    dfs(node.left, path, result)
                if node.right:
                    dfs(node.right, path, result)

            # Backtrack: remove the current node value from the path
            path.pop()

        result = []
        dfs(root, [], result)
        return result

# Helper function to build a tree from a list using level order insertion
def build_tree_from_list(lst):
    if not lst:
        return None

    root = TreeNode(lst[0])
    queue = [root]
    i = 1

    while queue and i < len(lst):
        current = queue.pop(0)

        if lst[i] is not None:
            current.left = TreeNode(lst[i])
            queue.append(current.left)
        i += 1

        if i < len(lst) and lst[i] is not None:
            current.right = TreeNode(lst[i])
            queue.append(current.right)
        i += 1

    return root

# Example 1
root1 = build_tree_from_list([1, 2, 3, None, 5])
sol = Solution()
print(sol.binaryTreePaths(root1))  # Output: ["1->2->5", "1->3"]

# Example 2
root2 = build_tree_from_list([1])
print(sol.binaryTreePaths(root2))  # Output: ["1"]
```

### Explanation

- **DFS Traversal**: The `dfs` function traverses the tree recursively. It appends the current node's value to the path list and checks if the node is a leaf (both left and right children are `None`).

- **Path Construction**: When a leaf node is reached, the current path is converted to a string using `"->".join(path)` and added to the result list.

- **Backtracking**: After exploring a node, we backtrack by removing the last node's value from the path to explore other paths.

### Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree. We visit each node once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree. This space is used by the recursion stack and the path list.

This solution effectively finds all root-to-leaf paths in the given binary tree using depth-first search and backtracking.
