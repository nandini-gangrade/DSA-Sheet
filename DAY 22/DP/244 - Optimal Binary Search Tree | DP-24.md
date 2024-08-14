# [Optimal Binary Search Tree | DP-24](https://www.geeksforgeeks.org/optimal-binary-search-tree-dp-24/)

The **Optimal Binary Search Tree (OBST)** problem is a classical problem in dynamic programming where we aim to construct a binary search tree that minimizes the expected search cost, given that each node has an associated probability (or frequency) of being searched.

### Problem Explanation:

Given a sorted array of keys and an array of frequencies representing the probability of searching each key, the task is to construct a Binary Search Tree (BST) that minimizes the expected search cost. The search cost for a node in the BST is calculated by multiplying the level of the node by its frequency. The goal is to build a tree where the total search cost is minimized.

### Dynamic Programming Approach:

The key observation is that the cost of searching for a key depends on its level in the tree. Therefore, we need to construct a tree that minimizes this cost, while keeping the search properties of a BST intact (i.e., left subtree contains smaller keys and right subtree contains larger keys).

#### Recursive Relation:

Let `optCost(i, j)` represent the minimum cost of constructing a BST with keys `i` to `j`.

The recursive formula to calculate `optCost(i, j)` is as follows:

\[
\text{optCost}(i, j) = \sum_{k=i}^{j} \text{freq}[k] + \min_{r=i}^{j} \left( \text{optCost}(i, r-1) + \text{optCost}(r+1, j) \right)
\]

Here:
- The first term `\sum_{k=i}^{j} \text{freq}[k]` represents the total frequency of all the keys from `i` to `j`, as these keys will be part of the subtree rooted between `i` and `j`.
- The second term represents the minimum cost of constructing subtrees for each possible root `r` in the range `[i, j]`.

#### Steps to Solve:

1. **Base Case**: If `i > j`, i.e., there are no keys, the cost is 0. Similarly, if `i == j`, the cost is simply `freq[i]`, as the only node is the root at level 1.
2. **Optimal Substructure**: For each possible root `r` between `i` and `j`, calculate the total cost of the tree with `r` as the root and recursively calculate the cost of the left and right subtrees.
3. **Memoization**: Use a table to store the minimum cost for each range `[i, j]` to avoid recalculating it multiple times.

### Solution Code:

Here's the dynamic programming solution in Python to construct the Optimal Binary Search Tree:

```python
def optimal_bst(keys, freq, n):
    # Create a table to store results of subproblems
    cost = [[0 for x in range(n)] for y in range(n)]

    # Base case: Single keys (i.e., i == j)
    for i in range(n):
        cost[i][i] = freq[i]

    # Now, calculate the optimal cost for larger subarrays (i.e., length > 1)
    for length in range(2, n + 1):  # length of the subarray
        for i in range(n - length + 1):
            j = i + length - 1  # End index of the subarray

            # Initialize cost[i][j] as infinity
            cost[i][j] = float('inf')

            # Sum of frequencies from i to j
            total_freq = sum(freq[i:j+1])

            # Try making each key in the range keys[i..j] as the root
            for r in range(i, j + 1):
                # Calculate cost when keys[r] is root
                left_cost = cost[i][r - 1] if r > i else 0
                right_cost = cost[r + 1][j] if r < j else 0
                total_cost = left_cost + right_cost + total_freq

                # Update the minimum cost
                cost[i][j] = min(cost[i][j], total_cost)

    # The result is in cost[0][n-1]
    return cost[0][n-1]


# Example usage
keys = [10, 12, 20]
freq = [34, 8, 50]
n = len(keys)
print("Cost of Optimal BST is", optimal_bst(keys, freq, n))
```

### Explanation of Code:

- **Base Case**: We initialize the cost of single-key trees (i.e., `cost[i][i]`) to be the frequency of that key, as it will be the root of its own tree.
- **Dynamic Programming Table**: We use a 2D table `cost` where `cost[i][j]` stores the minimum cost of constructing a BST with keys `i` to `j`.
- **Loop Structure**: We build the table for subarrays of increasing lengths (from 2 to `n`), calculating the cost for each subarray `[i, j]`.
- **Optimal Substructure**: For each subarray, we consider every key `r` in that range as the root and calculate the cost of the left and right subtrees. The total cost also includes the sum of frequencies of keys in the subarray.

### Example:

For the input:

```python
keys = [10, 12, 20]
freq = [34, 8, 50]
```

Possible BSTs and their costs are:

- Tree I: `10` as root → Cost = 142
- Tree II: `12` as root → Cost = 142
- Tree III: `20` as root → Cost = 182

The minimum cost is 142, and that is the result.

### Time Complexity:

The time complexity of this dynamic programming approach is \(O(n^3)\) because:
- We have to calculate the cost for all subarrays of increasing lengths (which is \(O(n^2)\)).
- For each subarray, we are calculating the sum of frequencies and trying every possible root (which takes \(O(n)\) time).

With optimizations, the time complexity can be reduced to \(O(n^2)\), but the given solution works well for moderate input sizes.
