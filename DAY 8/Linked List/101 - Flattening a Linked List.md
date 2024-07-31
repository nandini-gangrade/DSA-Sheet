# [Flattening a Linked List](https://www.geeksforgeeks.org/problems/flattening-a-linked-list/1)

Given a linked list where each node has a pointer to another sorted linked list (bottom list), you need to flatten the entire structure into a single sorted linked list.

## Approach

1. **Merge Two Bottom Lists:**
   - Implement a function to merge two sorted bottom lists into a single sorted list.

2. **Flatten the List:**
   - Recursively flatten the right-side linked lists.
   - Merge the current list with the flattened right-side list.

## Code

```python
class Node:
    def __init__(self, d):
        self.data = d
        self.next = None
        self.bottom = None

class Solution:
    def mergeSort(self, head1, head2):
        # Base cases
        if not head1:
            return head2
        if not head2:
            return head1
        
        # Recursive merge
        if head1.data < head2.data:
            result = head1
            result.bottom = self.mergeSort(head1.bottom, head2)
        else:
            result = head2
            result.bottom = self.mergeSort(head1, head2.bottom)
        
        return result
    
    def flatten(self, root):
        if not root:
            return None
        
        # Flatten the right list
        right = self.flatten(root.next)
        
        # Merge the current list with the flattened right list
        return self.mergeSort(root, right)
```

### Explanation

1. **Merge Two Sorted Bottom Lists:**
   - The `mergeSort` function merges two sorted bottom lists into a single sorted list.
   - It recursively compares the nodes and attaches the smaller node to the result list.

2. **Flatten the Linked List:**
   - The `flatten` function recursively flattens the right side of the list.
   - It then merges the current list with the flattened right side using the `mergeSort` function.

## Complexity

- **Time Complexity:** O(N * log N)
  - The flatten function recursively processes each node and merges lists. The merge operation takes linear time relative to the size of the lists.
- **Space Complexity:** O(N)
  - Due to recursion and the extra space used for merging.

This Python implementation ensures that the flattened list maintains the sorted order and handles all nodes efficiently.
