# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)
[LeetCode Solution](https://leetcode.com/problems/container-with-most-water/solutions/5535434/step-by-step-explanation-challenge-day-2-revisewitharsh)

Given an integer array `height` of length n, where each element represents the height of a vertical line at the respective index, find two lines that form a container with the x-axis to store the maximum amount of water.

### Examples

**Example 1:**

- **Input:** `height = [1,8,6,2,5,4,8,3,7]`
- **Output:** `49`

**Example 2:**

- **Input:** `height = [1,1]`
- **Output:** `1`

### Constraints

- n == height.length
- 2 <= n <= 10^5
- 0 <= height[i] <= 10^4

## Intuition

The key insight is that the amount of water a container can store is determined by the shorter of the two lines, as the water cannot go above the shorter line. Thus, the area of water the container can store is calculated as:

`Area=min(height[i],height[j])×(j−i)`

where \( i \) and \( j \) are the indices of the two lines forming the container.

## Approach

1. **Initialize Two Pointers:** Start with two pointers, `left` at the beginning (0) and `right` at the end (n-1) of the array.

2. **Calculate Area:** Compute the area formed between the lines at these two pointers.

3. **Update Maximum Area:** Track the maximum area encountered.

4. **Move Pointers:** To maximize the area, move the pointer pointing to the shorter line inward (i.e., increment `left` if `height[left] < height[right]`, else decrement `right`).

5. **Repeat:** Continue this process until the two pointers meet.

## Code

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_area = 0
        
        while left < right:
            # Calculate the area between the lines at the two pointers
            current_area = min(height[left], height[right]) * (right - left)
            # Update max_area if the current_area is larger
            max_area = max(max_area, current_area)
            
            # Move the pointer pointing to the shorter line
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        
        return max_area
```

### Complexity Analysis

- **Time Complexity:** (O(n)  
  The algorithm traverses the array with two pointers, each moving at most n times.

- **Space Complexity:** (O(1) 
  The algorithm uses a constant amount of extra space, regardless of the input size.

This approach efficiently finds the maximum area by using the two-pointer technique to explore all possible containers formed by the lines.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 


![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

`Let's tackle these coding challenges together! 🚀`
