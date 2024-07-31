# [148. Sort List](https://leetcode.com/problems/sort-list/description/)

To sort a linked list in ascending order with an optimal time complexity of \(O(n \log n)\) and \(O(1)\) extra space, we can use the **merge sort** algorithm. Merge sort is a divide-and-conquer algorithm that efficiently sorts the list by splitting it into two halves, recursively sorting each half, and then merging the two sorted halves together.

## Approach

1. **Find the Middle of the List**:
   - Use the slow and fast pointer technique to find the middle node of the list. This helps split the list into two halves.

2. **Recursively Sort Each Half**:
   - Apply merge sort recursively on each half to sort them individually.

3. **Merge the Sorted Halves**:
   - Use the merge function to combine the two sorted halves into a single sorted list.

4. **Base Case**:
   - If the list is empty or contains only a single node, return it as it is already sorted.

## Implementation

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head

        # Function to split the list into two halves
        def getMid(head):
            slow, fast = head, head
            prev = None
            while fast and fast.next:
                prev = slow
                slow = slow.next
                fast = fast.next.next
            if prev:
                prev.next = None  # Break the list into two halves
            return slow

        # Function to merge two sorted lists
        def merge(l1, l2):
            dummy = ListNode(-1)
            current = dummy
            while l1 and l2:
                if l1.val < l2.val:
                    current.next = l1
                    l1 = l1.next
                else:
                    current.next = l2
                    l2 = l2.next
                current = current.next
            if l1:
                current.next = l1
            else:
                current.next = l2
            return dummy.next

        # Recursive merge sort
        mid = getMid(head)
        left = self.sortList(head)
        right = self.sortList(mid)
        return merge(left, right)

# Helper function to print the list
def printList(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    print("->".join(map(str, result)))

# Example usage:
# Input: 4 -> 2 -> 1 -> 3
head = ListNode(4, ListNode(2, ListNode(1, ListNode(3))))
solution = Solution()
sorted_head = solution.sortList(head)
printList(sorted_head)  # Output: 1 -> 2 -> 3 -> 4

# Input: -1 -> 5 -> 3 -> 4 -> 0
head = ListNode(-1, ListNode(5, ListNode(3, ListNode(4, ListNode(0)))))
sorted_head = solution.sortList(head)
printList(sorted_head)  # Output: -1 -> 0 -> 3 -> 4 -> 5
```

### Explanation of the Code

- **Line 1-3**: Defines the `ListNode` class representing a node in the linked list.
- **Line 5-40**: Implements the `sortList` method which sorts the linked list using merge sort.
- **Line 11-19**: Implements `getMid` function to split the list into two halves.
- **Line 21-34**: Implements `merge` function to merge two sorted lists into one.
- **Line 37-39**: Demonstrates usage of the `sortList` function with examples.

## Complexity

- **Time Complexity**: \(O(n \log n)\), where \(n\) is the number of nodes in the linked list.
- **Space Complexity**: \(O(1)\) additional space (excluding recursive stack space).

This implementation efficiently sorts the linked list using the merge sort algorithm while maintaining \(O(n \log n)\) time complexity and minimizing space usage.
