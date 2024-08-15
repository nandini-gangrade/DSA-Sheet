# [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

To solve the problem of finding how much rainwater can be trapped after raining, we can utilize a two-pointer approach. Here's how the logic works:

### Problem Breakdown:
The idea is to compute the trapped water by calculating the difference between the height of the bars and the water that can be stored over them.

### Approach:

1. **Two Pointers (Left and Right):**
   - We maintain two pointers, `left` starting from the beginning and `right` starting from the end of the array.
   - The pointer with the smaller height (either `height[left]` or `height[right]`) determines how much water can be trapped at that index.
   - We calculate how much water can be trapped at each step based on the smaller height between the two pointers and move the corresponding pointer towards the middle.

2. **Tracking Maximum Heights:**
   - We maintain two variables `left_max` and `right_max` to store the maximum height encountered so far from the left and right side, respectively.
   - At every step, we calculate how much water can be trapped based on the difference between the current height and the minimum of `left_max` and `right_max`.

3. **Trapping Water Calculation:**
   - If `height[left] < height[right]`, the water trapped at the left index is determined by `left_max - height[left]`. Update `left_max` if needed and move the `left` pointer.
   - Otherwise, do the same for the `right` pointer by calculating the water trapped at the `right` index using `right_max`.

### Code Implementation:

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0

        left, right = 0, len(height) - 1
        left_max, right_max = height[left], height[right]
        trapped_water = 0

        while left < right:
            if height[left] < height[right]:
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    trapped_water += left_max - height[left]
                left += 1
            else:
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    trapped_water += right_max - height[right]
                right -= 1

        return trapped_water
```

### Explanation of the Code:

1. **Initial Check:**
   - If the input `height` array is empty, return `0` as no water can be trapped.

2. **Two Pointers:**
   - The `left` pointer starts from the beginning (`0`), and the `right` pointer starts from the end (`len(height) - 1`).
   - We initialize `left_max` and `right_max` to track the maximum heights encountered so far from the left and right, respectively.

3. **Main Loop:**
   - While `left < right`, we compare `height[left]` and `height[right]`.
   - If `height[left]` is less, it means we can only trap water based on the left side's maximum height. We update `left_max` if necessary and calculate how much water is trapped at the current `left` index.
   - If `height[right]` is less, we do the same on the right side, calculating the trapped water based on `right_max`.

4. **Water Calculation:**
   - For each position, the amount of water trapped is determined by the difference between the maximum height encountered so far and the current height at that position.

5. **Return:**
   - The total trapped water is stored in `trapped_water`, which is returned at the end.

### Example Walkthrough:

Let's consider the input:

```python
height = [0,1,0,2,1,0,1,3,2,1,2,1]
```

1. Initialize:
   - `left = 0`, `right = 11`, `left_max = 0`, `right_max = 1`, `trapped_water = 0`
2. First iteration (`left = 0` to `right = 11`):
   - Move `left` to `1`, update `left_max = 1`
   - No water is trapped at `left = 1` because `left_max = 1` and `height[left] = 1`.
3. Continue iterating and calculating:
   - At `left = 2`, water trapped is `1 - 0 = 1`.
   - At `left = 3`, water trapped is `2 - 1 = 1`.
   - The process continues until both pointers converge.

The total trapped water for this case is `6`.

### Time Complexity:

- The algorithm only traverses the array once, so the time complexity is **O(n)**, where `n` is the length of the `height` array.

### Space Complexity:

- The algorithm uses a constant amount of space, so the space complexity is **O(1)**.

### Example 2:

For the input `height = [4,2,0,3,2,5]`, the algorithm will calculate and return `9` as the amount of trapped water.

### Summary:

This solution efficiently computes the trapped rainwater using the two-pointer technique and takes advantage of keeping track of the maximum heights encountered from both sides to calculate the water trapped at each step.
