# [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/description/)

## Optimized Iterative Approach

1. **Use a Stack**:
   - Traverse the list and use a stack to keep track of nodes that need to be processed when their children are encountered.
   - This avoids the overhead of recursive function calls and is more memory efficient for deep lists.

2. **Iterative Flattening**:
   - Traverse the list using a `while` loop.
   - When a child node is encountered, push the `next` node onto the stack and update the `next` pointer to the child node.
   - Continue processing nodes from the stack until it is empty.

##  Code

```python
class Node:
    def __init__(self, val=0, prev=None, next=None, child=None):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child

class Solution:
    def flatten(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        if not head:
            return None
        
        # Initialize the stack with the head of the list
        stack = [head]
        prev = None  # To keep track of the last node processed
        
        while stack:
            current = stack.pop()  # Get the node from the top of the stack
            
            if prev:
                prev.next = current
                current.prev = prev
            
            # If there's a next node, push it onto the stack
            if current.next:
                stack.append(current.next)
            
            # If there's a child node, process it and set it as the next node
            if current.child:
                stack.append(current.child)
                current.child = None  # Remove the child pointer
            
            # Move the prev pointer to the current node
            prev = current
        
        return head
```

### Explanation of the Code

1. **Initialization**:
   - Use a stack to manage nodes during traversal.
   - Start with the head of the list on the stack.

2. **Processing**:
   - While there are nodes in the stack:
     - Pop the node from the stack.
     - If a previous node exists, link it to the current node.
     - Push the next node (if any) onto the stack.
     - Push the child node (if any) onto the stack and set `current.child` to `None`.

3. **Linking**:
   - Maintain the `prev` pointer to properly set the `prev` pointer of each node.

## Complexity

- **Time Complexity**: \(O(N)\), where `N` is the total number of nodes, including those in child lists. Each node is processed once.
- **Space Complexity**: \(O(N)\) for the stack, which is proportional to the number of nodes.

This iterative approach avoids deep recursion and manages the flattening process more efficiently, especially for large lists with deep child structures.
