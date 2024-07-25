# [442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/description/)
[LeetCode Solution](https://leetcode.com/problems/find-all-duplicates-in-an-array/solutions/5535347/step-by-step-explanation-challenge-day-2-revisewitharsh)

Given an integer array `nums` of length \(n\) where all integers are in the range \([1, n]\) and each integer appears once or twice, return an array of all integers that appear twice.

### Examples

**Example 1:**

- **Input:** `nums = [4,3,2,7,8,2,3,1]`
- **Output:** `[2,3]`

**Example 2:**

- **Input:** `nums = [1,1,2]`
- **Output:** `[1]`

**Example 3:**

- **Input:** `nums = [1]`
- **Output:** `[]`

### Constraints

- \(n = \text{nums.length}\)
- \(1 \leq n \leq 10^5\)
- \(1 \leq \text{nums}[i] \leq n\)
- Each element in `nums` appears once or twice.

## Intuition

The key insight is that since each number is in the range \([1, n]\) and the array length is \(n\), we can use the indices of the array itself to track whether a number has been seen before. By negating the number at the index corresponding to the current number, we can mark it as visited. If we encounter a number and the number at its corresponding index is already negative, it means we've seen this number before.

## Approach

1. **Iterate over the array:** For each number in `nums`, treat the absolute value of that number as an index.

2. **Negate the value at the calculated index:** If the value at this index is already negative, it means the number corresponding to this index has appeared before, so it is a duplicate.

3. **Collect duplicates:** Keep a list of all numbers that you encounter as duplicates.

4. **Return the list of duplicates.**

## Code

```python
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        duplicates = []  # List to store duplicate numbers
        
        for num in nums:
            index = abs(num) - 1  # Calculate index (0-based)
            
            if nums[index] < 0:
                # If the number at index is negative, it's a duplicate
                duplicates.append(abs(num))
            else:
                # Otherwise, negate the number at the calculated index
                nums[index] = -nums[index]
        
        return duplicates
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm iterates over the array once, performing constant-time operations for each element.

- **Space Complexity:** \(O(1)\)  
  The algorithm uses only a fixed amount of extra space for storing duplicates, aside from the input and output.

This approach efficiently identifies duplicates in the array without requiring additional data structures, making it both time and space efficient.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 


![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

`Let's tackle these coding challenges together! 🚀
`
