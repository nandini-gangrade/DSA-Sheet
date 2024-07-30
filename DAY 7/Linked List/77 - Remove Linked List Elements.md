# [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)

To solve the problem of removing all nodes from a linked list that have a specific value, you need to traverse the list and skip nodes that match the given value. This operation needs to handle various edge cases, such as when the head itself needs to be removed or when the list is empty.

## Approach

1. **Initialize a Dummy Node**:
   - Create a dummy node that acts as a placeholder before the head of the linked list. This helps simplify the code, especially when the node to be removed is the head node itself.

2. **Traversal**:
   - Use a pointer to traverse the list, checking each node's value.
   - If a node's value matches the target value (`val`), adjust the `next` pointer of the previous node to skip the current node.
   - Continue until you reach the end of the list.

3. **Return the New Head**:
   - After the traversal, the dummy node's next pointer will point to the new head of the list, which excludes all nodes with the target value.

## Code Implementation

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeElements(self, head, val):
        # Create a dummy node to handle cases where the head needs to be removed
        dummy = ListNode(-1)
        dummy.next = head
        
        # Initialize current pointer
        current = dummy
        
        # Traverse the list
        while current and current.next:
            if current.next.val == val:
                # Skip the node with the value equal to 'val'
                current.next = current.next.next
            else:
                # Move to the next node
                current = current.next
        
        # Return the new head, which is the next of the dummy node
        return dummy.next
```

## Explanation

1. **Dummy Node**:
   - `dummy` is used to handle edge cases where the head node itself needs to be removed. The `dummy` node's `next` points to the original head.

2. **Traversing and Removing**:
   - `current` starts at the dummy node. For each node, check if `current.next.val` equals `val`.
   - If it does, bypass the node by setting `current.next` to `current.next.next`.
   - Otherwise, move `current` to the next node.

3. **Return New Head**:
   - After processing all nodes, `dummy.next` points to the new head of the list (excluding nodes with the value `val`).

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the linked list. Each node is visited exactly once.
- **Space Complexity**: \(O(1)\), as no additional space is used beyond the input list.

This approach efficiently handles the problem of removing nodes with a specific value from a singly linked list.
