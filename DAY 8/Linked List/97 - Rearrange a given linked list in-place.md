# [Rearrange a given linked list in-place](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/)

To rearrange a singly linked list in the form \( L_0 \rightarrow L_n \rightarrow L_1 \rightarrow L_{n-1} \rightarrow L_2 \rightarrow L_{n-2} \rightarrow \ldots \) efficiently in-place, we can follow these steps:

1. **Find the Middle of the List**: Use the slow and fast pointer technique to find the middle of the linked list.

2. **Reverse the Second Half**: Reverse the second half of the list starting from the middle node.

3. **Merge the Two Halves**: Merge the two halves by alternating nodes from each half.

Let's go through the implementation of this efficient solution:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return

        # Step 1: Find the middle of the linked list
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # Step 2: Reverse the second half of the list
        prev, curr = None, slow
        while curr:
            next_node = curr.next
            curr.next = prev
            prev = curr
            curr = next_node

        # Step 3: Merge the two halves
        first, second = head, prev
        while second.next:
            # Save the next nodes
            tmp1, tmp2 = first.next, second.next

            # Reorder nodes
            first.next = second
            second.next = tmp1

            # Move to the next nodes in both halves
            first, second = tmp1, tmp2

# Helper function to print the list
def printList(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    print("->".join(map(str, result)))

# Example usage:
# Input: 1 -> 2 -> 3 -> 4
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4))))
solution = Solution()
solution.reorderList(head)
printList(head)  # Output: 1->4->2->3

# Input: 1 -> 2 -> 3 -> 4 -> 5
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
solution.reorderList(head)
printList(head)  # Output: 1->5->2->4->3
```

### Explanation

- **Finding the Middle**: We use two pointers, `slow` and `fast`, to find the middle of the linked list. The `fast` pointer moves twice as fast as the `slow` pointer. By the time `fast` reaches the end, `slow` will be at the middle.

- **Reversing the Second Half**: We reverse the second half of the list starting from the middle. This involves iterating through the second half and reversing the pointers so that they point backward instead of forward.

- **Merging the Two Halves**: We merge the two halves by alternating nodes from the first half and the reversed second half. We carefully adjust the `next` pointers to achieve the desired order.

This solution efficiently reorders the list with a time complexity of \( O(n) \) and uses \( O(1) \) additional space since the operations are done in place.
