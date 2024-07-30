# [Rearrange a Linked List in Zig-Zag fashion](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)

To rearrange the linked list in a zig-zag pattern such that the elements alternate between less than and greater than (`<, >`), we can follow a single-pass approach that uses a flag to keep track of the desired relation between consecutive nodes. Here's a detailed explanation of the approach and its implementation:

## Approach

1. **Initialize a Flag**:
   - Use a boolean flag `less` to indicate the desired relation between the current node and the next node. 
   - Start with `less = True`, which means the first node should be less than the next node.

2. **Traverse the List**:
   - Iterate through the linked list with a pointer `current` starting from the head.
   - For each pair of nodes (`current` and `current.next`), check the current value of the flag.
     - If `less` is `True`, ensure `current.val < current.next.val`. If not, swap the values.
     - If `less` is `False`, ensure `current.val > current.next.val`. If not, swap the values.
   - Toggle the `less` flag after processing each pair to switch the desired relation for the next pair.

3. **Swap Nodes**:
   - Swap the values of nodes instead of rearranging node pointers for simplicity.

4. **Continue Until the End**:
   - Continue this process until the end of the list is reached.

## Implementation

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
- **Line 8-10**: Returns the list unchanged if it's empty or contains only one node.
- **Line 12-29**: Iterates through the list, checking and swapping nodes as necessary based on the `less` flag.
- **Line 33-40**: Provides a helper function to print the linked list.
- **Line 43-51**: Demonstrates usage of the `zigzagList` function with examples.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes in the linked list. We only traverse the list once.
- **Space Complexity**: \(O(1)\), as we are using only a constant amount of extra space.

This approach efficiently rearranges the linked list in the required zig-zag pattern in a single pass.
