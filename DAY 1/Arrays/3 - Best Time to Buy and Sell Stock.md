# [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

Given an array `prices` where `prices[i]` represents the price of a stock on the ith day, maximize your profit by:
- Choosing one day to buy one stock.
- Choosing a different day in the future to sell that stock.

**Return the maximum profit you can achieve from this transaction. If no profit can be achieved, return 0.**

**Example 1:**
- **Input:** `prices = [7,1,5,3,6,4]`
- **Output:** `5`
  - Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6). Profit = 6 - 1 = 5.

**Example 2:**
- **Input:** `prices = [7,6,4,3,1]`
- **Output:** `0`
  - Explanation: In this case, no transactions are done and the max profit = 0.

## Intuition

To maximize profit, you need to:
- **Buy Low:** Identify the lowest price you can buy the stock for.
- **Sell High:** Sell the stock at a higher price after the buying day to maximize the difference.

The goal is to find the highest profit by selecting the best days to buy and sell, where you must buy before you sell.

## Approach

1. **Initialization:**
   - Use `min_price` to track the lowest price encountered as you iterate through the list.
   - Use `max_profit` to track the highest profit possible with the given prices.

2. **Iterate Through the Array:**
   - For each price in the array:
     - Update `min_price` to ensure it always holds the lowest price found so far.
     - Compute the potential profit if you were to sell at the current price.
     - Update `max_profit` if the computed profit exceeds the current `max_profit`.

3. **Return Result:**
   - At the end of the iteration, `max_profit` holds the maximum profit achievable.

## Code

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf')  # Initialize min_price to a very high value
        max_profit = 0  # Initialize max_profit to 0
        
        for price in prices:
            if price < min_price:
                min_price = price  # Update min_price if current price is lower
            profit = price - min_price  # Calculate profit if selling today
            if profit > max_profit:
                max_profit = profit  # Update max_profit if current profit is higher
        
        return max_profit
```

## Explanation

1. **Initialization:**
   - `min_price` starts as infinity, ensuring any price encountered will be lower initially.
   - `max_profit` starts at 0 because no transactions have been made yet.

2. **Processing Prices:**
   - As you iterate through each price:
     - Update `min_price` if the current price is lower than the previously recorded `min_price`.
     - Calculate the profit for the current price if you were to sell on that day.
     - Update `max_profit` if this profit is greater than the previously recorded `max_profit`.

3. **Return Result:**
   - Return the value of `max_profit`, which is the maximum profit achievable with the given prices.

## Complexity

- **Time Complexity:** O(n)  
  We traverse the list of prices once.

- **Space Complexity:** O(1)  
  We use a constant amount of extra space.

This approach efficiently calculates the maximum profit by iterating through the list of prices a single time and updating the necessary variables.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/solutions/5524972/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
