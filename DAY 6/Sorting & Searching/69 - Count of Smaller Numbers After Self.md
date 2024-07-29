# [315. Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/)

To solve the problem of finding the number of smaller elements to the right of each element in an array, an efficient approach is necessary due to the constraints. Given that the array length can be up to \(10^5\), a brute force solution with \(O(n^2)\) complexity is not feasible. Instead, we can use data structures that support efficient querying and updating, such as Binary Indexed Trees (BIT) or Balanced Binary Search Trees. 

## Approach

1. **Coordinate Compression**:
   - First, map the elements of the array to a smaller range if needed. This helps in efficiently using data structures like BIT.

2. **Binary Indexed Tree (BIT) or Fenwick Tree**:
   - Use BIT to keep track of counts of elements. The BIT helps in efficiently querying the number of smaller elements and updating the count as you process the array from right to left.

3. **Process the Array from Right to Left**:
   - For each element in the array, use BIT to count how many elements smaller than the current element have been processed.
   - Update BIT to include the current element.

### Steps

1. **Coordinate Compression**:
   - Convert the array elements to their ranks or indices in the sorted unique array. This makes the range manageable for BIT.

2. **Binary Indexed Tree Operations**:
   - **Update Operation**: Increment the count for an element in BIT.
   - **Query Operation**: Retrieve the count of elements smaller than the current element.

3. **Processing**:
   - Traverse the array from right to left, updating the BIT and querying it to find how many smaller elements exist to the right of the current element.

## Python Code

Here is a Python implementation using BIT:

```python
class Solution:
    def countSmaller(self, nums):
        def update(bit, index, val):
            while index < len(bit):
                bit[index] += val
                index += index & -index

        def query(bit, index):
            sum = 0
            while index > 0:
                sum += bit[index]
                index -= index & -index
            return sum

        # Coordinate compression
        sorted_nums = sorted(set(nums))
        rank_map = {num: i + 1 for i, num in enumerate(sorted_nums)}
        size = len(sorted_nums)
        
        bit = [0] * (size + 1)
        result = []
        
        for num in reversed(nums):
            rank = rank_map[num]
            result.append(query(bit, rank - 1))
            update(bit, rank, 1)
        
        return result[::-1]
```

### Explanation

1. **Coordinate Compression**:
   - Map each unique number to its rank in the sorted order to use as indices in BIT.

2. **Binary Indexed Tree (BIT)**:
   - **Update Function**: Updates the BIT at the specified index.
   - **Query Function**: Retrieves the cumulative frequency up to the specified index.

3. **Processing**:
   - Traverse the input array from right to left.
   - For each element, query BIT for the count of smaller elements and update BIT with the current element's rank.

## Complexity

- **Time Complexity**: \(O(n \log n)\)
  - Building the coordinate compression map takes \(O(n \log n)\).
  - Each update and query operation on BIT takes \(O(\log n)\), and these operations are done \(n\) times.
- **Space Complexity**: \(O(n)\)
  - Space for the BIT and the result list.

This approach efficiently computes the number of smaller elements to the right of each element in the array.
