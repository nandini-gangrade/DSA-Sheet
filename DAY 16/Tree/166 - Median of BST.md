# [Median of BST](https://www.geeksforgeeks.org/problems/median-of-bst/1)

Given a Binary Search Tree (BST) with `N` nodes, find the median of its node values. The BST is structured such that:
- For any given node, all nodes in its left subtree have values less than its own value.
- All nodes in its right subtree have values greater than its own value.

**Examples:**

Example 1:
```
Input:
       6
     /   \
   3      8   
 /  \    /  \
1    4  7    9

Output: 6
Explanation: The in-order traversal of the BST yields [1, 3, 4, 6, 7, 8, 9]. The median value is 6.
```

Example 2:
```
Input:
       6
     /   \
   3      8   
 /   \    /   
1    4   7   

Output: 5
Explanation: The in-order traversal of the BST yields [1, 3, 4, 6, 7, 8]. The median is (4 + 6) / 2 = 5.
```

### Approach

1. **In-order Traversal**:
   - Perform an in-order traversal of the BST to retrieve node values in sorted order.
   - Store these values in a list (or vector in C++).

2. **Calculate Median**:
   - Determine the number of nodes `n`.
   - If `n` is odd, the median is the middle element: `v[n/2]`.
   - If `n` is even, the median is the average of the two middle elements: `(v[n/2] + v[(n/2) - 1]) / 2`.

### Intuition

- The in-order traversal of a BST produces a sorted list of its node values.
- The median of a sorted list can be directly computed based on its length (odd or even).
- This approach efficiently leverages the BST properties to calculate the median without needing additional data structures beyond a list to store values.

### Code

Below is the Python version of the provided C++ code:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def inorder(root, values):
    if not root:
        return
    inorder(root.left, values)
    values.append(root.data)
    inorder(root.right, values)

def findMedian(root):
    values = []
    inorder(root, values)
    n = len(values)
    
    if n % 2 == 0:
        return (values[n // 2] + values[(n // 2) - 1]) / 2.0
    else:
        return float(values[n // 2])

# Example usage
# Constructing a BST
root = Node(6)
root.left = Node(3)
root.right = Node(8)
root.left.left = Node(1)
root.left.right = Node(4)
root.right.left = Node(7)
root.right.right = Node(9)

print(findMedian(root))  # Output: 6.0

root2 = Node(6)
root2.left = Node(3)
root2.right = Node(8)
root2.left.left = Node(1)
root2.left.right = Node(4)
root2.right.left = Node(7)

print(findMedian(root2))  # Output: 5.0
```

### Complexity Analysis

- **Time Complexity**: O(N), where N is the number of nodes in the BST.
  - The in-order traversal visits each node once.
  - Calculating the median from the list of values takes constant time O(1).

- **Space Complexity**: O(N).
  - We store all node values in a list of size N during the in-order traversal.
  - The additional space used is proportional to the number of nodes in the tree, which is the list to store the node values.

This approach is efficient given the constraints and leverages the properties of BSTs effectively to compute the median in linear time.
