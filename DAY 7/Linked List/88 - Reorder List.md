# [143. Reorder List](https://leetcode.com/problems/reorder-list/description/)

To solve the problem of reordering a singly linked list in the format `L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → ...`, you can follow these steps:

### Steps to Solve

1. **Find the Middle of the List**:
   - Use the slow and fast pointer technique to find the middle node. The slow pointer moves one step at a time, while the fast pointer moves two steps at a time.

2. **Reverse the Second Half of the List**:
   - After finding the middle, reverse the second half of the list. This reversed portion will be merged with the first half to get the desired order.

3. **Merge the Two Halves**:
   - Merge the first half of the list with the reversed second half. During merging, alternate between nodes from the first half and nodes from the reversed second half.

### Detailed Solution

1. **Finding the Middle**:
   - Traverse the list with two pointers: one moving at twice the speed of the other. When the faster pointer reaches the end, the slower pointer will be at the middle.

2. **Reversing the Second Half**:
   - Use a simple reversal algorithm to reverse the nodes in the second half of the list.

3. **Merging**:
   - Merge the two halves by alternating nodes from each half.

# Code

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        if not head or not head.next or not head.next.next:
            return
        
        # Step 1: Find the middle of the linked list
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        # Step 2: Reverse the second half of the list
        second = slow.next
        slow.next = None  # Split the list into two halves
        prev = None
        while second:
            next_node = second.next
            second.next = prev
            prev = second
            second = next_node
        second = prev  # The reversed second half
        
        # Step 3: Merge the two halves
        first = head
        while second:
            tmp1 = first.next
            tmp2 = second.next
            first.next = second
            second.next = tmp1
            first = tmp1
            second = tmp2
```

### Explanation of the Code

1. **Finding the Middle**:
   - `slow` and `fast` pointers are used to find the middle of the list. `slow` will point to the middle when `fast` reaches the end.

2. **Reversing the Second Half**:
   - After finding the middle, the second half is reversed. This is done by iterating through the second half and reversing the `next` pointers.

3. **Merging**:
   - The merging is done by alternating between nodes from the first half and the reversed second half. `tmp1` and `tmp2` are used to keep track of the next nodes in each half during merging.

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the linked list. Each node is visited a constant number of times.
- **Space Complexity**: \(O(1)\). The solution modifies the list in place and uses a constant amount of extra space.

This approach efficiently reorders the linked list as required while maintaining linear time complexity and constant space complexity.
