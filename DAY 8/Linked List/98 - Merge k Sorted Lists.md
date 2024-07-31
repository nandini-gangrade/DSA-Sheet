# [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)


You are given an array of `k` linked lists, each sorted in ascending order. Merge all the linked lists into one sorted linked list and return it.

### Example

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

### Constraints

- \( k == \text{lists.length} \)
- \( 0 \leq k \leq 10^4 \)
- \( 0 \leq \text{lists[i].length} \leq 500 \)
- \( -10^4 \leq \text{lists[i][j]} \leq 10^4 \)
- `lists[i]` is sorted in ascending order.
- The sum of `lists[i].length` will not exceed \( 10^4 \).

### Solution

The efficient approach uses a min-heap (priority queue) to merge `k` sorted linked lists in \( O(n \log k) \) time, where \( n \) is the total number of nodes.

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
   - We use `heapq` to create a min-heap. A custom class `ListNodeComparator` is used to handle comparisons based on node values.

2. **Heap Operations**:
   - Push the head nodes of all linked lists into the heap.
   - Continuously pop the smallest node from the heap, append it to the result list, and push the next node from the same list (if available) into the heap.

3. **Time Complexity**:
   - The time complexity is \( O(n \log k) \), where \( n \) is the total number of nodes and \( k \) is the number of linked lists.

This approach is optimal for merging multiple sorted linked lists efficiently.
