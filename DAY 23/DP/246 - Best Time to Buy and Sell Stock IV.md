# [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/)

To solve the problem of maximizing profit with at most `k` transactions, we need to use dynamic programming. The key challenge here is that we must optimize multiple transactions while ensuring that the buying and selling happen sequentially.

### Problem Breakdown:
1. **Multiple Transactions**: You can perform at most `k` transactions. A transaction consists of one buy and one sell operation.
2. **State Representation**: We need to track both the number of transactions made and whether we currently hold a stock or not.
3. **DP Transition**: For each day and each possible transaction, we need to decide whether we buy, sell, or hold based on maximizing profit.

### Edge Cases:
- If `k == 0` or `prices` has less than 2 entries, the maximum profit is 0.
- If `k >= len(prices) / 2`, we can simply calculate the maximum profit using as many transactions as needed (this is equivalent to the infinite transaction problem, as we can buy and sell whenever it’s profitable).

### Approach:
1. **Dynamic Programming**: We'll maintain a DP table `dp[t][i]`, where `t` is the number of transactions (from 0 to `k`), and `i` is the day (from 0 to `n-1`).
   - `dp[t][i]` represents the maximum profit achievable with exactly `t` transactions on day `i`.
2. **Recurrence Relation**:
   - For each transaction `t` on day `i`, we either:
     - Do nothing and keep the maximum profit from the previous day, i.e., `dp[t][i] = dp[t][i-1]`.
     - Or, we sell the stock today, meaning we must have bought the stock on a previous day `j < i`. We calculate this as `dp[t][i] = max(dp[t][i], prices[i] - prices[j] + dp[t-1][j])`.

### Optimized Version:
Instead of recalculating the previous maximum for each transaction from scratch, we maintain a running maximum (`max_diff`) for the best buying price that we can use for the current day.

### Code Implementation:

```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        n = len(prices)
        if n == 0 or k == 0:
            return 0
        
        # If k >= n // 2, we can perform unlimited transactions
        if k >= n // 2:
            return sum(max(prices[i] - prices[i - 1], 0) for i in range(1, n))
        
        # DP table: dp[t][i] means the max profit with at most t transactions by day i
        dp = [[0] * n for _ in range(k + 1)]
        
        for t in range(1, k + 1):
            max_diff = -prices[0]
            for i in range(1, n):
                # Update dp[t][i]: either we do nothing today, or we sell today
                dp[t][i] = max(dp[t][i - 1], prices[i] + max_diff)
                # Update max_diff: best profit we could have gotten from buying earlier
                max_diff = max(max_diff, dp[t - 1][i] - prices[i])
        
        # The answer is the maximum profit we can get with at most k transactions on the last day
        return dp[k][n - 1]
```

### Explanation:
1. **Base Cases**:
   - When `t == 0`, no transactions are made, so `dp[0][i] = 0` for all `i`.
   - When `i == 0`, there are no profits possible since the frog is on the first stone.
   
2. **Main DP Table Calculation**:
   - For each transaction `t` (from 1 to `k`), we maintain a running `max_diff` to keep track of the best day to buy a stock for the current transaction.
   - On each day `i`, we decide whether to:
     - Not sell the stock (i.e., the same profit as the previous day).
     - Sell the stock (i.e., `prices[i] + max_diff`).

3. **Edge Case Handling**:
   - If `k >= n // 2`, we can treat the problem as having unlimited transactions, and simply buy and sell on every profitable opportunity (i.e., when the price difference is positive).

### Complexity:
- **Time Complexity**: \(O(k \times n)\), where `k` is the number of transactions and `n` is the number of days. We fill out a DP table with `k+1` rows and `n` columns.
- **Space Complexity**: \(O(k \times n)\), as we are using a DP table of size \(k+1\) by \(n\).

### Example Walkthrough:

#### Example 1:
```python
k = 2
prices = [2, 4, 1]
```
- We buy at day 1 (price = 2) and sell at day 2 (price = 4), profit = \(4 - 2 = 2\).
- The answer is 2.

#### Example 2:
```python
k = 2
prices = [3, 2, 6, 5, 0, 3]
```
- Buy at day 2 (price = 2) and sell at day 3 (price = 6), profit = \(6 - 2 = 4\).
- Buy at day 5 (price = 0) and sell at day 6 (price = 3), profit = \(3 - 0 = 3\).
- Total profit = 4 + 3 = 7.
