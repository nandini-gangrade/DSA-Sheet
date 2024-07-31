# [Subtraction in Linked List](https://www.geeksforgeeks.org/problems/subtraction-in-linked-list/1)

Given two linked lists that represent two large positive numbers, subtract the smaller number from the larger one and return the result as a linked list. The linked lists represent numbers with each node containing a single digit, and the digits are stored in the order from most significant to least significant.

**Example:**
- **Input:** `L1 = 1 -> 0 -> 0`, `L2 = 1 -> 2`
- **Output:** `8 -> 8` (because 100 - 12 = 88)

## Intuition

The problem is to perform arithmetic subtraction on large numbers represented as linked lists. To achieve this:
1. Convert the linked lists into their integer representations.
2. Perform the subtraction operation on these integer values.
3. Convert the result back into a linked list format.

## Approach

1. **Convert Linked Lists to Integers:**
   - Traverse each linked list and collect the digits in a list.
   - Convert this list of digits into a string and then to an integer.

2. **Perform Subtraction:**
   - Subtract the smaller number from the larger number.

3. **Convert the Result to a Linked List:**
   - Convert the result of the subtraction back into a string.
   - Create a new linked list from this string representation.

## Code

```python
class LinkedList:
    def __init__(self):
        self.head = None
    
    def insert(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

class Node:
    def __init__(self, data=0, next=None):
        self.data = data
        self.next = next

class Solution:
    def subLinkedList(self, l1, l2): 
        arr = []
        while l1:
            arr.append(l1.data)
            l1 = l1.next
        arr2 = []
        while l2:
            arr2.append(l2.data)
            l2 = l2.next
        
        # Convert lists to integers
        str1 = "".join(str(x) for x in arr)
        str2 = "".join(str(x) for x in arr2)
        k = int(str1)
        j = int(str2)
        
        # Subtract the smaller number from the larger one
        if k > j:
            ans = k - j
        else:
            ans = j - k
        
        # Convert the result to a string and then to a linked list
        t = str(ans)
        new_list = LinkedList()
        for i in range(len(t)):
            new_list.insert(int(t[i]))
        
        return new_list.head
```

## Complexity

- **Time Complexity:**
  - **Conversion of Linked Lists to Integers:** O(n + m) where `n` and `m` are the lengths of the two linked lists. This is because we need to traverse both lists to collect the digits.
  - **Subtraction:** O(1) since it’s a direct arithmetic operation on integers.
  - **Conversion of Result to Linked List:** O(p) where `p` is the number of digits in the result. 

  Overall time complexity is O(n + m + p), where `p` is typically proportional to `n` and `m`.

- **Space Complexity:**
  - **Storage for Digits:** O(n + m) for storing the digits from both linked lists.
  - **Result Linked List:** O(p) for storing the digits of the result.

  Overall space complexity is O(n + m + p).

### Summary

The approach involves:
1. Traversing the linked lists to gather digits.
2. Converting these digits into integers for arithmetic operations.
3. Constructing a new linked list from the result.

This method is straightforward and efficient, making use of Python’s ability to handle large integers natively.
