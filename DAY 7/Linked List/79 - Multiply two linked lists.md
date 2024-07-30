# [Multiply two linked lists](https://www.geeksforgeeks.org/problems/multiply-two-linked-lists/1)

To solve the problem of multiplying two linked lists representing numbers, we'll follow these steps:

1. **Extract Numbers from Linked Lists**:
   - Convert each linked list to its numerical value by traversing through the list and constructing the number.

2. **Multiply the Two Numbers**:
   - Multiply the two numbers obtained from the linked lists.

3. **Handle Large Numbers**:
   - Use modulo \(10^9 + 7\) to ensure the result fits within standard integer limits.

## Approach

1. **Convert Linked List to Number**:
   - Traverse the linked list from head to tail.
   - Construct the number by multiplying the current result by 10 and adding the node value at each step.

2. **Multiply and Apply Modulo**:
   - Multiply the two numbers and take modulo \(10^9 + 7\).

## Code

```python
class Node:
    def __init__(self, data=0, next=None):
        self.data = data
        self.next = next

class Solution:
    def multiply_two_lists(self, head1, head2):
        MOD = 10**9 + 7
        
        # Helper function to convert linked list to integer
        def linked_list_to_number(head):
            number = 0
            while head:
                number = (number * 10 + head.data) % MOD
                head = head.next
            return number
        
        # Convert both linked lists to numbers
        num1 = linked_list_to_number(head1)
        num2 = linked_list_to_number(head2)
        
        # Multiply the numbers and take modulo
        result = (num1 * num2) % MOD
        
        return result
```

### Explanation

1. **Linked List to Number Conversion**:
   - The `linked_list_to_number` function iterates through the linked list.
   - It constructs the number by maintaining the current value and multiplying it by 10 before adding the current node’s data.
   - To handle large numbers and avoid overflow, the result is taken modulo \(10^9 + 7\) at each step.

2. **Multiplication and Modulo**:
   - After converting both linked lists to their respective numbers, multiply these numbers.
   - Apply modulo \(10^9 + 7\) to the final result to handle large numbers.

## Complexity Analysis

- **Time Complexity**: \(O(n + m)\), where \(n\) is the number of nodes in the first list and \(m\) is the number of nodes in the second list. This is because each node in both lists is processed exactly once.
- **Space Complexity**: \(O(1)\) auxiliary space, as we are only using a constant amount of extra space regardless of the input size.

This approach is efficient and handles the problem constraints effectively.
