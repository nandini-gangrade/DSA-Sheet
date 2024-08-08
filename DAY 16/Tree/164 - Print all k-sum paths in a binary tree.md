# [Print all k-sum paths in a binary tree](https://www.geeksforgeeks.org/print-k-sum-paths-binary-tree/)

To solve the problem of finding all paths in a binary tree where the sum of the nodes in each path equals a given value \( k \), we can perform a pre-order traversal of the tree while maintaining a list of nodes in the current path. For each node, we will check all possible paths ending at that node to see if any sum up to \( k \). Here's the detailed approach:

### Approach

1. **Pre-order Traversal**: 
   - We will perform a pre-order traversal of the tree, which means we process the current node before its children.

2. **Path Tracking**:
   - As we traverse the tree, we maintain a list of nodes representing the path from the root to the current node.
   - At each node, we check all paths ending at the current node to see if any have a sum equal to \( k \).

3. **Check Paths**:
   - For each node, traverse the current path backward to check the sum of all possible sub-paths that end at the current node.
   - If any sub-path has a sum equal to \( k \), we print that path.

4. **Recursive Traversal**:
   - Continue this process recursively for both left and right children of the current node.

5. **Backtracking**:
   - After processing both children of a node, remove the current node from the path to backtrack as we return to the parent node.

### Implementation

Here's the Python code implementing the above approach:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def printKSumPaths(root, k):
    def findPaths(node, path):
        if not node:
            return

        # Add current node to the path
        path.append(node.val)
        
        # Check all sub-paths in the path that end with the current node
        path_sum = 0
        for j in range(len(path) - 1, -1, -1):
            path_sum += path[j]
            if path_sum == k:
                print(path[j:])  # Print the valid path
        
        # Recursively process the left and right subtrees
        findPaths(node.left, path)
        findPaths(node.right, path)
        
        # Remove the current node from the path to backtrack
        path.pop()

    # Call the recursive helper function with an empty path
    findPaths(root, [])

# Example usage:
# Constructing the tree from the example
root = TreeNode(1)
root.left = TreeNode(3)
root.right = TreeNode(-1)
root.left.left = TreeNode(2)
root.left.right = TreeNode(1)
root.left.right.left = TreeNode(1)
root.right.left = TreeNode(4)
root.right.right = TreeNode(5)
root.right.left.left = TreeNode(1)
root.right.left.right = TreeNode(2)
root.right.right.right = TreeNode(6)

k = 5
print("Paths with sum", k, "are:")
printKSumPaths(root, k)
```

### Explanation of the Code

- **TreeNode Class**: Defines a node of the binary tree with `val`, `left`, and `right`.
  
- **printKSumPaths Function**: 
  - This is the main function that initializes the recursive process.

- **findPaths Function**:
  - This recursive helper function takes a node and the current path as arguments.
  - It appends the current node's value to the path and checks all sub-paths ending at this node.
  - If a sub-path's sum equals \( k \), it prints the path.
  - It then recursively calls itself for the left and right children of the current node.
  - After processing the children, it pops the current node from the path to backtrack.

### Complexity Analysis

- **Time Complexity**: \( O(N^2) \) in the worst case, where \( N \) is the number of nodes in the tree. This is because for each node, we might check a path that is as long as the height of the tree.

- **Space Complexity**: \( O(h) \), where \( h \) is the height of the tree. This is the space used by the recursion stack and the path list.

This code efficiently finds and prints all paths in the binary tree with a sum equal to \( k \). It leverages recursion and backtracking to explore all potential paths and ensure that no paths are missed.
