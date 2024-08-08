[# 968. Binary Tree Cameras](https://leetcode.com/problems/binary-tree-cameras/description/)

To solve the problem of placing the minimum number of cameras in a binary tree to monitor all nodes, we can use a greedy strategy combined with depth-first search (DFS). The main idea is to cover the nodes with the least number of cameras by making decisions based on the status of child nodes.

### Approach

1. **Node States**:
   - **State 0**: The node needs a camera.
   - **State 1**: The node is covered (by its child).
   - **State 2**: The node has a camera.

2. **DFS Traversal**:
   - Perform a DFS traversal of the tree starting from the root.
   - At each node, determine the state based on its children's states.

3. **Decision Making**:
   - If either of the children needs a camera (state 0), place a camera at the current node (state 2).
   - If at least one child has a camera (state 2), the current node is covered (state 1).
   - If both children are covered but don't have a camera, the current node needs a camera (state 0).

4. **Post-order Traversal**:
   - Use post-order traversal to ensure that decisions at a node are based on the states of its children.

### Implementation

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def minCameraCover(self, root: TreeNode) -> int:
        # Initialize camera count
        self.cameras = 0
        
        # Define DFS function to determine the state of each node
        def dfs(node):
            if not node:
                return 1  # If the node is null, it is considered covered
            
            left = dfs(node.left)
            right = dfs(node.right)
            
            if left == 0 or right == 0:
                # If either child needs a camera, place a camera at the current node
                self.cameras += 1
                return 2  # Node has a camera
            
            if left == 2 or right == 2:
                # If either child has a camera, the current node is covered
                return 1  # Node is covered
            
            # If both children are covered but don't have a camera, the current node needs a camera
            return 0  # Node needs a camera

        # Start DFS from the root
        if dfs(root) == 0:
            # If the root needs a camera after DFS, add one more camera
            self.cameras += 1

        return self.cameras

# Example usage:
# Constructing the tree [0,0,null,0,0]
root = TreeNode(0)
root.left = TreeNode(0)
root.left.left = TreeNode(0)
root.left.right = TreeNode(0)

solution = Solution()
print(solution.minCameraCover(root))  # Output: 1
```

### Explanation of Code

- **DFS Function**: 
  - The `dfs` function returns the state of each node.
  - It checks the states of the left and right children and decides whether to place a camera or mark the node as covered.

- **Post-order Traversal**:
  - The post-order traversal ensures that the decision at each node takes into account the states of its children.

- **Root Node Check**:
  - After the traversal, if the root is in state 0 (needs a camera), we increment the camera count by 1.

### Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the tree, since each node is visited once.
- **Space Complexity**: \(O(h)\), where \(h\) is the height of the tree, due to the recursion stack. In the worst case (a skewed tree), this can be \(O(n)\).

This solution effectively finds the minimum number of cameras needed by focusing on the state of each node in relation to its children.
