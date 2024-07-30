# [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

To solve the problem of creating a deep copy of a linked list with random pointers, you can follow a three-step approach:

1. **Clone Nodes and Insert Them**: Create a copy of each node and insert it right after the original node in the list. This ensures that each new node is next to its original counterpart, allowing us to easily set up the random pointers later.

2. **Set Random Pointers**: Iterate through the modified list to set the random pointers of the new nodes. Since the new nodes are placed right next to the original nodes, you can directly use the next pointers to find the corresponding new nodes.

3. **Separate the Lists**: Extract the copied nodes to form the new list and restore the original list to its initial state.

### Detailed Steps

1. **Clone Nodes and Insert Them**:
   - Traverse the original list.
   - For each node, create a new node with the same value.
   - Insert this new node right after the original node.

2. **Set Random Pointers**:
   - Traverse the modified list again.
   - For each original node, set the `random` pointer of the new node to point to the new node corresponding to the random pointer of the original node.

3. **Separate the Lists**:
   - Restore the original list and separate out the cloned nodes to form the new list.

## Code

```python
class Node:
    def __init__(self, x, next=None, random=None):
        self.val = int(x)
        self.next = next
        self.random = random

class Solution:
    def copyRandomList(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        if not head:
            return None
        
        # Step 1: Clone nodes and insert them right after original nodes
        current = head
        while current:
            # Create a new node with the value of the current node
            new_node = Node(current.val)
            # Insert the new node right after the current node
            new_node.next = current.next
            current.next = new_node
            current = new_node.next
        
        # Step 2: Set the random pointers for the new nodes
        current = head
        while current:
            new_node = current.next
            if current.random:
                new_node.random = current.random.next
            current = new_node.next
        
        # Step 3: Separate the original and copied lists
        original = head
        copy = head.next
        new_head = copy
        while original:
            original.next = original.next.next
            if copy.next:
                copy.next = copy.next.next
            original = original.next
            copy = copy.next
        
        return new_head
```

### Explanation

1. **Clone Nodes and Insert**:
   - We iterate through the original list. For each node, we create a new node and place it immediately after the original node.

2. **Set Random Pointers**:
   - In the second pass, we set the `random` pointer of each new node. Since each new node is immediately after its original counterpart, the new node corresponding to a node's `random` pointer can be found using `current.random.next`.

3. **Separate Lists**:
   - In the final pass, we restore the original list and extract the new list. We maintain two pointers, one for the original list and one for the new list.

This approach ensures that both the original and the copied linked lists are correctly managed, with time complexity \(O(n)\) and space complexity \(O(1)\) since we only use extra space for the new nodes.
