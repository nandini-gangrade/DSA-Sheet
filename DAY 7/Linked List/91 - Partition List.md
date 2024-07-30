# [86. Partition List](https://leetcode.com/problems/partition-list/description/)

To partition a linked list around a value \( x \), we can use the two-pointer technique with dummy nodes, similar to the previous solution. This ensures that all nodes with values less than \( x \) appear before nodes with values greater than or equal to \( x \), while maintaining the original relative order of nodes in each partition.

Here's how you can implement this:

### Steps

1. **Initialize Dummy Nodes**:
   - Create two dummy nodes, `less_head` and `greater_head`, to start two separate linked lists.
   - `less` will point to the end of the list containing nodes less than \( x \).
   - `greater` will point to the end of the list containing nodes greater than or equal to \( x \).

2. **Iterate Through the Original List**:
   - For each node in the original list:
     - If the node's value is less than \( x \), append it to the `less` list.
     - Otherwise, append it to the `greater` list.

3. **Connect the Two Lists**:
   - Connect the last node of the `less` list to the head of the `greater` list.
   - Ensure the end of the `greater` list points to `None`.

4. **Return the Combined List**:
   - The head of the modified list will be the node after `less_head`.

## Python Code

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        # Dummy nodes to start the less and greater lists
        less_head = ListNode(0)
        greater_head = ListNode(0)
        
        # Pointers to the current end of the less and greater lists
        less = less_head
        greater = greater_head
        
        # Iterate through the original list
        current = head
        while current:
            if current.val < x:
                # Append to the less list
                less.next = current
                less = less.next
            else:
                # Append to the greater list
                greater.next = current
                greater = greater.next
            current = current.next
        
        # Connect the two lists
        greater.next = None  # Ensure the last node points to None
        less.next = greater_head.next  # Connect the end of less to the start of greater
        
        # Return the head of the new partitioned list
        return less_head.next
```

### Explanation

- **Dummy Nodes**: Using `less_head` and `greater_head` allows us to easily manage the start and end of the two lists.
- **Pointers**: `less` and `greater` maintain the current end of the respective lists.
- **Iteration**: As we iterate, we decide where each node should go based on its value compared to \( x \).
- **Linking**: After constructing the two lists, we connect them to form the final list.
- **Return Value**: The combined list starts at `less_head.next`.

## Complexity

- **Time Complexity**: \(O(n)\), where \( n \) is the number of nodes in the linked list, as we process each node once.
- **Space Complexity**: \(O(1)\), since we only use a constant amount of additional space for pointers and dummy nodes.
