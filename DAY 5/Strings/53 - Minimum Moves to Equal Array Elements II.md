# [462. Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/)
[LC Solution](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/solutions/4552469/microsoft-easy-solution-challenge)

To solve the problem of finding the minimum number of moves required to make all elements of an integer array equal, we can use a median-based approach. The intuition behind using the median is that minimizing the sum of absolute differences between elements is achieved when they are all equal to the median of the array. Here's how you can implement this solution in Python:

## Intuition

1. **Median as the Target**: 
   - When you want to minimize the total distance (or cost) to make all elements equal, the optimal target value is the median of the array.
   - This is because the median minimizes the sum of absolute deviations from it.

2. **Calculate Moves**: 
   - Once you have the median, calculate the sum of absolute differences between each element and the median.
   - This gives you the total number of moves required.

## Approach

1. **Sort the Array**: 
   - First, sort the array to easily find the median.

2. **Find the Median**: 
   - For an odd-length array, the median is the middle element.
   - For an even-length array, any element between the two middle elements minimizes the distance.

3. **Calculate the Total Moves**:
   - Iterate through the array and compute the sum of absolute differences from the median.

## Code

```python
class Solution:
    def minMoves2(self, nums):
        # Sort the array to find the median
        nums.sort()
        
        # Find the median
        median = nums[len(nums) // 2]
        
        # Calculate the total moves required
        moves = sum(abs(num - median) for num in nums)
        
        return moves
```

## Complexity Analysis

- **Time Complexity**: \(O(n \log n)\) due to the sorting step, where \(n\) is the number of elements in the array.
- **Space Complexity**: \(O(1)\), as we are sorting the array in place and using a constant amount of additional space for calculations.

This approach efficiently calculates the minimum moves required to make all elements in the array equal by aligning them to the median.
