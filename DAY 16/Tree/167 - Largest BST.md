# [Largest BST](https://www.geeksforgeeks.org/problems/largest-bst/1)

To solve the problem of finding the size of the largest subtree that is a Binary Search Tree (BST) in a given binary tree, we can use a recursive approach that efficiently checks the properties of a BST for each subtree and calculates the size of the largest one.

### Approach

1. **Recursive Function**: We will define a recursive function that will return several pieces of information for each subtree:
   - Whether the subtree is a BST.
   - The size of the largest BST within the subtree.
   - The minimum and maximum values within the subtree to validate BST properties for parent nodes.

2. **Base Case**: For a null node, the subtree is trivially a BST with size 0, and we can assume infinite bounds to not interfere with the parent checks.

3. **Leaf Node**: A leaf node is a BST of size 1.

4. **Recursive Case**:
   - Recursively find the largest BSTs in the left and right subtrees.
   - If the current node can be the root of a BST (i.e., the left subtree is a BST, the right subtree is a BST, and the current node's value is greater than the maximum of the left subtree and less than the minimum of the right subtree), then calculate the size of the current BST.
   - Update the maximum size if the current subtree forms a larger BST.

5. **Return Values**: For each node, return:
   - A boolean indicating whether it's a BST.
   - The size of the largest BST.
   - The minimum and maximum node values in the subtree.

### Code

Here's an optimized implementation of the approach in Python:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class Solution:
    
    def largestBst(self, root):
        self.max_size = 0
        
        def largestBSTUtil(node):
            if node is None:
                return True, 0, float('inf'), float('-inf')
            
            if node.left is None and node.right is None:
                self.max_size = max(1, self.max_size)
                return True, 1, node.data, node.data
            
            left_is_bst, left_size, left_min, left_max = largestBSTUtil(node.left)
            right_is_bst, right_size, right_min, right_max = largestBSTUtil(node.right)
            
            if left_is_bst and right_is_bst and left_max < node.data < right_min:
                size = left_size + right_size + 1
                self.max_size = max(self.max_size, size)
                return True, size, min(left_min, node.data), max(right_max, node.data)
            
            return False, 0, 0, 0
        
        largestBSTUtil(root)
        return self.max_size

# Example usage:
root = Node(6)
root.left = Node(6)
root.right = Node(2)
root.left.right = Node(2)
root.right.left = Node(1)
root.right.right = Node(3)

solution = Solution()
print(solution.largestBst(root))  # Output: 3
```

### Complexity Analysis

- **Time Complexity**: O(N), where N is the number of nodes in the tree. Each node is visited once, and operations per node take constant time.
  
- **Space Complexity**: O(H), where H is the height of the tree. This is the space used by the call stack during recursion. In the worst case of a skewed tree, H could be O(N), but for a balanced tree, it's O(log N).

This approach efficiently checks each subtree and keeps track of the size of the largest BST found, ensuring an optimal solution within the given constraints.
