# [47. Permutations II](https://leetcode.com/problems/permutations-ii/description/)

The error `AttributeError: 'Solution' object has no attribute 'permuteUnique'` indicates that the code is trying to call a method named `permuteUnique` on an instance of the `Solution` class, but the method doesn't exist in that class.

If you're working on a problem where you need to generate all unique permutations of a list of numbers (which may contain duplicates), you need to define a `permuteUnique` method in your `Solution` class.

Here's how you can define the `permuteUnique` method:

### Problem Statement:
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

### Example:
```python
Input: nums = [1,1,2]
Output: [[1,1,2], [1,2,1], [2,1,1]]
```

### Implementation:
```python
class Solution:
    def permuteUnique(self, nums):
        result = []
        nums.sort()  # Sort the array to handle duplicates
        
        def backtrack(path, used):
            if len(path) == len(nums):
                result.append(path[:])  # Add a copy of the current path (one permutation)
                return
            
            for i in range(len(nums)):
                if used[i]:
                    continue  # Skip already used elements
                if i > 0 and nums[i] == nums[i-1] and not used[i-1]:
                    continue  # Skip duplicates
                
                used[i] = True
                path.append(nums[i])
                backtrack(path, used)
                path.pop()  # Backtrack
                used[i] = False
        
        backtrack([], [False] * len(nums))
        return result
```

### Explanation:
1. **Sorting**: The input list `nums` is sorted initially. This helps in easily skipping over duplicates during the permutation generation.

2. **Backtracking**: 
   - `path` keeps track of the current permutation being built.
   - `used` is a list of booleans that indicates whether a particular element in `nums` has been used in the current permutation.
   - For each element in `nums`, we decide whether to include it in the current permutation. If the element is already used or is a duplicate that has not been used in the previous position, it is skipped.

3. **Adding the Permutation**:
   - When the length of `path` matches the length of `nums`, it means we have a complete permutation, which we then add to `result`.

4. **Avoiding Duplicates**:
   - The check `if i > 0 and nums[i] == nums[i-1] and not used[i-1]` ensures that duplicates are skipped unless they have been used in the previous position.

### Example Usage:
```python
solution = Solution()
result = solution.permuteUnique([1,1,2])
print(result)  # Output: [[1,1,2], [1,2,1], [2,1,1]]
```

This will correctly generate all unique permutations of the input list.

### Common Issues:
- **Not Sorting the Input List**: If the input list is not sorted, it becomes difficult to skip duplicates correctly.
- **Incorrect Handling of Duplicates**: Ensure that duplicates are skipped in a way that doesn't miss valid permutations. This is handled by checking `if i > 0 and nums[i] == nums[i-1] and not used[i-1]`.

If you replace your current `Solution` class with this code, the `permuteUnique` method should work without any issues.
