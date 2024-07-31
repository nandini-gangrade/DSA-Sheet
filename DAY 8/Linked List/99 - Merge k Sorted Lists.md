# [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)

To reverse nodes in groups of `k` in a singly linked list, you can follow this approach:

### Approach

1. **Check the Length of the List**: Determine if there are at least `k` nodes left in the list to reverse. If not, return the list as is.

2. **Reverse Nodes in Groups**: Reverse nodes in groups of `k` and link the reversed segments together.

3. **Handle Remaining Nodes**: If there are fewer than `k` nodes left, they should remain as they are.

### Solution Code

Here's a Python implementation of this approach:

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        # Helper function to reverse a linked list
        def reverseLinkedList(head, k):
            prev = None
            curr = head
            while k > 0:
                next_node = curr.next
                curr.next = prev
                prev = curr
                curr = next_node
                k -= 1
            return prev
        
        # Helper function to get the length of the linked list
        def getLength(head):
            length = 0
            while head:
                length += 1
                head = head.next
            return length
        
        # Calculate the length of the linked list
        length = getLength(head)
        
        # Create a dummy node to simplify the head management
        dummy = ListNode(-1)
        dummy.next = head
        prev_end = dummy
        
        # Reverse nodes in groups of k
        while length >= k:
            # Find the start and end of the current group
            group_start = prev_end.next
            group_end = group_start
            for _ in range(k - 1):
                group_end = group_end.next
            
            # Get the next group start
            next_group_start = group_end.next
            
            # Reverse the current group
            group_end.next = None
            prev_end.next = reverseLinkedList(group_start, k)
            group_start.next = next_group_start
            
            # Move prev_end to the end of the reversed group
            prev_end = group_start
            
            # Decrement the length of the remaining nodes
            length -= k
        
        return dummy.next
```

### Explanation

1. **`reverseLinkedList` Function**: This function reverses `k` nodes starting from a given head node. It returns the new head of the reversed segment.

2. **`getLength` Function**: This function calculates the total length of the linked list.

3. **Main Logic**:
   - Calculate the total length of the list to determine how many complete groups of `k` nodes can be reversed.
   - Use a dummy node to handle edge cases where the head of the list might change.
   - Iterate through the list, reversing nodes in groups of `k` and linking them together.
   - If fewer than `k` nodes are left at the end, they remain unchanged.

This approach maintains a time complexity of O(n) and uses O(1) extra space, satisfying the problem's constraints.
