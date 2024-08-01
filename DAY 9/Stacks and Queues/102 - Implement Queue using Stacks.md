# [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/description/)

To implement a queue using two stacks, we need to manage how we handle push and pop operations to maintain the FIFO order. We will use two stacks:
1. `stack_in` for push operations.
2. `stack_out` for pop and peek operations.

Here's the step-by-step explanation of how this will work:
1. **Push Operation:** Simply push the element onto `stack_in`.
2. **Pop Operation:** If `stack_out` is empty, transfer all elements from `stack_in` to `stack_out` and then pop from `stack_out`. If `stack_out` is not empty, directly pop from `stack_out`.
3. **Peek Operation:** If `stack_out` is empty, transfer all elements from `stack_in` to `stack_out` and then return the top element of `stack_out`. If `stack_out` is not empty, directly return the top element of `stack_out`.
4. **Empty Operation:** The queue is empty if both `stack_in` and `stack_out` are empty.

Here is the implementation in Python:

```python
class MyQueue(object):

    def __init__(self):
        self.stack_in = []
        self.stack_out = []

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.stack_in.append(x)

    def pop(self):
        """
        :rtype: int
        """
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
        return self.stack_out.pop()

    def peek(self):
        """
        :rtype: int
        """
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
        return self.stack_out[-1]

    def empty(self):
        """
        :rtype: bool
        """
        return not self.stack_in and not self.stack_out

# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

### Explanation
1. **Constructor (`__init__`):** Initializes the two stacks, `stack_in` and `stack_out`.
2. **Push Method (`push`):** Adds the element to `stack_in`.
3. **Pop Method (`pop`):** Ensures that if `stack_out` is empty, it transfers all elements from `stack_in` to `stack_out` before popping the top element of `stack_out`.
4. **Peek Method (`peek`):** Ensures that if `stack_out` is empty, it transfers all elements from `stack_in` to `stack_out` before returning the top element of `stack_out`.
5. **Empty Method (`empty`):** Checks if both stacks are empty to determine if the queue is empty.

## Complexity
- **Time Complexity:** Each element is moved between the stacks at most once, giving an amortized O(1) time complexity for each operation.
- **Space Complexity:** O(n), where n is the number of elements in the queue, as both stacks together will hold all elements.

This implementation efficiently uses two stacks to mimic the behavior of a queue while ensuring that each operation is performed in constant amortized time.
