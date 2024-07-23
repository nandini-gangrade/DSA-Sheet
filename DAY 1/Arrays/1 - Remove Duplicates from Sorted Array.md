# [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Return the number of unique elements in `nums`.

### Example

**Input:** `nums = [1, 1, 2, 3, 3]`  
**Output:** `3, nums = [1, 2, 3, _, _]`  
**Explanation:** The function should return `3`, with the first three elements of `nums` being `1`, `2`, and `3` respectively.

## Intuition

Since the array is sorted, all duplicates will be adjacent. We can use a two-pointer technique to efficiently remove duplicates. Pointer `i` tracks the position for the next unique element, while pointer `j` scans through the array to find these unique elements.

## Approach

1. **Initialization:**
   - Set pointer `i` to `0`, which will mark the position of the last unique element.

2. **Iterate Through the Array:**
   - Use pointer `j` starting from index `1` to scan through the array.
   - Compare `nums[j]` with `nums[i]`. If they are different, increment `i` and update `nums[i]` with `nums[j]`.

3. **Return the Result:**
   - After iterating through the array, `i + 1` will be the number of unique elements.

## Code

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0

        i = 0  # Pointer for the position of the last unique element

        for j in range(1, len(nums)):
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]

        return i + 1  # Number of unique elements
```

## Complexity

- **Time Complexity:** O(n)  
  We iterate through the array once, where `n` is the length of the array.

- **Space Complexity:** O(1)  
  We use constant extra space as we modify the array in place.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solutions/5524617/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
