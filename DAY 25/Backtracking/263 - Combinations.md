# [77. Combinations](https://leetcode.com/problems/combinations/description/)

The problem asks for all possible combinations of `k` numbers chosen from the range `[1, n]`. This problem can be solved efficiently using a **backtracking** approach.

### Problem Breakdown:
1. **Input**:
   - An integer `n` representing the upper limit of the range.
   - An integer `k` representing how many numbers to choose from the range `[1, n]`.
2. **Output**:
   - A list of all combinations of `k` distinct numbers selected from `[1, n]`. Each combination must be unique, and the order within each combination doesn't matter.
   
### Key Points:
- You need to generate combinations, not permutations. That means the order of numbers doesn't matter, i.e., `[1, 2]` is the same as `[2, 1]`.
- The number of combinations can be computed using the formula \( C(n, k) = \frac{n!}{k!(n-k)!} \), but we need to find all combinations programmatically.

### Approach:
We will use **backtracking** to generate all valid combinations:
1. **Recursive Backtracking**:
   - Start from 1, recursively pick numbers.
   - For each recursive call, add a number to the current combination and reduce the number of remaining picks (`k`).
   - Once `k` becomes zero (i.e., we have picked enough numbers), we add the current combination to the result.
   - Ensure that each number is used only once by continuing the recursion from the next number onward.
2. **Pruning**:
   - We can prune unnecessary recursion by stopping early if the remaining numbers are insufficient to form a valid combination.
   
### Algorithm:
1. **Base case**: When the combination length reaches `k`, add it to the result.
2. **Recursive case**: Start from the current number, recursively explore the next numbers, and backtrack once a valid combination is found or invalid paths are pruned.

### Code Implementation:

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        # Result list to store all combinations
        result = []
        
        # Backtracking function to generate combinations
        def backtrack(start, current_combination):
            # If the current combination's length is k, add it to the result
            if len(current_combination) == k:
                result.append(current_combination[:])
                return
            
            # Iterate from 'start' to 'n', generating valid combinations
            for i in range(start, n + 1):
                # Add the current number to the combination
                current_combination.append(i)
                
                # Recursively explore further numbers
                backtrack(i + 1, current_combination)
                
                # Backtrack by removing the last added number
                current_combination.pop()
        
        # Start backtracking from 1 and an empty combination
        backtrack(1, [])
        
        return result
```

### Explanation:
1. **Initialization**: 
   - `result` is the list that will store all valid combinations.
   - The `backtrack` function is initialized to start generating combinations from `start = 1` and with an empty `current_combination`.
2. **Base Case**: 
   - When the length of `current_combination` equals `k`, the combination is complete, so it is added to the `result`.
3. **Recursive Case**:
   - For each number `i` from `start` to `n`, the function appends `i` to `current_combination` and recursively calls `backtrack(i + 1, current_combination)` to explore further numbers.
   - After exploring, the function removes the last element (backtracking) to try different possibilities.
4. **Termination**: The recursion terminates when all possible combinations of size `k` are explored.

### Time Complexity:
- The time complexity is \( O(C(n, k)) \), where \( C(n, k) \) is the number of ways to choose `k` numbers from `n`, i.e., \( \frac{n!}{k!(n-k)!} \).
- Since for each valid combination, we perform constant-time operations like appending and popping, the overall complexity is dominated by the number of valid combinations.

### Example Walkthrough:

#### Example 1:
```python
n = 4, k = 2
```

- Start with an empty combination and try each number from `1` to `4`.
- First, pick `1`, then recursively pick numbers greater than `1` to form combinations:
  - `[1, 2]`
  - `[1, 3]`
  - `[1, 4]`
- Next, backtrack and pick `2`:
  - `[2, 3]`
  - `[2, 4]`
- Finally, pick `3`:
  - `[3, 4]`

The result is:
```python
[[1, 2], [1, 3], [1, 4], [2, 3], [2, 4], [3, 4]]
```

#### Example 2:
```python
n = 1, k = 1
```

- The only possible combination is `[1]`, as there is only one number available.

The result is:
```python
[[1]]
```

### Conclusion:
The backtracking approach efficiently generates all combinations of `k` numbers chosen from `n`. By pruning unnecessary paths and ensuring combinations are built sequentially, this method explores all valid combinations while avoiding unnecessary computations.
