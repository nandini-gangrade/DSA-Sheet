# [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/description/)

To solve the problem of reversing a segment of a singly linked list from position `left` to position `right`, you need to manipulate the pointers in the list carefully. The goal is to reverse the segment in-place and then reconnect the reversed segment with the rest of the list.

### Steps to Solve the Problem

1. **Identify the Segment to Reverse**:
   - Traverse the list to reach the `left` position and keep track of the previous node to `left` and the node at `left`.

2. **Reverse the Segment**:
   - Reverse the segment from `left` to `right` by adjusting the pointers within the segment.

3. **Reconnect the Reversed Segment**:
   - Connect the reversed segment back to the list: update the `next` of the node before `left` to point to the new head of the reversed segment, and update the `next` of the node at `left` to point to the node after `right`.

### Detailed Explanation

1. **Traversing to `left`**:
   - Use a dummy node to handle cases where `left` is `1`. This dummy node helps simplify edge cases by providing a consistent starting point.
   - Traverse to the node just before `left` and the node at `left`.

2. **Reversing the Segment**:
   - Use three pointers (`prev`, `curr`, `next`) to reverse the nodes within the segment. Adjust the pointers of the nodes to achieve the reversal.

3. **Reconnecting**:
   - Once reversed, reconnect the segment to the rest of the list. Update the `next` pointers to ensure the reversed segment integrates smoothly into the original list.

# Code

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseBetween(self, head, left, right):
        """
        :type head: ListNode
        :type left: int
        :type right: int
        :rtype: ListNode
        """
        # Create a dummy node that points to the head
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy
        
        # Move prev to the node just before the left-th node
        for _ in range(left - 1):
            prev = prev.next
        
        # The node at the start of the reversal
        reverse_start = prev.next
        curr = reverse_start.next
        
        # Reverse the sublist from left to right
        for _ in range(right - left):
            reverse_start.next = curr.next
            curr.next = prev.next
            prev.next = curr
            curr = reverse_start.next
        
        return dummy.next
```

### Explanation of the Code

1. **Dummy Node**:
   - A dummy node is created and points to the head of the list. This helps in handling the edge case where the reversal starts at the very beginning of the list.

2. **Traversal to `left`**:
   - Traverse the list to find the node just before `left`. The `prev` pointer will help in reconnecting the reversed segment.

3. **Reversing the Segment**:
   - Reverse the segment by adjusting pointers within the segment. The `curr` pointer is used to traverse and reverse nodes.

4. **Reconnect**:
   - After reversing, connect the reversed segment back to the rest of the list using the pointers updated during the reversal.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the list. The algorithm traverses the list a few times but each node is processed a constant number of times.
- **Space Complexity**: \(O(1)\) as the reversal is done in-place and no additional data structures are used.

This approach efficiently handles the problem in one pass, reversing the specified segment while maintaining overall list structure.
