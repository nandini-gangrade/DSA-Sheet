# [Delete nodes having greater value on right](https://www.geeksforgeeks.org/problems/delete-nodes-having-greater-value-on-right/1)

To solve the problem of removing nodes from a singly linked list such that any node with a greater node to its right is removed, we can use a reverse traversal approach. Here’s a step-by-step explanation:

## Approach

1. **Reverse Traversal**:
   - Traverse the linked list from right to left (which can be simulated by reversing the list).
   - Keep track of the maximum value encountered during the traversal. Nodes that have a value less than this maximum value will be removed.
   - Build a new list with nodes that are not removed.

2. **Reverse the List**:
   - Reverse the input linked list.
   - Traverse the reversed list to determine which nodes to keep.
   - Reverse the modified list again to restore the original order.

### Steps

1. **Reverse the List**:
   - Reverse the given linked list to facilitate right-to-left traversal.

2. **Traverse and Filter Nodes**:
   - Traverse the reversed list and maintain a variable to track the maximum value found.
   - For each node, if its value is greater than or equal to the maximum value, keep it and update the maximum value.

3. **Reverse the Modified List**:
   - After filtering, reverse the list again to restore the original order.

## Implementation

```python
class Node:
    def __init__(self, x):
        self.data = x
        self.next = None

class Solution:
    def compute(self, head):
        # Helper function to reverse the linked list
        def reverse(head):
            prev = None
            current = head
            while current:
                next_node = current.next
                current.next = prev
                prev = current
                current = next_node
            return prev

        # Reverse the linked list
        head = reverse(head)
        
        # Traverse the reversed list and keep track of the maximum value
        max_node = head
        current = head
        
        while current and current.next:
            if current.next.data < max_node.data:
                # Remove the node
                current.next = current.next.next
            else:
                # Update max_node and move to next node
                max_node = current.next
                current = current.next
        
        # Reverse the list again to restore the original order
        return reverse(head)
```

### Explanation

1. **Reverse Function**:
   - Reverses the given linked list to allow right-to-left traversal.

2. **Compute Function**:
   - Calls `reverse` to get a reversed list.
   - Traverses the reversed list to remove nodes with smaller values.
   - Calls `reverse` again to restore the original order of the nodes.
  
## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the list. Each list reversal and traversal operation takes linear time.
- **Space Complexity**: \(O(1)\), as no extra space is used apart from a few pointers.


This approach ensures that the linked list is processed in linear time with constant space, making it efficient and suitable for the given constraints.
