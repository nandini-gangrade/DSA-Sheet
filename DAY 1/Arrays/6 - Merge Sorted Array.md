# 88. [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
[Leetcode Solution](https://leetcode.com/problems/merge-sorted-array/solutions/5525044/best-solution-challenge-day-1-revisewitharsh)

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively. The task is to merge `nums1` and `nums2` into a single array sorted in non-decreasing order, stored in `nums1`.

- `nums1` has a length of `m + n`, where the first `m` elements are the elements that should be merged, and the last `n` elements are set to `0` and should be ignored.
- `nums2` has a length of `n`.

### Examples

**Example 1:**

- **Input:**  
  `nums1 = [1,2,3,0,0,0]`, `m = 3`  
  `nums2 = [2,5,6]`, `n = 3`
  
- **Output:**  
  `[1,2,2,3,5,6]`

- **Explanation:**  
  The arrays being merged are `[1,2,3]` and `[2,5,6]`. The result is `[1,2,2,3,5,6]`.

**Example 2:**

- **Input:**  
  `nums1 = [1]`, `m = 1`  
  `nums2 = []`, `n = 0`

- **Output:**  
  `[1]`

- **Explanation:**  
  The arrays being merged are `[1]` and `[]`. The result is `[1]`.

**Example 3:**

- **Input:**  
  `nums1 = [0]`, `m = 0`  
  `nums2 = [1]`, `n = 1`

- **Output:**  
  `[1]`

- **Explanation:**  
  The arrays being merged are `[]` and `[1]`. The result is `[1]`.

### Constraints

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-10^9 <= nums1[i], nums2[j] <= 10^9`

## Intuition

Since the arrays `nums1` and `nums2` are already sorted, we can take advantage of this to perform an efficient merge. Instead of using extra space to store the merged array, we can utilize the empty space at the end of `nums1` (the trailing zeros) to merge the arrays in-place. We will fill `nums1` from the back to ensure that we don't overwrite any elements before they are processed.

## Approach

1. **Initialize Pointers:**
   - Use three pointers:
     - `p1` for tracking the current index in the original `nums1` (i.e., up to `m`).
     - `p2` for tracking the current index in `nums2`.
     - `p` for tracking the position in `nums1` where the next largest element should be placed (starts from `m + n - 1`).

2. **Merge from Back to Front:**
   - Compare elements at `p1` and `p2`:
     - If `nums1[p1] > nums2[p2]`, place `nums1[p1]` at `nums1[p]` and decrement `p1`.
     - Otherwise, place `nums2[p2]` at `nums1[p]` and decrement `p2`.
   - Decrement `p` in each step.

3. **Copy Remaining Elements:**
   - If `nums2` still has elements left after `p1` is exhausted, copy them into `nums1`.

4. **Return:**
   - Since the function modifies `nums1` in place, there is no need to return it.

## Code

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        # Initialize the pointers
        p1, p2, p = m - 1, n - 1, m + n - 1

        # Merge in reverse order
        while p1 >= 0 and p2 >= 0:
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            p -= 1

        # If there are remaining elements in nums2, copy them
        while p2 >= 0:
            nums1[p] = nums2[p2]
            p2 -= 1
            p -= 1
```

## Complexity Analysis

- **Time Complexity:** \(O(m + n)\)  
  The algorithm iterates through both arrays once, merging them in a single pass.

- **Space Complexity:** \(O(1)\)  
  The algorithm modifies `nums1` in place without using additional space for another array, thus achieving constant space complexity.

This approach effectively leverages the fact that both arrays are sorted, allowing for an efficient merge process using the available space in `nums1`.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/merge-sorted-array/solutions/5525044/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
