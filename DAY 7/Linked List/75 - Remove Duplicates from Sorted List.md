# [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

Given the head of a sorted linked list, your task is to remove all duplicate elements such that each element appears only once. The linked list is already sorted in ascending order.

### Explanation of Examples

- **Example 1**:
  - **Input**: `[1, 1, 2]`
  - **Output**: `[1, 2]`
  - **Explanation**: The value `1` appears twice. The second `1` is removed, leaving `[1, 2]`.

- **Example 2**:
  - **Input**: `[1, 1, 2, 3, 3]`
  - **Output**: `[1, 2, 3]`
  - **Explanation**: The values `1` and `3` each appear twice. The duplicate values are removed, leaving `[1, 2, 3]`.


## Intuition

Since the linked list is sorted, all duplicates will be next to each other. Thus, you can traverse the list and simply remove any node whose value is the same as the next node's value.

## Approach

1. **Initialize**: Start with the head of the linked list.
2. **Traverse the Linked List**:
   - For each node, compare its value with the value of the next node.
   - If they are the same, skip the next node.
   - Continue this process until the end of the list is reached.
3. **Return the Modified List**: After processing all nodes, return the head of the modified list.

### Python Code

Here’s how you can implement this approach in Python:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        current = head
        
        while current and current.next:
            if current.val == current.next.val:
                # Skip the next node
                current.next = current.next.next
            else:
                # Move to the next node
                current = current.next
        
        return head
```

### Explanation

- **Initialization**: Set `current` to the head of the linked list.
- **Traversal**:
  - **Compare**: Check if the value of the `current` node is equal to the value of the `current.next` node.
  - **Skip Duplicates**: If they are equal, update the `current.next` to `current.next.next`, effectively removing the duplicate node.
  - **Move Forward**: If they are not equal, simply move to the next node.
- **Return**: Return the head of the modified linked list.

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the linked list. Each node is processed once.
- **Space Complexity**: \(O(1)\), as no extra space is used beyond the given list.

This solution efficiently removes duplicates from a sorted linked list with a linear time complexity and constant space usage.
