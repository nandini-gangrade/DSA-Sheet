# [987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/)

To solve the problem of finding the vertical order traversal of a binary tree, we can use a breadth-first search (BFS) approach. This approach involves traversing the tree level by level while maintaining the column index for each node.

### Approach

1. **Use a Queue for BFS**:
   - Use a queue to perform BFS, where each element in the queue is a tuple containing the node, its row, and its column index.

2. **Dictionary to Store Nodes**:
   - Use a dictionary to store nodes grouped by their column indices. The keys are the column indices, and the values are lists of tuples containing (row, value) for nodes at that column.

3. **BFS Traversal**:
   - Start with the root node at position (0, 0) in the queue.
   - For each node, add its left child to the queue with column index decreased by 1 and its right child with column index increased by 1.
   - For each node, store its value in the dictionary under its column index, along with its row index.

4. **Sort and Construct Result**:
   - After the BFS traversal, iterate over the dictionary sorted by column indices.
   - For each column, sort the nodes first by their row index and then by value.
   - Append the sorted node values for each column to the result.

5. **Return the Result**:
   - The result is a list of lists, where each list contains the node values for a column in top-to-bottom order.

### Implementation

Here's the Python code to achieve the vertical order traversal:

```python
from collections import defaultdict, deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def verticalTraversal(self, root: TreeNode):
        # Dictionary to store nodes by column index
        col_table = defaultdict(list)
        
        # Queue for BFS with (node, row, col) as elements
        queue = deque([(root, 0, 0)])
        
        while queue:
            node, row, col = queue.popleft()
            if node:
                # Add the node to the column table
                col_table[col].append((row, node.val))
                # Add left and right children to the queue
                queue.append((node.left, row + 1, col - 1))
                queue.append((node.right, row + 1, col + 1))
        
        # Sort the columns and build the result
        result = []
        for col in sorted(col_table.keys()):
            # Sort by row first, then by value
            col_table[col].sort(key=lambda x: (x[0], x[1]))
            result.append([val for row, val in col_table[col]])
        
        return result

# Example usage:
# Constructing the tree [3,9,20,null,null,15,7]
root = TreeNode(3)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)

solution = Solution()
print(solution.verticalTraversal(root))  # Output: [[9], [3, 15], [20], [7]]
```

### Explanation of Code

- **BFS Traversal**:
  - We perform a BFS to ensure nodes are processed level by level.
  - For each node, we calculate its column index and add it to the dictionary.

- **Sorting**:
  - The dictionary is sorted by column indices.
  - Within each column, nodes are sorted first by row index and then by node value.

### Complexity Analysis

- **Time Complexity**: \(O(N \log N)\), where \(N\) is the number of nodes. Sorting the nodes within each column contributes to the \(\log N\) factor.
- **Space Complexity**: \(O(N)\), where \(N\) is the number of nodes. This accounts for the space used by the queue and the column table.

This solution efficiently computes the vertical order traversal by leveraging BFS and sorting techniques.
