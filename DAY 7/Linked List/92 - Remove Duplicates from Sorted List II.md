# [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

To remove all nodes with duplicate values from a sorted linked list, you can use a dummy node to help manage edge cases where the head itself is a duplicate. Here's how you can implement the solution:

### Steps

1. **Initialize a Dummy Node**:
   - Create a `dummy` node that points to the head of the list. This helps handle edge cases where the head itself might need to be removed.
   - Use a `prev` pointer initialized to `dummy` to track the last node before the duplicate sequence.

2. **Iterate Through the List**:
   - Use a `current` pointer to traverse the list.
   - For each node, check if it has duplicates by comparing it with the next node.
   - If duplicates are found, skip all nodes with the same value.
   - If no duplicates are found, move the `prev` pointer forward.

3. **Skip Duplicates**:
   - When duplicates are detected, connect `prev.next` to the node after the last duplicate.

4. **Return the Modified List**:
   - The new head of the list will be `dummy.next`.

## Python Code

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # Create a dummy node to help with edge cases
        dummy = ListNode(0)
        dummy.next = head
        
        # `prev` points to the last node before the duplicate sequence
        prev = dummy
        
        # Iterate through the list
        current = head
        while current:
            # Check if it's a start of a duplicate sequence
            if current.next and current.val == current.next.val:
                # Skip all nodes with the same value
                while current.next and current.val == current.next.val:
                    current = current.next
                # Connect prev.next to the node after the last duplicate
                prev.next = current.next
            else:
                # No duplicates detected, move prev forward
                prev = prev.next
            
            # Move current forward
            current = current.next
        
        return dummy.next
```

### Explanation

- **Dummy Node**: The `dummy` node allows you to easily return the new head of the list, especially when the head itself has duplicates.
- **Prev Pointer**: Tracks the node before the current node. This is important for connecting the last non-duplicate node to the node after the duplicates.
- **Skipping Duplicates**: When a sequence of duplicates is found, `current` is moved past all duplicates, and `prev.next` is updated to skip these nodes.
- **Maintaining Order**: The solution maintains the relative order of non-duplicate nodes because it only changes pointers when duplicates are found.

## Complexity

- **Time Complexity**: \(O(n)\), where \( n \) is the number of nodes in the linked list, since each node is processed once.
- **Space Complexity**: \(O(1)\), as only a constant amount of extra space is used for pointers and the dummy node.
