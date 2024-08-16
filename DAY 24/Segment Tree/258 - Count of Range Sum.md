# [327. Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/description/)

To solve the problem of counting range sums that lie between `lower` and `upper`, we can use a combination of **prefix sums** and **merge sort** to efficiently count the ranges. This problem can be tackled using a modified divide-and-conquer approach, similar to merge sort, which helps us count the number of valid range sums in `O(n log n)` time.

### Key Concept: Prefix Sums

- **Prefix Sum**: The sum of elements from the start of the array to a given index `i`.
  - Let `prefix[i] = sum(nums[0] to nums[i-1])`.
- The **range sum** between indices `i` and `j` is:
  - `sum(nums[i] to nums[j]) = prefix[j+1] - prefix[i]`.
- Thus, we are interested in finding all pairs `(i, j)` such that `lower <= prefix[j+1] - prefix[i] <= upper`.

### Approach:
1. **Prefix Sum Calculation**: Compute the prefix sum for the array, which will allow us to compute any range sum as a difference between two prefix sums.
  
2. **Divide-and-Conquer with Merge Sort**: We use a merge sort-like approach to maintain the order of prefix sums while counting how many valid range sums (i.e., differences between prefix sums) fall within the `[lower, upper]` range during the merge step.

3. **Counting Valid Range Sums**: While merging two halves of the prefix sums array, for each element in the left half, we count how many elements in the right half form a valid range sum by checking if the difference lies between `lower` and `upper`.

### Code Implementation:

```python
class Solution:
    def countRangeSum(self, nums: List[int], lower: int, upper: int) -> int:
        # Function to count range sums using modified merge sort
        def countWhileMerging(left, right):
            if right - left <= 1:  # Base case: if the range is of length 1 or less
                return 0
            
            mid = (left + right) // 2
            count = countWhileMerging(left, mid) + countWhileMerging(mid, right)
            
            # Count the range sums in the merged array
            j = k = t = mid
            temp = []
            for i in range(left, mid):
                while k < right and prefix[k] - prefix[i] < lower:
                    k += 1
                while j < right and prefix[j] - prefix[i] <= upper:
                    j += 1
                while t < right and prefix[t] < prefix[i]:
                    temp.append(prefix[t])
                    t += 1
                temp.append(prefix[i])
                count += j - k  # Count valid sums
                
            # Finish merging the two halves
            temp.extend(prefix[t:right])
            prefix[left:left+len(temp)] = temp
            
            return count
        
        # Step 1: Compute prefix sums
        prefix = [0]
        for num in nums:
            prefix.append(prefix[-1] + num)
        
        # Step 2: Use merge sort to count valid range sums
        return countWhileMerging(0, len(prefix))

```

### Explanation of the Code:

1. **Prefix Sum Calculation**:
   - We start by calculating the prefix sums of the `nums` array. This gives us an array `prefix` where `prefix[i]` represents the sum of the subarray from `nums[0]` to `nums[i-1]`.

2. **Merge Sort with Count**:
   - The function `countWhileMerging` is a recursive function that splits the `prefix` array into two halves, sorts them, and counts valid range sums.
   - For each element in the left half, it tries to find how many elements in the right half satisfy the condition:
     - `lower <= prefix[j+1] - prefix[i] <= upper`.
   - It uses two pointers `j` and `k` to find how many elements in the right half satisfy the range condition for each element in the left half.
   - It merges the two halves while counting the valid range sums.

3. **Merge Process**:
   - During the merge step, we sort the elements in the two halves and count the valid sums simultaneously.
   - After counting the valid sums, the two halves are merged back in sorted order.

### Example Walkthrough:

For the input:

```python
nums = [-2, 5, -1]
lower = -2
upper = 2
```

1. **Prefix Sums**:
   - `prefix = [0, -2, 3, 2]`.

2. **Merge Sort with Counting**:
   - The algorithm recursively splits the `prefix` array into two halves and counts valid range sums while merging:
     - The range sums for indices `(i, j)` that fall within the bounds `[-2, 2]` are counted as:
       - Range `[0, 0]` sum is `-2`.
       - Range `[2, 2]` sum is `-1`.
       - Range `[0, 2]` sum is `0`.

3. **Final Result**:
   - The total number of valid ranges is `3`.

### Time and Space Complexity:

- **Time Complexity**: `O(n log n)` — The algorithm runs in logarithmic time for both splitting the array (like merge sort) and counting the range sums during the merge step.
  
- **Space Complexity**: `O(n)` — We use additional space for storing the prefix sums and temporary arrays during the merge process.

This approach efficiently handles large input sizes up to `10^5` elements, making it suitable for competitive programming scenarios.
