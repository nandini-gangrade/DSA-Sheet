# [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

Given the head of a singly linked list, determine if the linked list has a cycle in it. A cycle occurs if there is some node in the list that can be reached again by continuously following the next pointer. The task is to return `true` if there is a cycle in the linked list, otherwise return `false`.

### Explanation of Examples

- **Example 1**:
  - **Input**: [3, 2, 0, -4], pos = 1
  - **Output**: `true`
  - **Explanation**: There is a cycle in the linked list, with the tail connecting back to the 1st node.

- **Example 2**:
  - **Input**: [1, 2], pos = 0
  - **Output**: `true`
  - **Explanation**: The list contains a cycle with the tail connecting back to the head.

- **Example 3**:
  - **Input**: [1], pos = -1
  - **Output**: `false`
  - **Explanation**: There is no cycle in the linked list.

## Intuition

The problem can be solved efficiently using Floyd's Tortoise and Hare algorithm. The idea is to use two pointers that traverse the list at different speeds. If there is a cycle, these pointers will eventually meet. This method ensures that we detect cycles in \(O(N)\) time complexity and \(O(1)\) space complexity.

## Approach

1. **Initialize Two Pointers**:
   - `slow`: This pointer moves one step at a time.
   - `fast`: This pointer moves two steps at a time.

2. **Traverse the List**:
   - Start both `slow` and `fast` at the head of the list.
   - Move `slow` one step and `fast` two steps in each iteration.
   - If `fast` or `fast.next` becomes `None`, there is no cycle, and we return `false`.
   - If `slow` equals `fast`, a cycle is detected, and we return `true`.

This approach leverages the fact that, in a cycle, the fast pointer will eventually "lap" the slow pointer.

## Python Code

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        # Edge case: if the list is empty or has only one node
        if head is None or head.next is None:
            return False
        
        slow = head
        fast = head.next
        
        # Traverse the list
        while slow != fast:
            # If fast or fast.next is None, no cycle exists
            if fast is None or fast.next is None:
                return False
            
            slow = slow.next         # Move slow by one step
            fast = fast.next.next    # Move fast by two steps
        
        return True  # Cycle detected
```

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the linked list. Both pointers traverse the list at most once.
- **Space Complexity**: \(O(1)\), as only a constant amount of extra space is used (two pointers).

This solution efficiently detects cycles by using a two-pointer technique, ensuring optimal time and space performance.
