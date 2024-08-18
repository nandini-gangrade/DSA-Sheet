# [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)

To solve the problem of finding all unique combinations of candidate numbers that sum up to the given target, where each number can only be used once, we can utilize **backtracking**. This approach helps explore all possible combinations, and we can ensure uniqueness by sorting and skipping duplicates.

### Problem Breakdown:
1. **Candidate numbers**: You are given a list of candidate numbers, and each number can be used at most once.
2. **Target sum**: You need to find all the combinations that sum to the target.
3. **Unique combinations**: The combinations should not contain duplicates. This means that even if the same number appears multiple times in the input, we must ensure that only distinct sets of numbers are returned.

### Approach:
1. **Sort the array**: By sorting the candidate numbers, we can easily handle duplicate elements. This allows us to skip repeated numbers and avoid generating duplicate combinations.
2. **Backtracking**: We explore combinations recursively:
   - If the current combination's sum exceeds the target, we backtrack.
   - If the sum equals the target, we add that combination to the result.
   - We continue exploring possible combinations by iterating over the remaining candidates.
3. **Avoid duplicates**: After sorting the candidates, if a number is the same as the previous one and hasn’t been used, we skip it to avoid duplicates in the result.

### Detailed Steps:
1. **Sort** the `candidates` to help manage duplicates.
2. Define a **backtracking function** that:
   - Takes the current index, the remaining target sum, and the current combination of numbers.
   - Recursively tries each number from the current index onwards.
   - Skips over duplicates to avoid redundant combinations.
3. Once the target is reached, add the current combination to the result.
4. If the target is exceeded, stop the recursion (backtrack).

### Code Implementation:

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        # Sort the candidates to handle duplicates easily
        candidates.sort()
        
        # This will hold the final unique combinations
        result = []
        
        # Backtracking function to find combinations
        def backtrack(start, target, path):
            # If we reach the target, add the current path to the result
            if target == 0:
                result.append(path)
                return
            # If the target is negative, we stop exploring
            if target < 0:
                return
            
            # Explore each number starting from the current index
            for i in range(start, len(candidates)):
                # Skip duplicates to avoid redundant combinations
                if i > start and candidates[i] == candidates[i - 1]:
                    continue
                
                # Include the current number and recursively explore
                backtrack(i + 1, target - candidates[i], path + [candidates[i]])
        
        # Start the backtracking process
        backtrack(0, target, [])
        
        return result
```

### Explanation of the Code:
1. **Sorting**: 
   - The candidates are sorted to ensure that we can easily skip duplicates.
2. **Backtracking**:
   - The `backtrack` function is called with the starting index, remaining target, and the current path (combination of numbers).
   - For each call, if the target becomes `0`, it means we’ve found a valid combination, and it is added to the result.
   - If the target becomes negative, we stop further exploration (backtrack).
   - For each index, if the current number is the same as the previous one (and it's not the first iteration for that number), we skip that number to prevent duplicate combinations.
3. **Avoiding Duplicates**:
   - The condition `if i > start and candidates[i] == candidates[i - 1]` ensures that we skip numbers that have already been considered at the current level of recursion.

### Time Complexity:
- Sorting the candidates takes \(O(n \log n)\), where \(n\) is the length of the `candidates` array.
- The backtracking process explores all possible subsets of the array, but due to pruning (skipping duplicates), the complexity is reduced compared to exploring every subset.
  Therefore, the overall complexity is approximately \(O(2^n)\) in the worst case, with the additional cost of checking uniqueness.

### Example Walkthrough:

#### Example 1:
```python
candidates = [10,1,2,7,6,1,5]
target = 8
```

1. **Sort the candidates**: `[1,1,2,5,6,7,10]`
2. **Backtracking process**:
   - Start from index `0` with the first `1`, subtract it from the target, and continue. The target becomes `7`.
   - Include the next `1` and subtract, making the target `6`. Continue with `6`, and the combination `[1,1,6]` reaches the target. Add it to the result.
   - Continue exploring other combinations like `[1,2,5]` and `[2,6]`.
   - Skip duplicates and backtrack to explore other paths like `[1,7]`.

The final result is:
```python
[
 [1, 1, 6],
 [1, 2, 5],
 [1, 7],
 [2, 6]
]
```

#### Example 2:
```python
candidates = [2,5,2,1,2]
target = 5
```

1. **Sort the candidates**: `[1,2,2,2,5]`
2. **Backtracking**:
   - Explore combinations starting with `1`, then `2` and `2`, reaching the target `5`. Skip duplicates.
   - Include only `5` to reach the target.

The result is:
```python
[
 [1, 2, 2],
 [5]
]
```

### Conclusion:
The backtracking approach efficiently explores all possible combinations and avoids duplicates by sorting and skipping repeated elements. This ensures that we generate only unique combinations that sum up to the target.
