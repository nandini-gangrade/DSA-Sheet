# [322. Coin Change](https://leetcode.com/problems/coin-change/description/)

To solve the problem of finding the minimum number of coins needed to make up a given amount, you can use a dynamic programming approach. Here's a step-by-step breakdown:

### Approach:

1. **Define the DP Array**:
   - Let `dp[i]` represent the minimum number of coins needed to make up the amount `i`.
   - Initialize a `dp` array of size `amount + 1` with a large value (infinity), which represents that initially, it's impossible to reach that amount. Set `dp[0] = 0` because zero coins are needed to make the amount `0`.

2. **Transition**:
   - For each coin in `coins`, update the `dp` array. For each amount `i` from `coin` to `amount`, check if using the current coin reduces the number of coins needed for the amount `i`. The update rule is:
     - `dp[i] = min(dp[i], dp[i - coin] + 1)`
   - This checks if the current coin can be used to reach the amount `i`, by adding one coin to the solution for the amount `i - coin`.

3. **Final Answer**:
   - After processing all coins, `dp[amount]` will contain the minimum number of coins needed to make up the given `amount`.
   - If `dp[amount]` is still a large value (infinity), return `-1`, indicating that it's impossible to make the amount with the given coins.

### Code Implementation:

Here’s the implementation in Python:

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        # Initialize dp array with a large value (infinity)
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        
        # Fill the dp array
        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] = min(dp[i], dp[i - coin] + 1)
        
        # If dp[amount] is still infinity, return -1; otherwise, return dp[amount]
        return dp[amount] if dp[amount] != float('inf') else -1
```

### Example Explanation:

1. **Example 1**:
   - Input: `coins = [1,2,5]`, `amount = 11`
   - The optimal solution is to use 2 coins of `5` and 1 coin of `1`, resulting in a total of 3 coins.
   - Output: `3`

2. **Example 2**:
   - Input: `coins = [2]`, `amount = 3`
   - It's impossible to make `3` using only coins of `2`, so the output is `-1`.

3. **Example 3**:
   - Input: `coins = [1]`, `amount = 0`
   - No coins are needed to make an amount of `0`, so the output is `0`.

### Complexity Analysis:

- **Time Complexity**: O(n * m), where `n` is the `amount` and `m` is the number of coins. Each amount is computed in terms of the available coins.
- **Space Complexity**: O(n), for storing the `dp` array.

This solution is efficient and works well within the problem's constraints, providing the minimum number of coins needed to make up the given amount.
