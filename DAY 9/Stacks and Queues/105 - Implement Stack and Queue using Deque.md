# [Implement Stack and Queue using Deque](https://www.geeksforgeeks.org/implement-stack-queue-using-deque/)

To implement a stack and a queue using a deque (double-ended queue), we'll use a linked list representation of a deque. This allows us to perform insertions and deletions at both ends of the list efficiently.


### Deque Implementation

A deque can be visualized as follows:

```
Head  <--> Node1 <--> Node2 <--> Node3 <--> Tail
```

- **Head**: Points to the first element.
- **Tail**: Points to the last element.
- **Node**: Each node contains a value, a pointer to the next node, and a pointer to the previous node.

Operations on a deque involve inserting or removing nodes from the head or the tail.

### Stack Using Deque

A stack is a LIFO (last-in, first-out) data structure. Using a deque, we can push and pop elements from the end of the deque.

```
Push 7:     Head <--> 7 <--> Tail
Push 8:     Head <--> 7 <--> 8 <--> Tail
Pop:        Head <--> 7 <--> Tail
```

#### Queue Using Deque

A queue is a FIFO (first-in, first-out) data structure. Using a deque, we can enqueue elements at the end and dequeue elements from the beginning.

```
Enqueue 12: Head <--> 12 <--> Tail
Enqueue 13: Head <--> 12 <--> 13 <--> Tail
Dequeue:    Head <--> 13 <--> Tail
```

## Implementation

Below is the implementation of a deque and how it can be used to simulate both a stack and a queue:

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.prev = None
        self.next = None

class Deque:
    def __init__(self):
        self.head = self.tail = None

    def isEmpty(self):
        return self.head is None

    def insert_first(self, element):
        newP = Node(element)
        if self.isEmpty():
            self.head = self.tail = newP
        else:
            newP.next = self.head
            self.head.prev = newP
            self.head = newP

    def insert_last(self, element):
        newP = Node(element)
        if self.isEmpty():
            self.head = self.tail = newP
        else:
            newP.prev = self.tail
            self.tail.next = newP
            self.tail = newP

    def remove_first(self):
        if self.isEmpty():
            print('List is Empty')
            return
        if self.head == self.tail:  # Only one element
            self.head = self.tail = None
        else:
            self.head = self.head.next
            self.head.prev = None

    def remove_last(self):
        if self.isEmpty():
            print('List is Empty')
            return
        if self.head == self.tail:  # Only one element
            self.head = self.tail = None
        else:
            self.tail = self.tail.prev
            self.tail.next = None

    def size(self):
        curr = self.head
        length = 0
        while curr:
            length += 1
            curr = curr.next
        return length

    def display(self):
        if self.isEmpty():
            print('List is Empty')
            return
        curr = self.head
        while curr:
            print(curr.val, end=' ')
            curr = curr.next
        print()

class Stack:
    def __init__(self):
        self.stack = Deque()

    def push(self, element):
        self.stack.insert_last(element)

    def pop(self):
        self.stack.remove_last()

    def size(self):
        return self.stack.size()

    def display(self):
        self.stack.display()

class Queue:
    def __init__(self):
        self.queue = Deque()

    def enqueue(self, element):
        self.queue.insert_last(element)

    def dequeue(self):
        self.queue.remove_first()

    def size(self):
        return self.queue.size()

    def display(self):
        self.queue.display()
```

### Explanation

- **Deque Class**: This class manages the linked list representation, allowing insertions and deletions at both ends.

- **Stack Class**: Implements a stack using the deque by inserting and removing elements from the tail.

- **Queue Class**: Implements a queue using the deque by inserting elements at the tail and removing them from the head.

## Complexity

- **Time Complexity**: 
  - All operations (`push`, `pop`, `enqueue`, `dequeue`) are O(1) because they involve a constant number of pointer updates.
  
- **Space Complexity**: 
  - O(n), where n is the number of elements in the deque, as each element requires a node.

This implementation provides efficient stack and queue operations by leveraging the flexibility of the deque structure.
