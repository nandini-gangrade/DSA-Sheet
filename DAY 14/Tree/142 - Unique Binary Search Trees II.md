# [95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

To solve the problem of generating all structurally unique binary search trees (BSTs) that have exactly `n` nodes with unique values from 1 to `n`, we can use a recursive approach. This problem can be solved by considering each number as a root and constructing all possible left and right subtrees recursively.

### Approach

1. **Recursive Construction**:
   - For each number `i` from 1 to `n`, consider it as the root of the tree.
   - Recursively construct all possible left subtrees with nodes from 1 to `i-1`.
   - Recursively construct all possible right subtrees with nodes from `i+1` to `n`.
   - Combine each left and right subtree with the root node `i` to form unique BSTs.

2. **Base Case**:
   - When the start index is greater than the end index in a subtree, return a list with `None` to indicate an empty subtree.

3. **Combination**:
   - For each combination of left and right subtrees, create a new tree with the current root node and add it to the result list.

### Code Implementation

Here is the Python implementation of the approach:

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def generateTrees(self, n: int):
        if n == 0:
            return []
        
        # Helper function to generate all trees
        def generate_trees(start, end):
            trees = []
            if start > end:
                trees.append(None)
                return trees
            
            # Try each number as root
            for i in range(start, end + 1):
                # Generate all left and right subtrees
                left_trees = generate_trees(start, i - 1)
                right_trees = generate_trees(i + 1, end)
                
                # Combine each left and right subtree with the root
                for left in left_trees:
                    for right in right_trees:
                        root = TreeNode(i)
                        root.left = left
                        root.right = right
                        trees.append(root)
            
            return trees

        # Generate all trees from 1 to n
        return generate_trees(1, n)

# Example usage
solution = Solution()
result = solution.generateTrees(3)

# Function to print the tree in a list form
def print_tree(node):
    if not node:
        return [None]
    result = [node.val]
    left = print_tree(node.left)
    right = print_tree(node.right)
    return result + left + right

# Print all unique BSTs
output = [print_tree(tree) for tree in result]
print(output)
```

### Explanation

- **Recursive Helper Function**: `generate_trees(start, end)` generates all BSTs with nodes from `start` to `end`.
- **Iterating over Roots**: For each `i` in `start` to `end`, treat it as the root.
- **Recursive Calls**:
  - Generate all possible left subtrees with nodes from `start` to `i-1`.
  - Generate all possible right subtrees with nodes from `i+1` to `end`.
- **Combining Subtrees**: For each combination of left and right subtrees, create a new tree with root `i` and append to the list of trees.
- **Base Case**: If `start > end`, return `[None]` to signify no subtree.

### Complexity

- **Time Complexity**: The problem's complexity is Catalan number related, specifically \(O(C_n)\), where \(C_n\) is the \(n\)th Catalan number. The average case for Catalan numbers grows asymptotically as \(O(4^n / n^{3/2})\).
- **Space Complexity**: The space complexity is also related to Catalan numbers due to the number of recursive calls and the list of trees generated.
