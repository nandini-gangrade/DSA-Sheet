# [Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/description/)

Given the head of a singly-linked list where each node's value is either 0 or 1, the linked list represents a binary number. The most significant bit (MSB) is at the head of the list. Your task is to convert this binary number to its decimal representation and return it.

### Explanation of Examples

- **Example 1**:
  - **Input**: `[1, 0, 1]`
  - **Output**: `5`
  - **Explanation**: The binary number `101` corresponds to the decimal number `5`.

- **Example 2**:
  - **Input**: `[0]`
  - **Output**: `0`
  - **Explanation**: The binary number `0` corresponds to the decimal number `0`.

## Intuition

To solve this problem, you can traverse the linked list and build the decimal number by shifting and adding values. Since the list represents a binary number where the head is the most significant bit, you need to accumulate the decimal value by processing each bit and adjusting the result accordingly.

## Approach

1. **Initialize a Result Variable**:
   - Start with `result = 0`.

2. **Traverse the Linked List**:
   - For each node in the linked list, shift the current `result` left by one position (equivalent to multiplying by 2) and add the current node's value (0 or 1).

3. **Return the Result**:
   - Once all nodes are processed, the result will contain the decimal value of the binary number represented by the linked list.

## Code

Here's the implementation of the above approach in Python:

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def getDecimalValue(self, head):
        """
        :type head: ListNode
        :rtype: int
        """
        result = 0
        current = head
        
        while current:
            result = (result << 1) | current.val
            current = current.next
        
        return result
```

### Explanation

- **Initialization**: Start with `result` set to 0.
- **Traversal**:
  - For each node, left-shift the `result` (multiply by 2) and add the current node’s value using bitwise OR.
  - Move to the next node.
- **Return**: After processing all nodes, `result` will contain the decimal representation of the binary number.

## Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the linked list. Each node is visited exactly once.
- **Space Complexity**: \(O(1)\), as only a constant amount of extra space is used for variables.

This solution efficiently converts the binary number represented by the linked list into its decimal equivalent with linear time complexity and constant space usage.
