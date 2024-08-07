# [Binary Tree to DLL](https://www.geeksforgeeks.org/problems/binary-tree-to-dll/1)

### Approach

1. **Inorder Traversal**:
   - Perform an inorder traversal of the binary tree. Inorder traversal of a binary search tree (BST) results in nodes being visited in ascending order. For a general binary tree, it will result in nodes being visited from left to right as they appear in the binary tree.
   - Collect the nodes' values during this traversal.

2. **Construct DLL**:
   - Create a DLL from the list of values obtained from the inorder traversal.
   - Use the `left` pointer of nodes as the previous pointer and the `right` pointer as the next pointer in the DLL.

### Python Code

Here is a complete Python implementation based on the given approach:

```python
class Node:
    def __init__(self, value):
        self.left = None  # This will be used as previous in DLL
        self.data = value
        self.right = None  # This will be used as next in DLL

class Solution:
    def __init__(self):
        self.head = None
        self.prev = None
    
    def inorderTraversal(self, root):
        if not root:
            return
        
        # Traverse the left subtree
        self.inorderTraversal(root.left)
        
        # Process current node
        if not self.head:
            # First node is the head of the DLL
            self.head = root
            self.prev = root
        else:
            # Adjust the pointers to maintain the DLL properties
            self.prev.right = root
            root.left = self.prev
            self.prev = root
        
        # Traverse the right subtree
        self.inorderTraversal(root.right)
    
    def bToDLL(self, root):
        self.head = None
        self.prev = None
        self.inorderTraversal(root)
        return self.head

# Helper function to print DLL from head to tail
def printDLL(head):
    curr = head
    while curr:
        print(curr.data, end=' ')
        curr = curr.right
    print()

# Helper function to print DLL from tail to head
def printDLLReverse(head):
    if not head:
        return
    # Go to the end of the DLL
    while head.right:
        head = head.right
    # Print from tail to head
    while head:
        print(head.data, end=' ')
        head = head.left
    print()

# Example usage:
# Construct a binary tree
root = Node(10)
root.left = Node(20)
root.right = Node(30)
root.left.left = Node(40)
root.left.right = Node(60)

solution = Solution()
dll_head = solution.bToDLL(root)

# Print DLL in forward direction
print("DLL from head to tail:")
printDLL(dll_head)

# Print DLL in reverse direction
print("DLL from tail to head:")
printDLLReverse(dll_head)
```

### Explanation

1. **Inorder Traversal**:
   - The `inorderTraversal` function recursively traverses the tree in an inorder manner. It processes the node values and adjusts the `left` and `right` pointers to form the DLL.

2. **Construct DLL**:
   - The `bToDLL` function initializes the `head` and `prev` pointers and starts the inorder traversal to construct the DLL.

3. **Printing DLL**:
   - The `printDLL` function prints the DLL from head to tail.
   - The `printDLLReverse` function prints the DLL from tail to head by first traversing to the end of the DLL and then moving backward.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the binary tree. Each node is visited once.
- **Space Complexity**: \(O(H)\), where \(H\) is the height of the tree due to the recursion stack. This is optimal for this problem.
