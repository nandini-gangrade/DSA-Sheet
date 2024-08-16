# [887. Super Egg Drop](https://leetcode.com/problems/super-egg-drop/description/)

The problem of determining the minimum number of moves to find the critical floor `f` in an `n`-floor building with `k` eggs is a classic dynamic programming challenge. It requires efficiently managing the eggs to minimize the worst-case number of moves needed to determine the exact critical floor.

### Key Observations:
- If you have only 1 egg, you must try every floor from the bottom up to avoid breaking the egg prematurely. This requires `n` moves in the worst case (linear search).
- If you have infinite eggs, you can perform a binary search to determine the critical floor in `log(n)` moves by halving the search space each time.

However, with limited eggs and a large number of floors, we need to carefully choose a strategy that minimizes the number of moves in the worst case, given that an egg may break and reduce our number of available eggs.

### Dynamic Programming Approach:

We can use dynamic programming to build a table where each entry `dp[k][n]` represents the minimum number of moves needed to find the critical floor when we have `k` eggs and `n` floors.

#### Key Recurrence Relation:

- If we drop an egg from the `x`-th floor:
  1. **If it breaks**, we reduce the problem to determining the critical floor in the floors below (`x - 1`) with one fewer egg (`k - 1`).
  2. **If it doesn’t break**, we reduce the problem to the floors above (`n - x`) with the same number of eggs (`k`).

Thus, the number of moves required in the worst case is:
\[
dp[k][n] = 1 + \min_{x=1}^{n} (\max(dp[k-1][x-1], dp[k][n-x]))
\]
We take the minimum over all possible `x` (the floor where we drop the egg), and in each case, we take the maximum of the two possible outcomes (either the egg breaks or it doesn’t).

### Optimized Approach:

Instead of iterating over every floor `x`, we can optimize using a different perspective. We look at the problem as determining how many floors we can check with a given number of moves.

Let `dp[m][k]` represent the maximum number of floors we can check with `m` moves and `k` eggs. If we make a move:
- **If the egg breaks**, we have `k - 1` eggs and `m - 1` moves left to check the lower floors.
- **If the egg doesn’t break**, we have `k` eggs and `m - 1` moves left to check the upper floors.

Thus, the recurrence relation becomes:
\[
dp[m][k] = dp[m-1][k-1] + dp[m-1][k] + 1
\]
This formula counts:
1. `dp[m-1][k-1]`: the floors we can check if the egg breaks.
2. `dp[m-1][k]`: the floors we can check if the egg doesn’t break.
3. `+1`: the current floor we are testing.

We are looking for the smallest `m` such that `dp[m][k] >= n`, i.e., we can check all `n` floors with `k` eggs in `m` moves.

### Algorithm:

```python
class Solution:
    def superEggDrop(self, k: int, n: int) -> int:
        # dp[m][k] will hold the maximum number of floors we can check with m moves and k eggs
        dp = [[0] * (k + 1) for _ in range(n + 1)]
        
        m = 0
        # Increment the number of moves until we can check at least n floors
        while dp[m][k] < n:
            m += 1
            for eggs in range(1, k + 1):
                dp[m][eggs] = dp[m - 1][eggs - 1] + dp[m - 1][eggs] + 1
        
        return m
```

### Explanation:

1. **Dynamic Programming Table**:
   - `dp[m][eggs]` holds the maximum number of floors that can be checked with `m` moves and `eggs` eggs.
   
2. **Moves Calculation**:
   - For each move `m`, we calculate the number of floors we can check with every number of eggs from `1` to `k`.
   
3. **Termination Condition**:
   - We stop when the maximum number of floors we can check (`dp[m][k]`) is greater than or equal to `n`, meaning we have enough moves to check all `n` floors.

### Time Complexity:
- The time complexity is \(O(k \times m)\), where `m` is the number of moves required, and `k` is the number of eggs. Since `m` is generally much smaller than `n`, this solution is efficient for large values of `n`.

### Example Walkthrough:

For the input `k = 2`, `n = 6`:

- After 1 move, we can only check 1 floor.
- After 2 moves, we can check up to 3 floors.
- After 3 moves, we can check all 6 floors.

Thus, the minimum number of moves required is 3.

### Example:

```python
k = 2
n = 6
solution = Solution()
print(solution.superEggDrop(k, n))  # Output: 3
```

### Explanation of Example:

With 2 eggs and 6 floors:
- We use the first egg strategically, dropping it from floors to minimize the worst case.
- By the third move, we can guarantee that we find the critical floor with a minimum number of moves.

Thus, the answer is 3 moves.
