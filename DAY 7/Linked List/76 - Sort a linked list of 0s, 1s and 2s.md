# [Sort a linked list of 0s, 1s and 2s](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/)

Given a linked list containing only `0`s, `1`s, and `2`s, the task is to sort the linked list in ascending order. The sorted list should have all `0`s followed by `1`s and then `2`s.

## Approach

To solve this problem, you can use a frequency counting method:

1. **Count Occurrences**: Traverse the linked list and count the number of `0`s, `1`s, and `2`s.
2. **Repopulate List**: Traverse the list again and update each node's value according to the counts obtained.

### Steps

1. **Initialize Counters**: Use three counters to keep track of the number of `0`s, `1`s, and `2`s.
2. **First Pass - Count Elements**:
   - Traverse the list from the head to the end.
   - For each node, increment the respective counter (`n0`, `n1`, `n2`).
3. **Second Pass - Update Values**:
   - Traverse the list again.
   - Set the first `n0` nodes to `0`, the next `n1` nodes to `1`, and the remaining nodes to `2`.

## Code

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def sortList(self, head):
        # Step 1: Count the number of 0s, 1s, and 2s
        n0 = n1 = n2 = 0
        current = head
        
        while current:
            if current.val == 0:
                n0 += 1
            elif current.val == 1:
                n1 += 1
            elif current.val == 2:
                n2 += 1
            current = current.next
        
        # Step 2: Reassign values based on counts
        current = head
        while current:
            if n0 > 0:
                current.val = 0
                n0 -= 1
            elif n1 > 0:
                current.val = 1
                n1 -= 1
            else:
                current.val = 2
            current = current.next
        
        return head
```

### Explanation

1. **Counting Phase**:
   - Initialize counters `n0`, `n1`, and `n2` to zero.
   - Traverse the list and increment the appropriate counter based on the value of each node.

2. **Updating Phase**:
   - Traverse the list again.
   - For each node, set the value to `0` if `n0` is greater than `0`, decrement `n0`.
   - Otherwise, set the value to `1` if `n1` is greater than `0`, decrement `n1`.
   - If neither `n0` nor `n1` is greater than `0`, set the value to `2`.

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the linked list. The list is traversed twice.
- **Space Complexity**: \(O(1)\), as no additional space is used beyond the input list.

This method efficiently sorts a linked list with `0`s, `1`s, and `2`s in linear time and constant space, leveraging the fact that there are only three distinct values to handle.
