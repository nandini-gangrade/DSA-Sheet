# 75. Sort Colors
[Leetcode Solution](https://leetcode.com/problems/sort-colors/solutions/5529132/best-solution-challenge-day-2-revisewitharsh/)

Given an array `nums` with \(n\) objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue. Use the integers 0, 1, and 2 to represent the colors red, white, and blue, respectively. Solve this problem without using the library's sort function.

### Examples

**Example 1:**

- **Input:** `nums = [2,0,2,1,1,0]`
- **Output:** `[0,0,1,1,2,2]`

**Example 2:**

- **Input:** `nums = [2,0,1]`
- **Output:** `[0,1,2]`

### Constraints

- \(n == \text{nums.length}\)
- \(1 \leq n \leq 300\)
- \(\text{nums}[i]\) is either 0, 1, or 2.

## Intuition

The problem is similar to the "Dutch National Flag" problem proposed by Edsger Dijkstra. The goal is to sort the array in one pass using three pointers: one to track the position of zeros, one for twos, and another for traversing the array.

## Approach

1. **Initialize Pointers:**
   - `low`: Initially set to the start of the array to track the boundary of zeros.
   - `mid`: Initially set to the start of the array to traverse the elements.
   - `high`: Initially set to the end of the array to track the boundary of twos.

2. **Traverse and Swap:**
   - Traverse the array with the `mid` pointer:
     - If `nums[mid]` is 0, swap it with `nums[low]`, and increment both `low` and `mid`.
     - If `nums[mid]` is 1, increment `mid`.
     - If `nums[mid]` is 2, swap it with `nums[high]` and decrement `high`.

3. **Continue Until `mid` Exceeds `high`:**
   - The process continues until the `mid` pointer exceeds the `high` pointer, ensuring all zeros are moved to the front, twos to the end, and ones in the middle.

## Code

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        # Initialize pointers
        low, mid, high = 0, 0, len(nums) - 1

        # Traverse and swap
        while mid <= high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                mid += 1
            else:  # nums[mid] == 2
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm makes a single pass through the array, performing constant-time operations on each element.

- **Space Complexity:** \(O(1)\)  
  The solution uses only a fixed amount of extra space for the pointers, making it an in-place sorting algorithm.

This approach efficiently sorts the array using a one-pass algorithm with constant extra space, as required by the problem's constraints.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/sort-colors/solutions/5529132/best-solution-challenge-day-2-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
