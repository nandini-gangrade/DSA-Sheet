# [Rearrange a Linked List in Zig-Zag fashion](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)

To rearrange a linked list such that it follows a zig-zag pattern (`a < b > c < d > e < f ...`), we can use an efficient single-pass approach. This involves traversing the list while maintaining a flag to determine the desired order between the current node and the next node.

## Approach

1. **Initialize a Flag**:
   - Use a boolean flag `less` to track the desired relation between consecutive nodes.
   - Start with `less = True`, indicating that the first node should be less than the second node.

2. **Traverse the List**:
   - Iterate through the list using a pointer `current`.
   - For each pair of nodes (`current` and `current.next`), do the following:
     - If `less` is `True`, check if `current.val < current.next.val`. If not, swap their values.
     - If `less` is `False`, check if `current.val > current.next.val`. If not, swap their values.
   - Toggle the `less` flag after each comparison to switch between `<` and `>` for the next pair.

3. **Swap Values**:
   - Swap the values of the nodes instead of rearranging node pointers to achieve the desired order.

4. **Continue Until End**:
   - Continue this process until the end of the list is reached.

## Implementation

Here is the Python implementation of the above approach:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def zigzagList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head

        current = head
        # Start with the assumption that the first element should be less than the next
        less = True

        while current.next:
            if less:
                if current.val > current.next.val:
                    # Swap values
                    current.val, current.next.val = current.next.val, current.val
            else:
                if current.val < current.next.val:
                    # Swap values
                    current.val, current.next.val = current.next.val, current.val

            # Move to the next pair
            current = current.next
            # Toggle the flag
            less = not less

        return head

# Helper function to print the list
def printList(head):
    while head:
        print(head.val, end=" -> " if head.next else "\n")
        head = head.next

# Example usage:
# Input: 1 -> 2 -> 3 -> 4
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4))))
solution = Solution()
new_head = solution.zigzagList(head)
printList(new_head)  # Output: 1 -> 3 -> 2 -> 4

# Input: 11 -> 15 -> 20 -> 5 -> 10
head = ListNode(11, ListNode(15, ListNode(20, ListNode(5, ListNode(10)))))
new_head = solution.zigzagList(head)
printList(new_head)  # Output: 11 -> 20 -> 5 -> 15 -> 10
```

### Explanation of the Code

- **Line 1-3**: Defines the `ListNode` class representing a node in the linked list.
- **Line 5-30**: Implements the `zigzagList` method which rearranges the list in the desired zig-zag pattern.
- **Line 8-10**: Handles cases where the list is empty or contains only one node by returning the list unchanged.
- **Line 12-29**: Iterates through the list, checking and swapping nodes as necessary based on the `less` flag.
- **Line 33-40**: Provides a helper function to print the linked list.
- **Line 43-51**: Demonstrates usage of the `zigzagList` function with examples.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the linked list.
- **Space Complexity**: \(O(1)\), as we only use a constant amount of additional space.

This solution efficiently rearranges the linked list in a single pass while maintaining the zig-zag order.
