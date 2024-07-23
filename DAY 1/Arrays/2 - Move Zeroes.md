# [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)
Given an integer array `nums`, move all `0`s to the end of it while maintaining the relative order of the non-zero elements.

**Constraints:**
- `1 <= nums.length <= 10^4`
- `-2^31 <= nums[i] <= 2^31 - 1`

**Example 1:**
- **Input:** `nums = [0, 1, 0, 3, 12]`
- **Output:** `[1, 3, 12, 0, 0]`

**Example 2:**
- **Input:** `nums = [0]`
- **Output:** `[0]`

## Intuition
The key insight here is that we need to maintain the relative order of non-zero elements while moving all zeros to the end. We can achieve this efficiently by using a two-pointer technique.

## Approach
1. **Initialization:**
   - Use a pointer `last_non_zero_index` to keep track of the position where the next non-zero element should be placed. Initialize it to `0`.

2. **Iterate Through the Array:**
   - Traverse the array using a second pointer `current`.
   - Whenever a non-zero element is encountered at `current`, place it at the `last_non_zero_index` position and increment `last_non_zero_index`.

3. **Fill Remaining Positions with Zeros:**
   - After processing all elements, all positions from `last_non_zero_index` to the end of the array should be set to `0`.

## Code

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        last_non_zero_index = 0
        
        # Move non-zero elements to the front
        for current in range(len(nums)):
            if nums[current] != 0:
                nums[last_non_zero_index] = nums[current]
                last_non_zero_index += 1
        
        # Fill the remaining positions with zeros
        for i in range(last_non_zero_index, len(nums)):
            nums[i] = 0
```

### Explanation
1. **Moving Non-Zero Elements:**
   - As we iterate through the array, every time we find a non-zero element, we place it at the position indicated by `last_non_zero_index` and then increment `last_non_zero_index`.

2. **Setting Zeros:**
   - After all non-zero elements have been moved to their correct positions, we set all remaining positions in the array to `0`.

## Complexity Analysis

- **Time Complexity:** O(n)
  We traverse the array twice, once to move non-zero elements and once to fill in zeros.
- **Space Complexity:** O(1)
  We use constant extra space as we modify the array in place.

This approach ensures that the relative order of non-zero elements is preserved while efficiently moving all zeros to the end of the array.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/move-zeroes/solutions/5524919/best-solution-challenge-day-1-revisewitharsh/) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
