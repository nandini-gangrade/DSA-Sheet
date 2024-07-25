# 122. Best Time to Buy and Sell Stock II.md
[Leetcode Solution](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/solutions/5535198/best-solution-challenge-day-2-revisewitharsh/)

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the \(i^{th}\) day. You may decide to buy and/or sell the stock on each day. You can only hold at most one share of the stock at any time, but you can buy and then immediately sell it on the same day. Find and return the maximum profit you can achieve.

### Examples

**Example 1:**

- **Input:** `prices = [7,1,5,3,6,4]`
- **Output:** `7`
- **Explanation:** 
  - Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
  - Buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
  - Total profit is 4 + 3 = 7.

**Example 2:**

- **Input:** `prices = [1,2,3,4,5]`
- **Output:** `4`
- **Explanation:** 
  - Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
  - Total profit is 4.

**Example 3:**

- **Input:** `prices = [7,6,4,3,1]`
- **Output:** `0`
- **Explanation:** There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.

### Constraints

- \(1 \leq \text{prices.length} \leq 3 \times 10^4\)
- \(0 \leq \text{prices}[i] \leq 10^4\)

## Intuition

The main idea is to capture profit whenever there's an increase in the stock price from one day to the next. This is because each increase can be thought of as a potential profit if you had bought at the lower price and sold at the higher price. By accumulating these profits, you can achieve the maximum profit possible.

## Approach

1. **Initialize a variable `profit` to 0**: This will store the total profit accumulated over time.
   
2. **Iterate over the array `prices` from the first to the last day**:
   - For each day \(i\), check if the price on the next day \((i+1)\) is greater than the current day \(i\).
   - If `prices[i+1] > prices[i]`, calculate the difference and add it to `profit`.
   - This difference represents a profitable transaction where you buy on day \(i\) and sell on day \(i+1\).

3. **Return the accumulated `profit`**: This will be the maximum profit possible with the given transactions.

## Code

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0  # Initialize profit to zero
        
        # Loop through the prices array
        for i in range(len(prices) - 1):
            # If the next day's price is greater than the current day's price
            if prices[i + 1] > prices[i]:
                # Add the difference to profit
                profit += prices[i + 1] - prices[i]
        
        return profit  # Return the total profit
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm makes a single pass through the prices array, where \(n\) is the number of days, resulting in linear time complexity.

- **Space Complexity:** \(O(1)\)  
  The algorithm uses a fixed amount of extra space to store the profit variable, which is constant.

This solution efficiently calculates the maximum profit by leveraging the opportunity to profit from each increase in stock price from one day to the next.
