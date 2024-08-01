# [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/description/)

To implement a last-in-first-out (LIFO) stack using only two queues, we need to simulate stack operations by utilizing the queue operations. The key idea is to use two queues to manage the order of elements in such a way that the last element pushed into the stack is always accessible for popping.

## Approach

1. **Two Queues**: We use two queues, `queue1` and `queue2`. One queue will be used for primary storage, and the other will help in rearranging the elements.

2. **Push Operation**: When we push an element, we enqueue it into `queue2`. Then, we dequeue all elements from `queue1` and enqueue them into `queue2`. Finally, we swap the names of `queue1` and `queue2`, so that `queue1` always contains the stack elements in the correct order.

3. **Pop Operation**: To pop an element, we simply dequeue from `queue1`, as it contains the elements in the correct stack order.

4. **Top Operation**: The top operation will just return the front element of `queue1`.

5. **Empty Operation**: This operation checks if `queue1` is empty.

## Implementation

Here's how you can implement the `MyStack` class in Python:

```python
from collections import deque

class MyStack:

    def __init__(self):
        """
        Initialize two queues.
        """
        self.queue1 = deque()
        self.queue2 = deque()

    def push(self, x):
        """
        Push element x onto stack.
        """
        self.queue2.append(x)
        # Move all elements from queue1 to queue2
        while self.queue1:
            self.queue2.append(self.queue1.popleft())
        # Swap the queues
        self.queue1, self.queue2 = self.queue2, self.queue1

    def pop(self):
        """
        Removes the element on top of the stack and returns that element.
        """
        return self.queue1.popleft()

    def top(self):
        """
        Get the top element.
        """
        return self.queue1[0]

    def empty(self):
        """
        Returns whether the stack is empty.
        """
        return not self.queue1

# Example Usage:
# obj = MyStack()
# obj.push(1)
# obj.push(2)
# print(obj.top())    # Output: 2
# print(obj.pop())    # Output: 2
# print(obj.empty())  # Output: False
```

### Explanation

- **Push Operation**: The element is added to `queue2`, and all elements of `queue1` are transferred to `queue2`. This ensures that the most recently added element is always at the front of `queue1` after the swap.

- **Pop and Top Operations**: These operations directly interact with `queue1`, which is always maintained to have the order of elements like a stack.

- **Empty Operation**: It checks if `queue1` is empty, which determines if the stack is empty.

## Complexity

- **Time Complexity**:
  - `push`: O(n), where n is the number of elements in the stack, since we move all elements between the queues.
  - `pop`: O(1), as we simply pop the front of `queue1`.
  - `top`: O(1), as we directly access the front of `queue1`.
  - `empty`: O(1), since we check if `queue1` is empty.

- **Space Complexity**: O(n), where n is the number of elements in the stack, because we store all elements in two queues.

This approach ensures that the stack operations adhere to the LIFO principle using only queue operations.
