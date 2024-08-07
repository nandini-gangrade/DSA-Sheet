# [Min distance between two given nodes of a Binary Tree](https://www.geeksforgeeks.org/problems/min-distance-between-two-given-nodes-of-a-binary-tree/1)

### Intuition

To find the minimum distance between two nodes \(a\) and \(b\) in a binary tree, we can utilize the concept of the Lowest Common Ancestor (LCA). The idea is that the distance between two nodes in a tree can be broken down into:

1. **Finding the Lowest Common Ancestor (LCA)** of the two nodes. The LCA is the deepest node that is an ancestor of both \(a\) and \(b\).
2. **Calculate the distance from the LCA to node \(a\)**.
3. **Calculate the distance from the LCA to node \(b\)**.
4. **Sum the two distances** to get the minimum distance between the nodes.

### Approach

1. **Find the LCA**: 
   - Recursively traverse the tree.
   - If either of the nodes \(a\) or \(b\) is found, return that node.
   - If both the left and right subtrees return non-null values, the current node is the LCA.
   - If only one of the subtrees returns a non-null value, return that.

2. **Find Distance from LCA to Target Node**:
   - Starting from the LCA, find the distance to a target node (either \(a\) or \(b\)).
   - If the target node is found, return the distance.
   - If not found, return \(-1\).

3. **Calculate Total Distance**: Sum the distances from LCA to \(a\) and from LCA to \(b\).

### Code

```python
class TreeNode:
    def __init__(self, data=0, left=None, right=None):
        self.data = data
        self.left = left
        self.right = right

class Solution:
    def findDist(self, root, a, b):
        # Helper function to find the Lowest Common Ancestor
        def findLCA(node, a, b):
            if not node:
                return None
            if node.data == a or node.data == b:
                return node
            
            left = findLCA(node.left, a, b)
            right = findLCA(node.right, a, b)
            
            if left and right:
                return node
            
            return left if left else right

        # Helper function to find the distance from the LCA to the target node
        def distanceFromLCA(node, val, dist):
            if not node:
                return -1
            if node.data == val:
                return dist
            
            leftDist = distanceFromLCA(node.left, val, dist + 1)
            if leftDist != -1:
                return leftDist
            
            return distanceFromLCA(node.right, val, dist + 1)

        # Finding the Lowest Common Ancestor (LCA)
        lca = findLCA(root, a, b)
        
        # Calculating the distance from LCA to a and b
        distA = distanceFromLCA(lca, a, 0)
        distB = distanceFromLCA(lca, b, 0)
        
        # Returning the total distance
        return distA + distB
```

### Complexity

- **Time Complexity**: \(O(n)\)
  - The `findLCA` function visits each node once in the worst case, so it runs in \(O(n)\) time.
  - The `distanceFromLCA` function also visits nodes from the LCA to the target nodes. The combined operations ensure each node is processed at most twice, making the overall complexity \(O(n)\).

- **Space Complexity**: \(O(h)\)
  - This is the height of the tree, due to the recursive stack space. In the worst case, for a skewed tree, this can be \(O(n)\), but for a balanced tree, it's \(O(\log n)\).

This solution efficiently finds the minimum distance between two nodes in a binary tree by leveraging the concept of LCA, ensuring both clarity and optimal performance.
