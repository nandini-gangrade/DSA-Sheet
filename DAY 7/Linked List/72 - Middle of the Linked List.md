# [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)

In a linked list, finding the middle node can be tricky due to its one-way traversal nature. The key idea here is to use two pointers:

1. **Slow Pointer**: Moves one step at a time.
2. **Fast Pointer**: Moves two steps at a time.

When the fast pointer reaches the end of the list, the slow pointer will be at the middle. If the list has an even number of nodes, the slow pointer will end up on the second of the two middle nodes, which is exactly what we want.

### Explanation of Examples

- **Example 1**:
  - **Input**: [1, 2, 3, 4, 5]
  - **Output**: The middle node is 3, so the output list is [3, 4, 5].

- **Example 2**:
  - **Input**: [1, 2, 3, 4, 5, 6]
  - **Output**: The middle node is the second middle node, 4, so the output list is [4, 5, 6].
  - 
## Approach

1. Initialize two pointers, `slow` and `fast`, both pointing to the head of the list.
2. Move the `slow` pointer one step and the `fast` pointer two steps in each iteration.
3. When the `fast` pointer reaches the end (`fast` is `None` or `fast.next` is `None`), the `slow` pointer will be at the middle node.

## Code

Here's how you can implement this in Python:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def middleNode(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # Initialize two pointers, both start at the head of the list
        slow = head
        fast = head
        
        # Move fast pointer two steps and slow pointer one step until fast reaches the end
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        # Slow is now pointing at the middle node
        return slow
```

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the list. We traverse the list once.
- **Space Complexity**: \(O(1)\). We only use two pointers and do not allocate any additional space that grows with input size.


This approach efficiently finds the middle of the linked list and returns it, satisfying the constraints and requirements given in the problem.
