# [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

To reverse a singly linked list, you can use either an iterative approach or a recursive approach. Below are both methods implemented in Python:

### Iterative Approach

In the iterative approach, you use three pointers to reverse the linked list: `prev`, `current`, and `next`. The idea is to iterate through the linked list while reversing the direction of the `next` pointers.

### Recursive Approach

In the recursive approach, you reverse the rest of the list first, then fix the current node's `next` pointer to point to the previous node.

## Iterative Approach

**Algorithm**:
1. Initialize three pointers: `prev` as `None`, `current` as `head`, and `next` as `None`.
2. Iterate through the linked list.
   - Before changing the `next` of `current`, store the next node.
   - Reverse the `next` pointer of `current` to point to `prev`.
   - Move `prev` to `current`.
   - Move `current` to the next node.
3. Once the loop completes, `prev` will be the new head of the reversed list.

**Time Complexity**: \(O(n)\)  
**Space Complexity**: \(O(1)\)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        current = head
        
        while current:
            next_node = current.next  # Store the next node
            current.next = prev       # Reverse the link
            prev = current            # Move prev up
            current = next_node       # Move to the next node
            
        return prev
```

## Recursive Approach

**Algorithm**:
1. Define a recursive function that takes the `head` of the list as input.
2. Base Case: If `head` is `None` or `head.next` is `None`, return `head` (the list is empty or has only one node).
3. Recursively reverse the rest of the list.
4. Adjust the pointers: Set the `next` pointer of the next node (after the reversal) to point to the current node.
5. Set the `next` pointer of the current node to `None`.

**Time Complexity**: \(O(n)\)  
**Space Complexity**: \(O(n)\) due to the recursion stack

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # Helper function for recursion
        def reverse_recursive(node):
            if not node or not node.next:
                return node
            new_head = reverse_recursive(node.next)
            node.next.next = node
            node.next = None
            return new_head
        
        return reverse_recursive(head)
```

### Explanation of Both Approaches

- **Iterative Approach**: 
  - This method is efficient with constant space complexity and avoids the overhead of recursion. It's straightforward to implement and understand.

- **Recursive Approach**: 
  - This method leverages the call stack to reverse the list but may be less memory-efficient due to the stack space used in recursion. It is elegant and concise.

Both methods are valid, and the choice depends on the constraints and preferences regarding space and simplicity.
