# Segregate even and odd nodes in a Linked List

To rearrange a linked list such that all even numbers appear before all odd numbers while maintaining their relative order, we can follow a straightforward approach:

1. **Traverse the List**:
   - Maintain two separate lists: one for even numbers and another for odd numbers.
   - Traverse the given linked list and add nodes to the respective even or odd list.

2. **Concatenate the Lists**:
   - After traversing, connect the last node of the even list to the head of the odd list.

3. **Edge Cases**:
   - If there are no even nodes, return the original list.
   - If there are no odd nodes, return the even list as it is.

This approach ensures that the order of even and odd numbers is preserved as in the input list. 

Here is the implementation in Python:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def segregateEvenOdd(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head

        even_head = even_tail = ListNode(0)
        odd_head = odd_tail = ListNode(0)
        current = head

        while current:
            if current.val % 2 == 0:
                even_tail.next = current
                even_tail = even_tail.next
            else:
                odd_tail.next = current
                odd_tail = odd_tail.next
            current = current.next

        # Concatenate the even and odd lists
        even_tail.next = odd_head.next
        odd_tail.next = None

        return even_head.next

# Helper function to print the list
def printList(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    print("->".join(map(str, result)))

# Example usage:
# Input: 17->15->8->12->10->5->4->1->7->6->NULL
head = ListNode(17, ListNode(15, ListNode(8, ListNode(12, ListNode(10, ListNode(5, ListNode(4, ListNode(1, ListNode(7, ListNode(6))))))))))
solution = Solution()
sorted_head = solution.segregateEvenOdd(head)
printList(sorted_head)  # Output: 8->12->10->4->6->17->15->5->1->7

# Input: 1->3->5->7->NULL
head = ListNode(1, ListNode(3, ListNode(5, ListNode(7))))
sorted_head = solution.segregateEvenOdd(head)
printList(sorted_head)  # Output: 1->3->5->7

# Input: 8->12->10->NULL
head = ListNode(8, ListNode(12, ListNode(10)))
sorted_head = solution.segregateEvenOdd(head)
printList(sorted_head)  # Output: 8->12->10
```

### Explanation

- **Initialization**: Two dummy nodes, `even_head` and `odd_head`, are initialized to simplify list manipulations. `even_tail` and `odd_tail` are used to keep track of the end of the even and odd lists, respectively.
  
- **Traversal and Separation**: We iterate through the linked list, appending each node to either the even list or the odd list based on the node's value.

- **Concatenation**: After all nodes are distributed between even and odd lists, we connect the end of the even list to the head of the odd list and ensure the last node points to `None`.

- **Return**: The head of the modified list is the next node of the dummy `even_head`.

This implementation efficiently rearranges the nodes in a single pass through the linked list, maintaining the relative order of even and odd nodes, with a time complexity of \(O(n)\) and space complexity of \(O(1)\).
