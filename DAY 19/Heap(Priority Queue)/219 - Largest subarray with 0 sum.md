# [Largest subarray with 0 sum](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)

### Problem Explanation

The task is to find the length of the largest subarray within a given array where the sum of the elements is zero. A subarray is a contiguous part of the array, and its sum is simply the sum of its elements.

### Approach & Intuition

To solve this problem, we'll use a **prefix sum** approach along with a **hash map (dictionary)** to track the first occurrence of each prefix sum. 

**Step-by-Step Approach:**

1. **Prefix Sum Calculation:**
   - Traverse the array while maintaining a running sum (`sumi`). This sum is called the prefix sum and represents the sum of the array elements from the start up to the current index.

2. **Handling Prefix Sum:**
   - If the prefix sum has been seen before at some earlier index, it means that the elements between that earlier index and the current index sum to zero. The difference in indices gives the length of the subarray with sum zero.
   - If the prefix sum is zero, it means the subarray from the start of the array to the current index has a sum of zero.

3. **Dictionary Storage:**
   - Use a dictionary (`dic`) to store the first occurrence of each prefix sum along with its index. This allows for quick look-up to determine if the same prefix sum has been seen before.

4. **Tracking Maximum Length:**
   - Track the maximum length of any zero-sum subarray found during the traversal.

### Code Implementation

```python
from collections import defaultdict

class Solution:
    def maxLen(self, n, arr):
        # Dictionary to store the first occurrence of each prefix sum
        dic = defaultdict(int)
        dic[0] = -1  # Initialize with -1 to handle the case when the zero-sum subarray starts from the beginning
        sumi = 0
        max_len = 0
        
        # Traverse the array
        for i in range(n):
            sumi += arr[i]  # Calculate prefix sum
            
            # If the prefix sum has been seen before, calculate the subarray length
            if sumi in dic:
                max_len = max(max_len, i - dic[sumi])
            else:
                # Store the first occurrence of the prefix sum
                dic[sumi] = i
        
        return max_len
```

### Complexity Analysis

- **Time Complexity:** 
  - The time complexity is **O(n)** where `n` is the length of the array. This is because we traverse the array once while checking and updating the dictionary.

- **Space Complexity:**
  - The space complexity is **O(n)** for the dictionary that stores the prefix sums and their indices.

### Example Explanation

- **Example 1:**
  - Input: `arr = [15, -2, 2, -8, 1, 7, 10, 23]`
  - Output: `5`
  - Explanation: The subarray `[-2, 2, -8, 1, 7]` sums to zero, and its length is 5.

- **Example 2:**
  - Input: `arr = [2, 10, 4]`
  - Output: `0`
  - Explanation: There is no subarray with a sum of zero, so the output is 0.

- **Example 3:**
  - Input: `arr = [1, 0, -4, 3, 1, 0]`
  - Output: `5`
  - Explanation: The subarray `[0, -4, 3, 1, 0]` sums to zero, and its length is 5.

This approach ensures that we efficiently find the largest subarray with a sum of zero while maintaining the required time and space complexity constraints.
