# [526. Beautiful Arrangement](https://leetcode.com/problems/beautiful-arrangement/description/)

To solve the problem of counting the number of beautiful arrangements for a given integer \( n \), we can use a **backtracking** approach. The problem is essentially about generating all permutations of the numbers from 1 to \( n \) and counting those permutations that satisfy the given conditions.

### Key Concepts:

- A permutation \( perm \) is considered beautiful if for every position \( i \) (where \( 1 \leq i \leq n \)), either:
  1. \( perm[i] \) is divisible by \( i \), or
  2. \( i \) is divisible by \( perm[i] \).

### Approach:

1. **Backtracking**: We generate all possible permutations of the numbers from 1 to \( n \) and check each one to see if it is a beautiful arrangement.

2. **Recursive Exploration**: For each position \( i \), we attempt to place each number \( 1, 2, \ldots, n \) in that position, checking if the placement satisfies the conditions. If a placement is valid, we move to the next position.

3. **Pruning**: If at any step, a number can't be placed in a valid position, we backtrack (i.e., we undo the current placement and try the next possibility).

### Implementation:

Here's how we can implement this approach in Python:

```python
class Solution:
    def countArrangement(self, n: int) -> int:
        def count(i, X):
            if i == 1:
                return 1
            return sum(count(i - 1, X - {x}) for x in X if x % i == 0 or i % x == 0)
        
        return count(n, set(range(1, n + 1)))
```

### Explanation:

1. **Helper Function** `count(i, X)`:
   - `i`: The current position we are trying to fill.
   - `X`: The set of numbers that are still available to place in the permutation.

   The function recursively tries to fill position \( i \) with any number in \( X \) that satisfies the conditions. If it finds a valid number, it calls itself recursively to fill the next position with the remaining numbers.

2. **Base Case**:
   - When `i == 1`, it means we've successfully placed all numbers, so we return 1 as this represents a valid arrangement.

3. **Recursion**:
   - For each position \( i \), we sum up the results of valid placements (where the conditions are met) and return this sum as the total count of beautiful arrangements for the current configuration.

### Example Walkthrough:

#### Example 1:
```python
n = 2
```

- The valid permutations are `[1, 2]` and `[2, 1]`:
  - In `[1, 2]`: 1 is divisible by 1, and 2 is divisible by 2.
  - In `[2, 1]`: 2 is divisible by 1, and 1 is divisible by 2.
- So, the result is `2`.

#### Example 2:
```python
n = 1
```

- The only valid permutation is `[1]`.
- So, the result is `1`.

### Time Complexity:

- **Time Complexity**: The worst-case time complexity is \( O(n!) \), as we're essentially generating and checking all permutations. However, the pruning done by the conditions can reduce the number of permutations that need to be checked.

- **Space Complexity**: The space complexity is \( O(n) \) due to the recursion stack and the set used to track the remaining numbers.

### Conclusion:

The backtracking solution efficiently counts the number of beautiful arrangements by recursively attempting to build valid permutations, pruning invalid paths early, and summing up the valid configurations. This approach is feasible for the given constraint \( 1 \leq n \leq 15 \).
