# [90. Subsets II](https://leetcode.com/problems/subsets-ii/description/)

To solve the problem of generating all subsets (the power set) from a given array of integers that may contain duplicates, we can use **backtracking** while ensuring that we avoid duplicate subsets.

### Key Points:
1. **Backtracking**:
   - Backtracking is a method used to explore all possible combinations. Here, we'll generate all subsets of the array step by step by either including or excluding each element.
   
2. **Handling Duplicates**:
   - The input array may contain duplicates, so after sorting the array, we can avoid generating duplicate subsets by skipping elements that are the same as the previous one, but only after the previous one has been used.

3. **Approach**:
   - First, sort the input array `nums` to ensure duplicates are adjacent.
   - Use a backtracking function to explore all possible subsets. For each element, decide whether to include it in the current subset or skip it.
   - To avoid duplicate subsets, when we encounter a duplicate number, we skip it unless it's the first instance in the current recursive branch.

### Algorithm:
1. **Sort** the array `nums` to ensure duplicates are adjacent.
2. Use **backtracking** to generate subsets. At each recursive step, either include the current element or skip it.
3. If the current element is the same as the previous one and the previous one hasn't been included, skip the current element to avoid duplicates.

### Code Implementation:

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        # Sort the input array to handle duplicates
        nums.sort()
        result = []
        
        # Backtracking function to generate subsets
        def backtrack(start, current_subset):
            # Add the current subset to the result
            result.append(current_subset[:])
            
            # Iterate over the remaining elements
            for i in range(start, len(nums)):
                # Skip duplicates
                if i > start and nums[i] == nums[i - 1]:
                    continue
                
                # Include the current element and backtrack further
                current_subset.append(nums[i])
                backtrack(i + 1, current_subset)
                
                # Backtrack by removing the last element
                current_subset.pop()
        
        # Start backtracking with an empty subset
        backtrack(0, [])
        
        return result
```

### Explanation:
1. **Sorting**:
   - We first sort the input array `nums` to make sure that duplicates are adjacent. This helps in identifying duplicates easily when we are generating subsets.
   
2. **Backtracking Function**:
   - `backtrack(start, current_subset)` is the main function that generates all subsets:
     - `start` is the index from where we start considering elements.
     - `current_subset` is the subset we are currently building.
     - At each recursive call, the current subset is added to the `result`.
     - We iterate through the array from `start`, and for each element, we decide whether to include it in the current subset or skip it. If the element is the same as the previous one, we skip it to avoid duplicates.
   
3. **Avoiding Duplicates**:
   - The check `if i > start and nums[i] == nums[i - 1]: continue` ensures that we skip the current element if it’s the same as the previous one, unless it’s the first time we're encountering it in the current recursive branch.

### Example Walkthrough:

#### Example 1:
```python
Input: nums = [1, 2, 2]
```

1. Sort `nums` → `[1, 2, 2]`.
2. Start with an empty subset `[]`.
3. Include `1` → `[1]`, then explore subsets starting from the next index:
   - Include `2` → `[1, 2]`, then include the next `2` → `[1, 2, 2]`.
   - Backtrack by removing the last `2`, and then the first `2` → `[1]`.
4. Backtrack by removing `1` → `[]`, and explore subsets starting from `2`:
   - Include `2` → `[2]`, then include the next `2` → `[2, 2]`.
   - Backtrack to remove the last `2` and continue exploring.

The final result is:
```python
[[], [1], [1, 2], [1, 2, 2], [2], [2, 2]]
```

#### Example 2:
```python
Input: nums = [0]
```
There’s only one element, so the result is:
```python
[[], [0]]
```

### Time Complexity:
- Sorting the array takes \(O(n \log n)\), where \(n\) is the number of elements in the array.
- Generating all subsets takes \(O(2^n)\), as there are \(2^n\) possible subsets for an array of size \(n\). The time complexity of adding each subset to the result is proportional to the size of the subset, but the overall complexity is dominated by the number of subsets.

Thus, the overall time complexity is \(O(n \log n + 2^n)\).

### Space Complexity:
- The space complexity is \(O(2^n)\), where \(2^n\) is the number of possible subsets, as we need to store all the subsets in the result list.

### Conclusion:
This approach efficiently generates all unique subsets by using backtracking with a simple condition to skip duplicates. The solution explores all possible subsets while ensuring that no duplicate subsets are included.
