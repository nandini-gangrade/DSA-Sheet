# [Travelling Salesman Problem using Dynamic Programming](https://www.geeksforgeeks.org/travelling-salesman-problem-using-dynamic-programming/)

To solve the Traveling Salesman Problem (TSP) using Dynamic Programming with bitmasks, we can follow a structured approach that leverages the efficiency of bitmask operations to represent subsets of cities. The approach is suitable for a relatively small number of cities due to its exponential complexity in terms of the number of cities.

Here’s a step-by-step explanation and Python implementation of the TSP using the Dynamic Programming approach with bitmasks:

### Approach

1. **Problem Definition**:
   - Given `n` cities and a distance matrix where `dist[i][j]` represents the distance between city `i` and city `j`, find the shortest possible route that visits every city exactly once and returns to the starting point.

2. **State Definition**:
   - Let `dp[mask][i]` be the minimum cost to visit all cities in the subset represented by `mask`, ending at city `i`.
   - `mask` is a bitmask where each bit represents whether a city is included in the subset or not.

3. **Initial State**:
   - Start with `dp[1][0] = 0`, which means starting at city 0 with only city 0 visited.

4. **Transitions**:
   - For each subset of cities represented by `mask`, and for each ending city `i`, determine the minimum cost to reach city `i` from any other city `j` in the subset.

5. **Goal**:
   - Compute the minimum cost to visit all cities and return to the starting city.

### Python Implementation

```python
def tsp(n, dist):
    # Initialize the DP table
    INF = float('inf')
    dp = [[INF] * n for _ in range(1 << n)]
    dp[1][0] = 0  # Starting at city 0 with only city 0 visited
    
    # Iterate over all possible subsets
    for mask in range(1 << n):
        for i in range(n):
            if not (mask & (1 << i)):
                continue
            # Try to find the minimum cost to reach city i from any city j
            for j in range(n):
                if i == j or not (mask & (1 << j)):
                    continue
                dp[mask][i] = min(dp[mask][i], dp[mask ^ (1 << i)][j] + dist[j][i])
    
    # Reconstruct the shortest path cost to return to the start (city 0)
    min_cost = INF
    final_mask = (1 << n) - 1
    for i in range(1, n):
        min_cost = min(min_cost, dp[final_mask][i] + dist[i][0])
    
    return min_cost

# Example Usage
n = 4
dist = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]
print(tsp(n, dist))  # Output: 80
```

### Explanation

1. **Initialization**:
   - We initialize the `dp` table with `INF` to signify uncomputed states. The base case `dp[1][0] = 0` indicates that starting at city 0 with only city 0 visited has a cost of 0.

2. **Dynamic Programming Table Update**:
   - For each subset of cities (`mask`), and for each city `i` in the subset, we update `dp[mask][i]` by considering transitions from all other cities `j` in the subset.

3. **Final Computation**:
   - After filling the DP table, we compute the minimum cost to visit all cities and return to the starting city (city 0) by iterating over all possible ending cities.

### Time Complexity
- The time complexity is \(O(n^2 \cdot 2^n)\), where \(2^n\) represents the number of subsets, and \(n^2\) represents the number of state transitions.

### Space Complexity
- The space complexity is \(O(n \cdot 2^n)\) for storing the DP table.

This approach is feasible for \(n\) up to 20 or so, due to the exponential growth of the state space with respect to the number of cities.
