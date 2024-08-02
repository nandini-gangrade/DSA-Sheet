# [146. LRU Cache](https://leetcode.com/problems/lru-cache/description/)

To implement an LRU Cache that meets the given constraints, we need a data structure that allows us to efficiently update and access elements, while also maintaining the order of usage so that we can easily identify and remove the least recently used items when the cache reaches capacity.

The ideal solution involves using a combination of a hash map (for O(1) access and updates) and a doubly linked list (to maintain the order of usage).

### Approach

1. **Doubly Linked List:** 
   - We'll use a doubly linked list to store the cache items in order of usage, with the least recently used items at the head and the most recently used at the tail. 
   - This allows us to quickly remove the least recently used item when needed and move items to the tail when they are accessed or updated.

2. **Hash Map:**
   - A hash map will store references to the nodes in the doubly linked list for fast access and updates.

### Operations

- **Get:** 
  - Check if the key exists in the hash map. 
  - If it does, move the corresponding node to the tail of the list to mark it as recently used and return its value.
  - If it doesn't exist, return -1.

- **Put:**
  - If the key exists, update its value and move it to the tail.
  - If the key does not exist:
    - Add it to the list at the tail.
    - Add the key and reference to the hash map.
    - If the cache exceeds its capacity, remove the head node and its reference from the hash map.

## Code

```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}  # key -> Node
        self.head = Node(0, 0)  # Dummy head
        self.tail = Node(0, 0)  # Dummy tail
        self.head.next = self.tail
        self.tail.prev = self.head

    def _remove(self, node: Node):
        """Remove an existing node from the linked list."""
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node

    def _add(self, node: Node):
        """Add a new node right before the tail."""
        prev_tail = self.tail.prev
        prev_tail.next = node
        node.prev = prev_tail
        node.next = self.tail
        self.tail.prev = node

    def get(self, key: int) -> int:
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add(node)  # Move to tail (recently used)
            return node.value
        return -1

    def put(self, key: int, value: int):
        if key in self.cache:
            # Remove old
            self._remove(self.cache[key])
        elif len(self.cache) == self.capacity:
            # Remove LRU from cache and linked list
            lru = self.head.next
            self._remove(lru)
            del self.cache[lru.key]

        # Add new node
        new_node = Node(key, value)
        self._add(new_node)
        self.cache[key] = new_node
```

### Explanation

- **Node Class:** A helper class for doubly linked list nodes that store key-value pairs.
- **LRUCache Class:** 
  - **Initialization:** Initializes the cache with dummy head and tail nodes to simplify edge case handling.
  - **_remove and _add methods:** Handle node removal and insertion.
  - **Get and Put Methods:** Perform operations as described, maintaining the list and cache in sync.

### Complexity

- **Time Complexity:** Both `get` and `put` operations are \(O(1)\) on average due to the efficient use of the hash map and linked list.
- **Space Complexity:** \(O(N)\) where \(N\) is the capacity of the cache, accounting for the hash map and doubly linked list nodes.
