# [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/)

To solve the problem of efficiently calculating the sum of elements in an array between indices `left` and `right` (inclusive), we can use a technique called **prefix sum**. This approach allows us to preprocess the array such that each range query can be answered in constant time `O(1)` after an `O(n)` preprocessing step.

### Approach:

1. **Prefix Sum Array**:
   - We create a prefix sum array `prefix_sum` where each element at index `i` contains the sum of the elements from the start of the array up to index `i`.
   - This allows us to calculate the sum of any subarray from index `left` to `right` as:
     \[
     \text{sumRange(left, right)} = \text{prefix\_sum[right]} - \text{prefix\_sum[left - 1]}
     \]
   - If `left == 0`, we can directly use `prefix_sum[right]` because it gives the sum from the start to the `right` index.

2. **Preprocessing**:
   - We initialize a prefix sum array where:
     \[
     \text{prefix\_sum}[i] = \text{nums}[0] + \text{nums}[1] + ... + \text{nums}[i]
     \]
   - This takes `O(n)` time.

3. **Query**:
   - For each query, we can now calculate the sum in constant time `O(1)` by using the formula mentioned above.

### Solution Code:

```python
class NumArray:

    def __init__(self, nums: List[int]):
        # Create a prefix sum array to store the cumulative sum up to each index
        self.prefix_sum = [0] * (len(nums) + 1)
        
        # Precompute the prefix sum array
        for i in range(1, len(nums) + 1):
            self.prefix_sum[i] = self.prefix_sum[i - 1] + nums[i - 1]
        
    def sumRange(self, left: int, right: int) -> int:
        # Return the sum of the subarray from index left to right
        return self.prefix_sum[right + 1] - self.prefix_sum[left]
```

### Explanation:

1. **Constructor (`__init__`)**:
   - The `prefix_sum` array is created, where `prefix_sum[i]` stores the cumulative sum of elements from `nums[0]` to `nums[i-1]`.
   - The loop computes the prefix sum for each index.

2. **`sumRange` Function**:
   - Given the `left` and `right` indices, the function returns the difference:
     \[
     \text{prefix\_sum}[right + 1] - \text{prefix\_sum}[left]
     \]
   - This gives the sum of elements between indices `left` and `right` in constant time.

### Example Walkthrough:

Let's go through an example:

#### Example 1:

```python
nums = [-2, 0, 3, -5, 2, -1]
numArray = NumArray(nums)

# Query 1: sumRange(0, 2)
# prefix_sum = [0, -2, -2, 1, -4, -2, -3]
# sumRange(0, 2) = prefix_sum[3] - prefix_sum[0] = 1 - 0 = 1
result1 = numArray.sumRange(0, 2)  # Output: 1

# Query 2: sumRange(2, 5)
# sumRange(2, 5) = prefix_sum[6] - prefix_sum[2] = -3 - (-2) = -1
result2 = numArray.sumRange(2, 5)  # Output: -1

# Query 3: sumRange(0, 5)
# sumRange(0, 5) = prefix_sum[6] - prefix_sum[0] = -3 - 0 = -3
result3 = numArray.sumRange(0, 5)  # Output: -3
```

### Time and Space Complexity:

- **Time Complexity**:
  - Initialization (`__init__`): `O(n)` where `n` is the number of elements in the array `nums`, as we are computing the prefix sum for all elements.
  - Query (`sumRange`): `O(1)` for each query, as it only involves a couple of array lookups and a subtraction.

- **Space Complexity**:
  - The space complexity is `O(n)` due to the storage of the prefix sum array.

This solution is efficient and meets the problem constraints well. Each query is answered in constant time, making it scalable for large arrays and multiple queries.
