# [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/description/)

        
To solve this problem of finding the sum of distances between each node and all other nodes in a tree, we can employ a two-pass depth-first search (DFS) strategy. This allows us to efficiently calculate the distances by leveraging the properties of trees and avoiding recalculations.

### Approach

1. **Tree Representation**:
   - Represent the tree using an adjacency list to facilitate traversal.

2. **First DFS (Post-order Traversal)**:
   - Compute the total distance from a root node (say node 0) to all other nodes.
   - Calculate the count of nodes in each subtree rooted at each node.
   - Use a post-order DFS to accumulate these values starting from the leaf nodes.

3. **Second DFS (Pre-order Traversal)**:
   - Adjust the calculated distances for all other nodes based on the previously computed values.
   - Use the relationship that moving the root to another node in the tree will affect the distances by reducing the contribution from its subtree and increasing the contribution from other parts of the tree.
   - Propagate the results using pre-order DFS.

### Intuition

- For a node \(i\), if you know the total sum of distances from its parent \(p\), you can compute its total distance sum by adjusting the parent's distance sum with respect to the number of nodes in \(i\)'s subtree.
- Specifically, when moving the root from a parent \(p\) to a child \(i\), the distance sum is updated as:
  \[
  \text{dist}(i) = \text{dist}(p) + (n - \text{count}[i]) - \text{count}[i]
  \]
  where \(\text{count}[i]\) is the number of nodes in the subtree rooted at \(i\).

### Implementation

```python
from collections import defaultdict

class Solution:
    def sumOfDistancesInTree(self, n, edges):
        # Create an adjacency list for the tree
        tree = defaultdict(list)
        for a, b in edges:
            tree[a].append(b)
            tree[b].append(a)
        
        # Initialize necessary data structures
        res = [0] * n       # Result array
        count = [1] * n     # Number of nodes in the subtree rooted at each node

        # First DFS: Post-order to calculate initial distances and subtree sizes
        def post_order(node, parent):
            for neighbor in tree[node]:
                if neighbor == parent:
                    continue
                post_order(neighbor, node)
                count[node] += count[neighbor]
                res[node] += res[neighbor] + count[neighbor]
        
        # Second DFS: Pre-order to adjust the distances based on the first DFS results
        def pre_order(node, parent):
            for neighbor in tree[node]:
                if neighbor == parent:
                    continue
                # Update result for neighbor using current node's result
                res[neighbor] = res[node] + (n - count[neighbor]) - count[neighbor]
                pre_order(neighbor, node)

        # Execute the DFS traversals
        post_order(0, -1)
        pre_order(0, -1)
        
        return res

# Example usage:
solution = Solution()
print(solution.sumOfDistancesInTree(6, [[0,1],[0,2],[2,3],[2,4],[2,5]]))  # Output: [8, 12, 6, 10, 10, 10]
```

### Explanation of Code

- **Adjacency List**: We construct an adjacency list to represent the tree for efficient traversal.
- **First DFS** (`post_order`):
  - Calculates the initial distances from the root node and the count of nodes in each subtree.
- **Second DFS** (`pre_order`):
  - Adjusts these distances for all nodes using the results of the first DFS, essentially "rotating" the root to each node.

### Complexity

- **Time Complexity**: \(O(n)\) since each node and edge is visited a constant number of times.
- **Space Complexity**: \(O(n)\) for storing the adjacency list, result array, and count array.

This solution efficiently computes the desired distances using properties of tree traversal and distance propagation.
