# [341. Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/)

- **Input:** A nested list where each element is either an integer or another list.
- **Output:** A flattened sequence of integers.

### Approach

1. **Recursive Flattening:** 
   - Use a stack to keep track of the current position within the nested lists.
   - When an integer is encountered, it is added directly to the sequence.
   - When a list is encountered, its elements are pushed onto the stack in reverse order (to ensure the correct order when popping).
   - Recursively process nested lists until all integers are obtained.

2. **Iterator Design:**
   - Implement the `next` method to return the next integer in the sequence.
   - Implement the `hasNext` method to check if there are more integers to process.

### Implementation Steps

1. **Initialization:**
   - Initialize the stack with the entire nested list.
   - The stack helps keep track of the nested structure as we flatten it.

2. **Flattening Process:**
   - Use a helper method to recursively flatten the list and store integers in a queue.
   - Use a stack to manage the order of processing: push lists onto the stack, and pop to process.

3. **Iterator Methods:**
   - `next`: Return the next integer from the queue.
   - `hasNext`: Check if the queue is not empty.

### Code

Here's the implementation in Python:

```python
class NestedInteger:
    def __init__(self, value=None):
        self.value = value
        self.list = []

    def isInteger(self):
        return self.value is not None

    def getInteger(self):
        return self.value

    def getList(self):
        return self.list


class NestedIterator:
    def __init__(self, nestedList):
        # Initialize the stack with the reversed nested list
        self.stack = []
        for item in reversed(nestedList):
            self.stack.append(item)

    def next(self):
        # Pop from the stack since we ensured there is a next integer
        return self.stack.pop().getInteger()

    def hasNext(self):
        # Ensure the stack is processed until an integer is found
        while self.stack:
            top = self.stack[-1]
            if top.isInteger():
                return True
            # Otherwise, process the list
            self.stack.pop()  # Pop the list
            for item in reversed(top.getList()):
                self.stack.append(item)
        return False
```

### Explanation

- **Initialization:** The constructor takes a `nestedList` and initializes a stack by pushing all elements in reverse order.
- **`next()` Method:** Simply pops the top element from the stack and returns its integer value.
- **`hasNext()` Method:** Checks if the stack has any integers. If the top of the stack is a list, it unpacks the list by pushing its elements onto the stack in reverse order.

### Complexity Analysis

- **Time Complexity:** Each integer is processed once, so the overall time complexity is \(O(N)\), where \(N\) is the total number of integers across all levels of nesting.
- **Space Complexity:** The space complexity is \(O(N)\) for the stack used to store elements temporarily during flattening.

This approach efficiently handles the nested list structure using a stack and ensures that integers are accessed in the correct order.
