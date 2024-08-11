# [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

To solve the problem of finding the `k`th largest element in an array without sorting the entire array, we can utilize a **min-heap** (a binary heap data structure). The min-heap approach is efficient and allows us to maintain the `k` largest elements seen so far.

### Approach:

1. **Min-Heap Construction**:
   - We maintain a min-heap of size `k`. This heap will store the `k` largest elements encountered so far.
   - The smallest element in this heap (the root) will represent the `k`th largest element in the array as we process it.

2. **Heap Operations**:
   - As we iterate through the array, we add each element to the heap.
   - If the heap size exceeds `k`, we remove the smallest element (the root of the heap) to ensure the heap always contains only the `k` largest elements.

3. **Final Result**:
   - After processing all elements, the root of the min-heap will be the `k`th largest element in the array.

### Python Implementation:

```python
import heapq

class Solution:
    def findKthLargest(self, nums, k):
        # Step 1: Create a min-heap with the first k elements
        heap = nums[:k]
        heapq.heapify(heap)  # Convert the list to a min-heap
        
        # Step 2: Process the remaining elements
        for num in nums[k:]:
            if num > heap[0]:  # Only add to heap if num is greater than the smallest element in the heap
                heapq.heappushpop(heap, num)
        
        # Step 3: The root of the heap is the kth largest element
        return heap[0]

# Example Usage:
sol = Solution()
print(sol.findKthLargest([3,2,1,5,6,4], 2))  # Output: 5
print(sol.findKthLargest([3,2,3,1,2,4,5,5,6], 4))  # Output: 4
```

### Explanation:

1. **Heap Construction**:
   - `heapq.heapify(heap)` converts the first `k` elements into a min-heap.
   - The heap property ensures that the smallest of these `k` elements is at the root of the heap.

2. **Processing the Array**:
   - For each element beyond the first `k`, we compare it with the root of the heap.
   - If the element is larger than the root, it means that this element should be included in the `k` largest elements, so we replace the root with this new element using `heapq.heappushpop(heap, num)`.

3. **Result**:
   - The smallest element in the heap after processing all elements is the `k`th largest element in the array.

### Time Complexity:

- **Building the Heap**: \(O(k)\) to build the initial heap.
- **Processing Remaining Elements**: \(O((n-k) \log k)\), where \(n\) is the total number of elements in the array. Each insertion/removal in the heap is \(O(\log k)\).
- **Overall Complexity**: \(O(n \log k)\).

This approach is more efficient than sorting the entire array (which would take \(O(n \log n)\)) and is well-suited for large inputs.
