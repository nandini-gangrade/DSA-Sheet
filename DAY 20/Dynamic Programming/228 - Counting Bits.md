# [338. Counting Bits](https://leetcode.com/problems/counting-bits/description/)

To solve this problem efficiently, we need to count the number of 1's in the binary representation of every integer from 0 to `n`. The challenge is to achieve this in linear time, i.e., O(n).

### Observations:

1. **Bits Shifting:**
   - If you consider a number `i` and `i >> 1` (which is `i` divided by 2), the binary representation of `i >> 1` is simply the binary representation of `i` without its last bit.
   - For example, if `i = 5` (binary `101`), then `i >> 1` is `2` (binary `10`).

2. **Bit Count Relation:**
   - The number of 1's in `i` can be derived from the number of 1's in `i >> 1` plus the last bit of `i`.
   - Mathematically, `ans[i] = ans[i >> 1] + (i & 1)`.
   - Here, `(i & 1)` checks if the last bit of `i` is 1 (which means `i` is odd).

### Implementation:

Based on the above observations, we can build the solution by iterating from `0` to `n` and using the relation to calculate the number of 1's for each `i`.

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        # Initialize the array to store the results
        ans = [0] * (n + 1)
        
        # Compute the number of 1's for each number from 0 to n
        for i in range(1, n + 1):
            ans[i] = ans[i >> 1] + (i & 1)
        
        return ans
```

### Explanation:

- **Initialization:**
  - We start with an array `ans` of size `n + 1` initialized to zeros. This array will store the number of 1's for each index `i`.

- **Iteration and Calculation:**
  - We loop through all integers `i` from `1` to `n`.
  - For each `i`, we compute `ans[i]` using the relation `ans[i] = ans[i >> 1] + (i & 1)`, where `ans[i >> 1]` gives the number of 1's in the binary representation of `i // 2` and `(i & 1)` adds 1 if `i` is odd.

- **Return:**
  - Finally, the `ans` array is returned, containing the number of 1's for each index from `0` to `n`.

### Complexity:

- **Time Complexity:** O(n) - We process each number from `0` to `n` once.
- **Space Complexity:** O(n) - We use an array of size `n + 1` to store the results.

This solution is both efficient and elegant, leveraging the properties of binary numbers to achieve a linear-time solution.
