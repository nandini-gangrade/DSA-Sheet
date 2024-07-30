# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)

To solve the problem of adding two numbers represented by linked lists where the digits are stored in reverse order, you can follow these steps:

### Steps

1. **Initialize Pointers and Variables**:
   - Use a dummy head node for the result list.
   - Use pointers to traverse the two input lists.
   - Maintain a carry variable to handle sums greater than 9.

2. **Traverse the Lists**:
   - Iterate through both lists simultaneously.
   - For each pair of nodes, compute the sum of the values and the carry from the previous digit.
   - Update the carry for the next digit.

3. **Handle Remaining Carry**:
   - If there's any carry left after processing both lists, append it as a new node.

4. **Return the Result**:
   - Return the list starting from the node next to the dummy head.

### Example

For the input lists:
- `l1 = [2,4,3]` (represents 342)
- `l2 = [5,6,4]` (represents 465)

The sum should be `807`, which corresponds to the linked list `[7,0,8]`.

## Code Implementation

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy_head = ListNode(0)  # Dummy node to simplify edge cases
        current = dummy_head       # Pointer to the current node in the result list
        carry = 0                 # Initialize carry to 0

        # Traverse both linked lists
        while l1 or l2 or carry:
            # Get the value from each list node, or 0 if the node is None
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0

            # Compute the sum of the two values and the carry
            total = val1 + val2 + carry
            carry = total // 10   # Update carry
            sum_digit = total % 10  # Get the digit to store in the current node

            # Create a new node with the computed digit
            current.next = ListNode(sum_digit)
            current = current.next  # Move to the next node

            # Move to the next nodes in the input lists, if available
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next

        # Return the next node after the dummy head, which is the start of the result list
        return dummy_head.next
```

### Explanation

1. **Dummy Head Node**: Simplifies edge cases (e.g., when the input lists are empty or when there's a final carry).
2. **Current Node**: Points to the node being processed in the result list.
3. **Carry Handling**: The carry is updated with each digit sum to ensure proper handling of values greater than 9.
4. **While Loop**: Continues as long as there are nodes left in either list or there is a carry.

This approach ensures that all nodes are processed, handles cases with differing lengths of lists, and correctly manages the carry over for sums that exceed 9. The time complexity is \(O(n + m)\), where \(n\) and \(m\) are the lengths of the two input lists. The space complexity is \(O(max(n, m))\) for the new linked list.
