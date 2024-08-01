# [Implement two stacks in an array](https://www.geeksforgeeks.org/problems/implement-two-stacks-in-an-array/1)

Implement two stacks using a single array with the following operations:

1. **push1(x)**: Push `x` into the first stack.
2. **push2(x)**: Push `x` into the second stack.
3. **pop1()**: Pop and return the top element from the first stack. Return `-1` if the first stack is empty.
4. **pop2()**: Pop and return the top element from the second stack. Return `-1` if the second stack is empty.

## Approach

1. **Initialization**: 
   - Use a single array of a fixed size to hold both stacks.
   - Initialize two pointers: `top1` starting at the beginning of the array (`-1` initially, indicating the stack is empty) and `top2` starting at the end of the array (size of the array initially).

2. **Push Operations**:
   - For `push1(x)`: Check if there is space between `top1` and `top2`. If there is, increment `top1` and insert `x` at `top1`.
   - For `push2(x)`: Check if there is space between `top1` and `top2`. If there is, decrement `top2` and insert `x` at `top2`.

3. **Pop Operations**:
   - For `pop1()`: If `top1` is `-1`, return `-1` (indicating the stack is empty). Otherwise, return the element at `top1` and decrement `top1`.
   - For `pop2()`: If `top2` is equal to the size of the array, return `-1` (indicating the stack is empty). Otherwise, return the element at `top2` and increment `top2`.

## Code Implementation

Here is the implementation of the described approach:

```python
class TwoStacks:
    def __init__(self, size=100):
        # Initialize the array with the given size
        self.size = size
        self.array = [None] * size
        self.top1 = -1  # Initialize top for stack 1
        self.top2 = size  # Initialize top for stack 2

    # Function to push an integer into stack 1
    def push1(self, x):
        if self.top1 < self.top2 - 1:  # Check for available space
            self.top1 += 1
            self.array[self.top1] = x
        else:
            print("Stack Overflow")

    # Function to push an integer into stack 2
    def push2(self, x):
        if self.top1 < self.top2 - 1:  # Check for available space
            self.top2 -= 1
            self.array[self.top2] = x
        else:
            print("Stack Overflow")

    # Function to remove an element from the top of stack 1
    def pop1(self):
        if self.top1 >= 0:
            x = self.array[self.top1]
            self.top1 -= 1
            return x
        else:
            return -1

    # Function to remove an element from the top of stack 2
    def pop2(self):
        if self.top2 < self.size:
            x = self.array[self.top2]
            self.top2 += 1
            return x
        else:
            return -1
```

## Complexity Analysis

- **Time Complexity**: 
  - All operations (`push1`, `push2`, `pop1`, `pop2`) are performed in \(O(1)\) time as they involve only index updates and simple assignments.

- **Space Complexity**: 
  - The space complexity is \(O(n)\) due to the use of the array to store elements, where \(n\) is the total size allocated for both stacks.

This solution efficiently uses a single array to implement two stacks while maintaining \(O(1)\) time complexity for all operations, ensuring that both stacks can grow dynamically as long as space permits.
