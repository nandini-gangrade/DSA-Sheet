# [264. Ugly Number II](https://leetcode.com/problems/ugly-number-ii/description/)

To find the `n`th ugly number, we can use a dynamic programming approach that efficiently generates ugly numbers in sequence.

### Approach:

1. **Dynamic Programming with Multiple Pointers**:
   - We maintain a list `dp` where `dp[i]` stores the `i`th ugly number.
   - Use three pointers, `p2`, `p3`, and `p5`, initialized to 0, which will point to the position in the `dp` array to multiply by 2, 3, and 5, respectively.
   - The next ugly number is the minimum of `dp[p2] * 2`, `dp[p3] * 3`, and `dp[p5] * 5`.
   - After determining the next ugly number, we increment the corresponding pointer(s).

2. **Initialization**:
   - The first ugly number is `1` because it's defined as the starting point.

3. **Iterate**:
   - We repeat the process until we've generated `n` ugly numbers.

### Python Implementation:

```python
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        dp = [0] * n  # Array to store the first n ugly numbers
        dp[0] = 1  # The first ugly number is 1
        
        p2 = p3 = p5 = 0  # Pointers for multiples of 2, 3, and 5
        
        for i in range(1, n):
            # Get the minimum value among the next possible candidates
            next_ugly = min(dp[p2] * 2, dp[p3] * 3, dp[p5] * 5)
            dp[i] = next_ugly
            
            # Increment pointers for the corresponding factor
            if next_ugly == dp[p2] * 2:
                p2 += 1
            if next_ugly == dp[p3] * 3:
                p3 += 1
            if next_ugly == dp[p5] * 5:
                p5 += 1
        
        return dp[-1]

# Example Usage:
sol = Solution()
print(sol.nthUglyNumber(10))  # Output: 12
print(sol.nthUglyNumber(1))   # Output: 1
```

### Explanation:

1. **Dynamic Programming Array (`dp`)**:
   - The array `dp` is used to store the ugly numbers sequentially.
   - `dp[0]` is initialized to `1`, as the first ugly number is `1`.

2. **Pointers (`p2`, `p3`, `p5`)**:
   - These pointers keep track of which element in `dp` to multiply by 2, 3, or 5 to generate the next possible ugly number.

3. **Generating the Next Ugly Number**:
   - The minimum value among `dp[p2] * 2`, `dp[p3] * 3`, and `dp[p5] * 5` is chosen as the next ugly number.
   - We then move the corresponding pointer(s) to ensure we only consider the next potential ugly number for that factor.

4. **Termination**:
   - The loop runs until we fill the `dp` array with `n` ugly numbers. The last element of `dp` will be the `n`th ugly number.

### Time Complexity:
- **Time Complexity**: \(O(n)\) since we compute each ugly number exactly once.
- **Space Complexity**: \(O(n)\) due to the storage of the `dp` array.

This approach efficiently computes the `n`th ugly number without generating and checking each integer, making it optimal for large values of `n`.
