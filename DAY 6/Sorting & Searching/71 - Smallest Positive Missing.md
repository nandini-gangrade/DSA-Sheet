# S[mallest Positive Missing](https://www.geeksforgeeks.org/problems/smallest-positive-missing-number-1587115621/1)

You are given an array of \( N \) integers. The task is to find the smallest positive number that is missing from the array. Positive numbers start from 1. 

### Example

**Example 1:**

- **Input:** `arr = [1, 2, 3, 4, 5]`
- **Output:** `6`
- **Explanation:** The smallest positive missing number is 6, as all numbers from 1 to 5 are present.

**Example 2:**

- **Input:** `arr = [0, -10, 1, 3, -20]`
- **Output:** `2`
- **Explanation:** The smallest positive missing number is 2, as 1 is present but 2 is missing.

## Intuition

The goal is to find the smallest missing positive integer efficiently. A common approach is to use the array itself for marking the presence of numbers in the range `[1, N]`. By rearranging the array and marking indices, we can determine the smallest missing positive integer.

## Approach

1. **Separate Positive Numbers**:
   - First, separate positive numbers from non-positive numbers by rearranging them. This ensures that only positive numbers are considered in the next steps.

2. **Mark Presence**:
   - Use the indices of the array to mark the presence of each positive integer. If the number `num` exists in the range `[1, N]`, mark the index `num - 1` as negative.

3. **Find Missing Number**:
   - Traverse the array to find the first index with a positive value. This index corresponds to the smallest missing positive integer. If all indices from `0` to `N-1` are negative, then the smallest missing positive integer is `N + 1`.

## Code

```python
class Solution:
    # Function to find the smallest positive number missing from the array.
    def missingNumber(self, arr, n):
        # Separate positive numbers from non-positive numbers
        j = 0
        for i in range(n):
            if arr[i] > 0:
                arr[i], arr[j] = arr[j], arr[i]
                j += 1

        # Mark presence of each positive number
        for i in range(j):
            num = abs(arr[i])
            if num - 1 < j and arr[num - 1] > 0:
                arr[num - 1] = -arr[num - 1]

        # Find the first missing positive number
        for i in range(j):
            if arr[i] > 0:
                return i + 1

        # If all numbers from 1 to j are present, then the next missing number is j + 1
        return j + 1
```

## Complexity

- **Time Complexity**: \(O(N)\)
  - Each element is processed a constant number of times (during separation, marking, and checking), leading to linear time complexity.

- **Space Complexity**: \(O(1)\)
  - The solution operates in-place with no additional space required except for a few variables.

This approach efficiently finds the smallest missing positive integer by leveraging the array's indices for marking presence, achieving linear time complexity and constant space complexity.
