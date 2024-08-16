# [307. Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/description/)

To handle both **update** and **sumRange** operations efficiently on an array, a simple prefix sum approach won't be sufficient since updating an element would require recalculating the entire prefix sum, which would result in an `O(n)` complexity for each update. Instead, we can use a **Segment Tree** data structure that allows us to handle both updates and range sum queries in logarithmic time `O(log n)`.

### Segment Tree Overview

A segment tree allows:
- **Point updates** in `O(log n)` — when you update a single element in the array, the segment tree can efficiently update the affected range.
- **Range sum queries** in `O(log n)` — by summing the values from a specific range using the tree structure.

### Segment Tree Properties:
- Each node in the tree represents the sum of a segment (or range) of the array.
- The root node of the tree represents the sum of the entire array.
- Internal nodes represent the sum of subarrays, and leaf nodes represent individual elements of the array.

### Solution Approach:

1. **Build the Segment Tree**: Construct a segment tree where each node contains the sum of a range of elements.
2. **Update the Segment Tree**: When an element is updated, we propagate the change upwards through the tree to update the relevant segment sums.
3. **Query the Range Sum**: For any query, the segment tree allows summing up the range by combining the results of sub-ranges in `O(log n)` time.

### Code Implementation:

```python
class NumArray:

    def __init__(self, nums: List[int]):
        # Initialize the segment tree
        self.n = len(nums)
        self.tree = [0] * (2 * self.n)
        
        # Build the segment tree
        # Insert the leaf nodes in the second half of the tree array
        for i in range(self.n):
            self.tree[self.n + i] = nums[i]
        
        # Build the internal nodes
        for i in range(self.n - 1, 0, -1):
            self.tree[i] = self.tree[2 * i] + self.tree[2 * i + 1]

    def update(self, index: int, val: int) -> None:
        # Update the value at the leaf node
        index += self.n
        self.tree[index] = val
        
        # Propagate the change upwards
        i = index
        while i > 1:
            i //= 2
            self.tree[i] = self.tree[2 * i] + self.tree[2 * i + 1]

    def sumRange(self, left: int, right: int) -> int:
        # Get the sum in the range [left, right]
        left += self.n
        right += self.n
        total_sum = 0
        
        while left <= right:
            # If left is a right child, add it to the total and move to the parent's right neighbor
            if left % 2 == 1:
                total_sum += self.tree[left]
                left += 1
            # If right is a left child, add it to the total and move to the parent's left neighbor
            if right % 2 == 0:
                total_sum += self.tree[right]
                right -= 1
            # Move up to the parent nodes
            left //= 2
            right //= 2
        
        return total_sum
```

### Explanation:

1. **Segment Tree Construction (`__init__`)**:
   - We initialize the `tree` array of size `2 * n` where the first `n` indices are for internal nodes, and the last `n` indices are for leaf nodes.
   - The leaf nodes hold the values of the original array, and the internal nodes are built by summing up the values of the child nodes.

2. **Update Operation (`update`)**:
   - To update an element, we change its value in the corresponding leaf node and then propagate the changes upwards to update the internal nodes.
   - We keep dividing the index by 2 until we reach the root.

3. **Sum Query Operation (`sumRange`)**:
   - We perform a range sum query by combining the values from relevant segments.
   - If `left` is the right child of its parent, we include its value in the sum and move to the next segment.
   - Similarly, if `right` is the left child of its parent, we include its value and move.
   - This process continues until `left` exceeds `right`.

### Example Walkthrough:

For the example:

```python
nums = [1, 3, 5]
numArray = NumArray(nums)

# Query 1: sumRange(0, 2)
# Tree built: [0, 9, 4, 5, 1, 3, 5]
# sumRange(0, 2) = 9
result1 = numArray.sumRange(0, 2)  # Output: 9

# Update: update(1, 2)
# Tree updated: [0, 8, 3, 5, 1, 2, 5]
numArray.update(1, 2)

# Query 2: sumRange(0, 2)
# sumRange(0, 2) = 8
result2 = numArray.sumRange(0, 2)  # Output: 8
```

### Time and Space Complexity:

- **Time Complexity**:
  - **Build**: `O(n)` to construct the segment tree initially.
  - **Update**: `O(log n)` for updating a single element.
  - **Query**: `O(log n)` for summing a range.
  
- **Space Complexity**: `O(n)` to store the segment tree.

This approach provides efficient updates and range queries even for large arrays and multiple operations.
