# [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/description/)

To solve the problem of finding the maximum value in each sliding window of size `k` across an array, you can use a deque (double-ended queue) to efficiently keep track of indices of potential maximum values. This approach allows you to maintain an O(n) time complexity, where n is the length of the array. Here's a step-by-step explanation and the implementation:

### Approach

1. **Initialize a Deque:**
   - Use a deque to store indices of array elements. This deque will help in tracking the maximum element in the current window.

2. **Maintain the Deque:**
   - The deque will store indices in such a way that:
     - The elements corresponding to the indices in the deque are in decreasing order.
     - The front of the deque always represents the maximum element of the current window.
   - Remove indices from the deque that are out of the bounds of the current window.
   - Remove indices from the deque's back if the current element is greater than the element at those indices (since they can no longer be the maximum if the current element is greater).

3. **Update the Result:**
   - After processing each element, the front of the deque will be the index of the maximum element for the current window. Add this maximum to the result list once you have processed the first `k` elements.

### Implementation

Here's the code that implements this approach:

```python
from collections import deque
from typing import List

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # Initialize the deque and the result list
        dq = deque()
        max_values = []

        # Process each element in the array
        for i in range(len(nums)):
            # Remove elements not within the window
            if dq and dq[0] < i - k + 1:
                dq.popleft()

            # Remove elements from the back of the deque if they are smaller than the current element
            while dq and nums[dq[-1]] < nums[i]:
                dq.pop()

            # Add the current element's index to the deque
            dq.append(i)

            # If our window has reached size k, add the maximum element to the result
            if i >= k - 1:
                max_values.append(nums[dq[0]])

        return max_values
```

### Explanation

1. **Initialization:**
   - `dq` is used to maintain indices of the elements in a way that the element corresponding to the index at the front is always the largest in the current window.
   - `max_values` stores the maximum values of each sliding window.

2. **Processing Elements:**
   - For each element `nums[i]`:
     - Remove indices from `dq` that are out of the bounds of the current window.
     - Remove indices from the back of `dq` while the current element `nums[i]` is greater than the element at those indices. This maintains the decreasing order in `dq`.
     - Add the current index `i` to `dq`.

3. **Update Results:**
   - Once the first window is processed (i.e., `i >= k - 1`), append the maximum value of the current window (element at index `dq[0]`) to `max_values`.

### Complexity

- **Time Complexity:** O(n), where n is the length of `nums`. Each element is added and removed from the deque at most once.
- **Space Complexity:** O(k), where k is the size of the sliding window, due to the space used by the deque.

This approach efficiently computes the maximum values in each sliding window while maintaining an optimal time complexity.
