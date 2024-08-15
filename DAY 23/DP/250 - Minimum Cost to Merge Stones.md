# [1000. Minimum Cost to Merge Stones](https://leetcode.com/problems/minimum-cost-to-merge-stones/description/)

To solve the problem of merging stones, we need to approach it with dynamic programming. The main challenge is that we want to merge exactly `k` consecutive piles at each step, and we want to minimize the total cost incurred by these merges. Here's how we can break down the solution:

### Key Observations:

1. **Impossible Case**: 
   - If it is not possible to reduce the piles to exactly one pile, we should return `-1`. Specifically, merging exactly `k` piles reduces the number of piles by `k-1` each time. Thus, for it to be possible, the number of piles `(n - 1)` must be divisible by `(k - 1)`. If this condition doesn't hold, return `-1`.

2. **Merging Cost**:
   - Whenever we merge `k` consecutive piles, the cost is the sum of all stones in those piles.

3. **Dynamic Programming**:
   - We'll use a dynamic programming table `dp[i][j][m]` where:
     - `i` is the start index of the range of piles.
     - `j` is the end index of the range of piles.
     - `m` represents how many piles we want to reduce the range from `i` to `j`.
   - The goal is to merge all piles from `0` to `n-1` into exactly `1` pile, i.e., `dp[0][n-1][1]`.

4. **Cost Calculation**:
   - To calculate the cost for any range `i` to `j`, we need to find the sum of stones in that range.
   - If we reduce the range `i` to `j` to `k` piles, then the cost will depend on merging it to `k` piles and then merging those piles into one pile.

### Approach:

1. **DP Initialization**:
   - Initialize a 3D `dp` array where `dp[i][j][m]` is the minimum cost to merge piles from `i` to `j` into `m` piles.

2. **Recursive Transition**:
   - For each subarray of size `len`, and for each number of piles `m`, try merging at different possible midpoints and compute the cost recursively.

3. **Final Answer**:
   - The final answer will be stored in `dp[0][n-1][1]` if it's possible to merge into one pile. Otherwise, return `-1`.

### Code Implementation:

```python
class Solution:
    def mergeStones(self, stones: List[int], k: int) -> int:
        n = len(stones)
        if (n - 1) % (k - 1) != 0:
            return -1  # It's impossible to merge into one pile

        # Prefix sum to help calculate the sum of stones in any range
        prefix_sum = [0] * (n + 1)
        for i in range(n):
            prefix_sum[i + 1] = prefix_sum[i] + stones[i]

        # dp[i][j][m] means the minimum cost to merge stones[i:j+1] into m piles
        dp = [[[float('inf')] * (k + 1) for _ in range(n)] for _ in range(n)]

        # Base case: cost to merge a single pile is 0
        for i in range(n):
            dp[i][i][1] = 0

        # Solve for larger subarrays
        for length in range(2, n + 1):  # Subarray length
            for i in range(n - length + 1):  # Start of the subarray
                j = i + length - 1  # End of the subarray
                for m in range(2, k + 1):  # Number of piles to merge into
                    for mid in range(i, j, k - 1):
                        dp[i][j][m] = min(dp[i][j][m], dp[i][mid][1] + dp[mid + 1][j][m - 1])

                # Merge the entire subarray into 1 pile if possible
                if (j - i) % (k - 1) == 0:
                    dp[i][j][1] = dp[i][j][k] + (prefix_sum[j + 1] - prefix_sum[i])

        return dp[0][n - 1][1] if dp[0][n - 1][1] < float('inf') else -1
```

### Explanation of Code:

1. **Base Case Initialization**:
   - We initialize `dp[i][i][1] = 0` because no cost is needed to merge one pile.

2. **Prefix Sum**:
   - The `prefix_sum` array is used to calculate the sum of any subarray in constant time. `prefix_sum[i+1]` holds the sum of the first `i` stones, so the sum of the subarray from `i` to `j` is `prefix_sum[j+1] - prefix_sum[i]`.

3. **DP Table Update**:
   - For every subarray `stones[i:j+1]`, and for every possible number of piles `m`, we calculate the minimum cost by trying different midpoints `mid` to split the subarray into two parts, and merging them recursively.

4. **Final Merge**:
   - If the number of piles in the range `i` to `j` can be reduced to exactly `1` pile (i.e., `(j - i) % (k - 1) == 0`), we calculate the cost for this merge by summing up all the stones in the subarray.

5. **Result**:
   - Finally, the answer is stored in `dp[0][n-1][1]`. If it is `float('inf')`, that means it's impossible to merge all the piles, so we return `-1`.

### Example Walkthrough:

For the input `stones = [3,2,4,1]` and `k = 2`:
- We start with 4 piles.
- We merge `[3, 2]` for a cost of `5`, and we are left with `[5, 4, 1]`.
- We merge `[4, 1]` for a cost of `5`, and we are left with `[5, 5]`.
- We merge `[5, 5]` for a cost of `10`, and we are left with `[10]`.
- The total cost is `20`.

Thus, the output is `20`.

### Time Complexity:
- The time complexity is **O(n^3)** because we are iterating over all subarrays and considering every possible split and number of piles.

### Space Complexity:
- The space complexity is **O(n^3)** due to the 3D DP array used to store the results for every subarray and every possible number of piles.

This dynamic programming approach ensures that we efficiently compute the minimum cost to merge all piles into one pile, or determine if it's impossible.
