# [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

1. **Understand the Rotation**:
   - The array is originally sorted in ascending order.
   - It may have been rotated at some pivot, but the resulting array remains partially sorted in two segments.

2. **Objective**:
   - Find the index of the target value if it exists in the rotated array, or return -1 if it does not.

## Approach

1. **Identify the Pivot**:
   - The pivot is the point where the array was rotated. It divides the array into two sorted sub-arrays.

2. **Use Modified Binary Search**:
   - Perform a binary search considering the properties of the rotated array. In each step, determine which part of the array is sorted and whether the target might be in that segment.

### Steps

1. **Binary Search Algorithm**:
   - Start with the full range of the array.
   - Find the mid-point and check if the target is at the mid-point.
   - Determine if the left or right half is sorted:
     - If the left half is sorted and the target is within this range, narrow the search to the left half.
     - If the right half is sorted and the target is within this range, narrow the search to the right half.
   - Adjust the search range accordingly.

## Python Code

Here’s how you can implement this:

```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            # Check if mid is the target
            if nums[mid] == target:
                return mid
            
            # Determine which side is sorted
            if nums[left] <= nums[mid]:
                # Left side is sorted
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                # Right side is sorted
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
        
        return -1
```

### Explanation

1. **Initialization**:
   - Set `left` and `right` pointers to the start and end of the array, respectively.

2. **Binary Search Loop**:
   - Calculate the mid-point of the current search range.
   - Check if the mid-point is the target.
   - Identify which half of the array is sorted.
   - Adjust the search range based on where the target might be.

3. **Exit Condition**:
   - If the target is found, return its index.
   - If the search range becomes invalid (left > right), return -1 indicating that the target is not in the array.

## Complexity

- **Time Complexity**: \( O(\log n) \) due to the binary search.
- **Space Complexity**: \( O(1) \) as no extra space is used other than a few variables.

This approach ensures that you efficiently find the target in a rotated sorted array while maintaining logarithmic runtime complexity.
