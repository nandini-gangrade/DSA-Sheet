# [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)


You are given an array of `k` linked lists, each sorted in ascending order. Merge all the linked lists into one sorted linked list and return it.

### Example

**Example 1:**

**Input:**
```plaintext
lists = [[1,4,5],[1,3,4],[2,6]]
```

**Output:**
```plaintext
[1,1,2,3,4,4,5,6]
```

**Explanation:**
The linked lists are:
```
1->4->5
1->3->4
2->6
```
After merging them into one sorted list:
```
1->1->2->3->4->4->5->6
```

**Example 2:**

**Input:**
```plaintext
lists = []
```

**Output:**
```plaintext
[]
```

**Example 3:**

**Input:**
```plaintext
lists = [[]]
```

**Output:**
```plaintext
[]
```

### Constraints

- \( k == \text{lists.length} \)
- \( 0 \leq k \leq 10^4 \)
- \( 0 \leq \text{lists[i].length} \leq 500 \)
- \( -10^4 \leq \text{lists[i][j]} \leq 10^4 \)
- `lists[i]` is sorted in ascending order.
- The sum of `lists[i].length` will not exceed \( 10^4 \).

### Solution

To efficiently merge `k` sorted linked lists, you can use a min-heap (priority queue) approach which operates in \( O(n \log k) \) time complexity where \( n \) is the total number of nodes.

## Code

```python
import heapq

# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        # Define a comparator function for the heap to handle ListNode
        class ListNodeComparator:
            def __init__(self, node):
                self.node = node
            def __lt__(self, other):
                return self.node.val < other.node.val
        
        min_heap = []
        # Push the initial nodes of all lists into the heap
        for l in lists:
            if l:
                heapq.heappush(min_heap, ListNodeComparator(l))
        
        dummy = ListNode()
        current = dummy
        
        while min_heap:
            # Pop the smallest node from the heap
            smallest_node = heapq.heappop(min_heap).node
            current.next = smallest_node
            current = current.next
            
            # If there's a next node, push it to the heap
            if smallest_node.next:
                heapq.heappush(min_heap, ListNodeComparator(smallest_node.next))
        
        return dummy.next
```

### Explanation

1. **Min-Heap Initialization**:
   - A min-heap (priority queue) is used to efficiently retrieve the smallest element from the heads of the linked lists.

2. **Heap Operations**:
   - We push the head nodes of all linked lists into the heap. The custom `ListNodeComparator` class ensures that nodes are compared based on their values.
   - Extract the smallest node from the heap, append it to the result list, and push the next node from the same list into the heap if available.

3. **Time Complexity**:
   - The time complexity is \( O(n \log k) \), where \( n \) is the total number of nodes in all lists, and \( k \) is the number of linked lists. This is because each node is pushed and popped from the heap at most once, and the heap operations take \( \log k \) time.

This approach ensures that the merging of `k` sorted linked lists is done efficiently.
