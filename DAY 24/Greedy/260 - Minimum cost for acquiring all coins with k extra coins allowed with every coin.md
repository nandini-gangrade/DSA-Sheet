# [Minimum cost for acquiring all coins with k extra coins allowed with every coin](https://www.geeksforgeeks.org/minimum-cost-for-acquiring-all-coins-with-k-extra-coins-allowed-with-every-coin/)

This problem can be solved using a **greedy approach** where we acquire the coins in an optimal way by minimizing the cost. The main idea is to pay for the smallest coins, and with each paid coin, pick additional `K` coins for free.

### Steps to Solve:
1. **Sort the coins**: Sort the array in increasing order, because it's always optimal to pick the smallest coin to minimize the cost.
2. **Pay for the fewest coins possible**: Every time you pay for one coin, you can take `K` additional coins for free. Thus, in each "transaction," you can acquire up to `K + 1` coins (the coin you pay for plus `K` free coins).
3. **Calculate the minimum number of transactions**: To acquire all `N` coins, you need to make `ceil(N / (K + 1))` transactions.
4. **Sum up the cost of those transactions**: The total cost will be the sum of the smallest `ceil(N / (K + 1))` coins after sorting.

### Algorithm:
1. Sort the array of coins.
2. Find the number of transactions needed: `ceil(N / (K + 1))`.
3. Sum the smallest `ceil(N / (K + 1))` coins to get the minimum cost.

### Code Implementation:

```python
import math

def min_cost_to_acquire_coins(coin, k):
    # Step 1: Sort the coins in ascending order
    coin.sort()
    
    # Step 2: Calculate the number of coins we actually need to pay for
    n = len(coin)
    num_to_pay = math.ceil(n / (k + 1))
    
    # Step 3: Sum the smallest 'num_to_pay' coins
    min_cost = sum(coin[i] for i in range(num_to_pay))
    
    return min_cost

# Example 1
coin1 = [100, 20, 50, 10, 2, 5]
k1 = 3
print(min_cost_to_acquire_coins(coin1, k1))  # Output: 7

# Example 2
coin2 = [1, 2, 5, 10, 20, 50]
k2 = 3
print(min_cost_to_acquire_coins(coin2, k2))  # Output: 3
```

### Explanation:

1. **Sort the coins**: Sorting helps us prioritize paying for the smallest coins to minimize the total cost.
2. **Determine how many coins to pay for**: Since you can acquire `K + 1` coins in each transaction, you only need to pay for `ceil(N / (K + 1))` coins.
3. **Sum the smallest coins**: After sorting, the smallest coins will be at the beginning of the array, so we sum the first `ceil(N / (K + 1))` coins.

### Example Walkthrough:

#### Example 1:
Input: `coin = [100, 20, 50, 10, 2, 5], k = 3`
- After sorting: `coin = [2, 5, 10, 20, 50, 100]`
- We can pick `ceil(6 / (3 + 1)) = ceil(6 / 4) = 2` coins (the smallest 2 coins).
- Minimum cost = `2 + 5 = 7`.

#### Example 2:
Input: `coin = [1, 2, 5, 10, 20, 50], k = 3`
- After sorting: `coin = [1, 2, 5, 10, 20, 50]`
- We can pick `ceil(6 / (3 + 1)) = ceil(6 / 4) = 2` coins (the smallest 2 coins).
- Minimum cost = `1 + 2 = 3`.

### Time Complexity:
- Sorting the coins takes **O(n log n)** time.
- Summing the smallest `ceil(n / (K + 1))` coins takes **O(n)** time.
Thus, the overall time complexity is **O(n log n)** due to sorting.

### Space Complexity:
- The space complexity is **O(1)** if sorting is done in place, or **O(n)** if sorting creates a new array.
