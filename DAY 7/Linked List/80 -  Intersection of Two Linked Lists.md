# [160.  Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)

To solve the problem of finding the intersection node of two singly linked lists, we can use a two-pointer approach that is both time-efficient and space-efficient. Here’s how you can achieve this:

## Approach

1. **Two-Pointer Technique**:
   - Initialize two pointers, `pA` and `pB`, at the heads of the two linked lists.
   - Traverse both lists simultaneously. When one pointer reaches the end of its list, redirect it to the head of the other list.
   - Continue this process until both pointers meet. If there is an intersection, they will eventually meet at the intersection node. If there is no intersection, both pointers will eventually be `None`.

### Steps

1. **Initialize Pointers**:
   - Start with two pointers at the heads of `headA` and `headB`.

2. **Traverse Both Lists**:
   - Move each pointer one step at a time.
   - When a pointer reaches the end of its list, redirect it to the head of the other list.

3. **Check for Intersection**:
   - If the pointers meet at the same node, that node is the intersection node.
   - If the lists do not intersect, both pointers will eventually become `None`.

## Implementation

```python
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type headA: ListNode
        :type headB: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None
        
        pA = headA
        pB = headB
        
        # Traverse both lists
        while pA != pB:
            # Move to the next node or switch to the other list
            pA = pA.next if pA else headB
            pB = pB.next if pB else headA
        
        # Both pointers are either at the intersection node or at the end (None)
        return pA
```

### Explanation

1. **Pointer Initialization**:
   - `pA` starts at `headA` and `pB` starts at `headB`.

2. **Traversal Logic**:
   - Move each pointer one step at a time.
   - When `pA` reaches the end of `headA`, redirect it to `headB`.
   - When `pB` reaches the end of `headB`, redirect it to `headA`.
   - Continue this until both pointers either meet at the intersection node or both become `None`.

3. **Return Result**:
   - If the pointers meet, return that node as the intersection.
   - If no intersection exists, return `None`.


## Complexity

- **Time Complexity**: \(O(m + n)\), where \(m\) and \(n\) are the lengths of the two lists. Each pointer traverses each list at most twice.
- **Space Complexity**: \(O(1)\), as we only use a fixed number of pointers.

This approach ensures that you efficiently find the intersection with minimal extra space usage and linear time complexity.
