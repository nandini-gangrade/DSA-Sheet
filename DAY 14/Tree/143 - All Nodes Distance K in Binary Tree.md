# [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/description/)

To solve the problem of finding all nodes that are a distance `k` from a given target node in a binary tree, we can use a combination of depth-first search (DFS) to traverse the tree and a breadth-first search (BFS) to explore nodes at a specific distance. The approach involves converting the tree into an undirected graph, where edges can be traversed in both directions, allowing us to move upward from child to parent and vice versa.

### Approach

1. **Convert the Tree to a Graph**:
   - Use DFS to construct a graph representation of the tree, where each node points to its left, right, and parent nodes. This enables bidirectional traversal.

2. **Breadth-First Search (BFS)**:
   - Start a BFS from the target node to find all nodes at a distance `k`. 
   - Use a queue to track the current node and its distance from the target.
   - Maintain a visited set to avoid revisiting nodes.
   - If the current distance equals `k`, collect the node values.

3. **Return Results**:
   - Once the BFS completes, the nodes collected will be the ones at distance `k` from the target.

### Code Implementation

```python
from collections import defaultdict, deque

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int):
        # Step 1: Convert tree to graph using a map of adjacency lists
        graph = defaultdict(list)

        def build_graph(node, parent=None):
            if node is not None:
                if parent is not None:
                    graph[node.val].append(parent.val)
                    graph[parent.val].append(node.val)
                if node.left is not None:
                    build_graph(node.left, node)
                if node.right is not None:
                    build_graph(node.right, node)
        
        # Build the graph
        build_graph(root)

        # Step 2: BFS to find nodes at distance k from target
        queue = deque([(target.val, 0)])  # Start from target node with distance 0
        visited = set([target.val])
        result = []

        while queue:
            current, distance = queue.popleft()

            if distance == k:
                result.append(current)
            
            if distance > k:
                break

            # Check all adjacent nodes (children and parent)
            for neighbor in graph[current]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append((neighbor, distance + 1))
        
        return result

# Example usage
# Construct the tree as per the example
root = TreeNode(3)
root.left = TreeNode(5)
root.right = TreeNode(1)
root.left.left = TreeNode(6)
root.left.right = TreeNode(2)
root.right.left = TreeNode(0)
root.right.right = TreeNode(8)
root.left.right.left = TreeNode(7)
root.left.right.right = TreeNode(4)

target = root.left  # The target node with value 5
k = 2

solution = Solution()
output = solution.distanceK(root, target, k)
print(output)  # Output: [7, 4, 1]
```

### Explanation

- **Graph Construction**: The `build_graph` function constructs an undirected graph using an adjacency list where each node points to its left child, right child, and parent. This allows moving in both directions.
  
- **Breadth-First Search**: Starting from the target node, we explore its neighbors. For each neighbor not visited, we mark it as visited and add it to the queue with an incremented distance. Once we reach nodes with distance `k`, we collect their values.

- **Result**: The `result` list collects all nodes exactly `k` distance from the target node, which is returned at the end.

### Complexity

- **Time Complexity**: \(O(N)\), where \(N\) is the number of nodes in the tree. Each node and edge is visited once during the graph building and BFS traversal.
  
- **Space Complexity**: \(O(N)\), for the graph storage and BFS queue.

This solution efficiently finds all nodes at a specified distance from a target node by leveraging the tree's structure as a graph for bidirectional traversal.
