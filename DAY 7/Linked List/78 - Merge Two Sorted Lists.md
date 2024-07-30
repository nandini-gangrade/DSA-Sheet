# [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)

To merge two sorted linked lists into one sorted linked list, you can use a two-pointer technique. This method is efficient and straightforward, leveraging the fact that both input lists are already sorted.

## Approach

1. **Initialize a Dummy Node**:
   - Use a dummy node to act as a placeholder for the merged list. This helps simplify handling the head of the merged list and makes it easier to manage the current node during the merging process.

2. **Traverse Both Lists**:
   - Use two pointers to traverse both linked lists.
   - Compare the values of the nodes pointed to by the two pointers and attach the smaller node to the merged list.
   - Move the pointer forward in the list from which the node was taken.

3. **Attach Remaining Nodes**:
   - Once one of the lists is exhausted, attach the remaining nodes from the other list directly to the merged list since they are already sorted.

4. **Return the Merged List**:
   - Return the node following the dummy node, which represents the head of the merged linked list.

## Code

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1, list2):
        """
        :type list1: Optional[ListNode]
        :type list2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        # Initialize a dummy node and a pointer to build the new list
        dummy = ListNode(-1)
        current = dummy
        
        # Traverse both lists
        while list1 and list2:
            if list1.val < list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next
            current = current.next
        
        # Attach the remaining nodes
        if list1:
            current.next = list1
        if list2:
            current.next = list2
        
        # Return the next of dummy node which points to the head of the merged list
        return dummy.next
```

### Explanation

1. **Dummy Node**:
   - `dummy` is used to simplify the merging process. `current` is a pointer used to build the new merged list.

2. **Merging Process**:
   - Compare the current nodes of `list1` and `list2`.
   - Attach the smaller node to `current.next` and move the pointer of the list from which the node was taken.
   - Move `current` to `current.next` after each attachment.

3. **Remaining Nodes**:
   - After one of the lists is exhausted, append the remaining nodes of the other list directly to the merged list.

4. **Return**:
   - Return `dummy.next`, which points to the head of the newly merged list.

## Complexity

- **Time Complexity**: \(O(N + M)\), where \(N\) and \(M\) are the lengths of `list1` and `list2` respectively. This is because each node from both lists is processed exactly once.
- **Space Complexity**: \(O(1)\), excluding the space used for the output list. The space complexity is constant as no extra space is used beyond a few pointers.

This method ensures an efficient merge operation while maintaining the sorted order of the resultant list.
