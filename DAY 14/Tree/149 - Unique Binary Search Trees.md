# [96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/description/)

It looks like you encountered an `AttributeError` because the `numTrees` method isn't defined or accessible in the `Solution` class. Here's a solution to ensure the `numTrees` method is properly defined and accessible:

### Code Explanation

The `numTrees` method calculates the number of unique binary search trees (BSTs) that can be constructed with `n` distinct nodes. This is done using a dynamic programming approach where the number of unique BSTs for a given `n` is computed based on previously computed results for smaller values.

### Code Implementation

Here is the corrected implementation of the `numTrees` method within the `Solution` class:

```python
class Solution:
    def numTrees(self, n: int) -> int:
        # Initialize a DP array where dp[i] will store the number of unique BSTs with i nodes
        dp = [0] * (n + 1)
        dp[0] = 1  # Base case: An empty tree is considered a valid BST
        dp[1] = 1  # Base case: A single node tree is a valid BST

        # Fill the dp array using the results of smaller subproblems
        for i in range(2, n + 1):
            for j in range(1, i + 1):
                dp[i] += dp[j - 1] * dp[i - j]

        return dp[n]

# Example usage:
solution = Solution()
print(solution.numTrees(3))  # Output: 5
```

### Explanation

1. **Initialization**:
   - `dp[0] = 1`: There's exactly one way to arrange an empty tree.
   - `dp[1] = 1`: There's exactly one way to arrange a tree with a single node.

2. **Dynamic Programming Transition**:
   - For each number of nodes `i` from 2 to `n`, calculate the number of unique BSTs by considering each node `j` as the root and combining the number of unique BSTs that can be formed with nodes to the left and right of `j`.

3. **Time Complexity**:
   - **O(n^2)**: The nested loop structure results in a quadratic time complexity due to the double iteration over `i` and `j`.

4. **Space Complexity**:
   - **O(n)**: The space used by the `dp` array to store results for each value from 0 to `n`.

This method ensures that `numTrees` is correctly defined and can be called on an instance of the `Solution` class, avoiding the `AttributeError` you encountered.
