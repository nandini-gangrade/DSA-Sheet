# [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

To remove the nth node from the end of a singly linked list in one pass, you can use a two-pointer technique. Here's a step-by-step approach to achieve this:

### Steps to Solve

1. **Initialize Two Pointers**:
   - Start both pointers (`first` and `second`) at the head of the list.

2. **Advance the First Pointer**:
   - Move the `first` pointer `n` steps ahead. This positions the `first` pointer such that the gap between the `first` and `second` pointers is `n` nodes.

3. **Move Both Pointers Together**:
   - Move both pointers together until the `first` pointer reaches the end of the list. At this point, the `second` pointer will be right before the node that needs to be removed.

4. **Remove the Node**:
   - Adjust the `next` pointer of the node just before the node to be removed to skip over the node to be removed.

5. **Handle Edge Cases**:
   - If `n` is equal to the length of the list, it means you need to remove the head of the list.

### Example

For the input list `[1, 2, 3, 4, 5]` and `n = 2`:

- After advancing the `first` pointer `n` steps, the list looks like: `first -> 4`, `second -> 1`.
- Move both pointers together until `first` reaches the end, resulting in `second` pointing to the node before the node to be removed (`4` in this case).
- Adjust the `next` pointer of `second` to skip over the node to be removed.

# Code

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        # Initialize dummy node to handle edge cases such as removing the head
        dummy = ListNode(0)
        dummy.next = head
        first = second = dummy
        
        # Advance the first pointer by n + 1 steps
        for _ in range(n + 1):
            first = first.next
        
        # Move both pointers until the first reaches the end
        while first:
            first = first.next
            second = second.next
        
        # Remove the nth node from the end
        second.next = second.next.next
        
        return dummy.next
```

### Explanation of the Code

1. **Dummy Node**:
   - A dummy node is used to simplify edge cases, like removing the head of the list. It points to the original head.

2. **Advancing the First Pointer**:
   - The `first` pointer is moved `n + 1` steps ahead to ensure that the gap between `first` and `second` is `n` nodes.

3. **Moving Both Pointers**:
   - Both pointers are moved together until the `first` pointer reaches the end of the list. At this point, the `second` pointer will be pointing just before the node to be removed.

4. **Removing the Node**:
   - The `second.next` is adjusted to skip over the node to be removed.

## Complexity

- **Time Complexity**: \(O(sz)\), where `sz` is the number of nodes in the linked list. Each node is visited once.
- **Space Complexity**: \(O(1)\). The solution uses a constant amount of extra space, excluding the input and output.

This approach efficiently removes the nth node from the end of the list in a single pass, making it optimal for the given constraints.
