# [445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/description/)

To solve the problem of adding two numbers represented by linked lists where the most significant digit comes first, we can follow an approach that avoids reversing the linked lists. Instead, we use stacks to handle the digits in reverse order for addition. 

### Steps to Solve the Problem

1. **Use Stacks**: Use two stacks to store the digits of the linked lists. This allows us to process the digits in reverse order, making addition straightforward.

2. **Pop and Add**: Pop digits from the stacks to add them. Maintain a carry to handle cases where the sum of digits exceeds 9.

3. **Build the Result**: Use a dummy head to build the resulting linked list from the sum of digits. Insert the new nodes at the front of the result list to maintain the most significant digit order.

### Detailed Explanation

1. **Push Digits onto Stacks**:
   - Traverse each linked list and push each node's value onto a stack. This ensures that the most significant digit is at the bottom of the stack.

2. **Add Digits**:
   - Pop digits from the stacks, add them along with any carry from the previous step. Create new nodes for each digit in the result linked list.

3. **Build the Result**:
   - Since we are inserting nodes at the front, the result linked list will have the most significant digit at the head.

## Code

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
        # Helper function to push all nodes' values from a linked list to a stack
        def pushToStack(node):
            stack = []
            while node:
                stack.append(node.val)
                node = node.next
            return stack
        
        # Push all nodes' values to stacks
        stack1 = pushToStack(l1)
        stack2 = pushToStack(l2)
        
        carry = 0
        head = None
        
        # Process the stacks and build the resulting linked list
        while stack1 or stack2 or carry:
            sum_val = carry
            if stack1:
                sum_val += stack1.pop()
            if stack2:
                sum_val += stack2.pop()
            
            carry = sum_val // 10
            new_node = ListNode(sum_val % 10)
            new_node.next = head
            head = new_node
        
        return head
```

### Explanation of the Code

1. **pushToStack Function**:
   - This function traverses a linked list and pushes the values of its nodes onto a stack.

2. **Adding Digits**:
   - Digits are popped from the stacks to get the numbers in reverse order. The carry is handled by adding it to the sum. The new digit and carry are calculated.

3. **Building the Result**:
   - A new node is created for each digit, and it is inserted at the front of the result list. This ensures the most significant digit is at the head.

This approach efficiently handles the addition of numbers represented as linked lists without needing to reverse the input lists. The time complexity is \(O(n + m)\), where \(n\) and \(m\) are the lengths of the two linked lists, and the space complexity is also \(O(n + m)\) due to the use of stacks.
