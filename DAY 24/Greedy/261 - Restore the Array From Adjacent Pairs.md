# [1743. Restore the Array From Adjacent Pairs](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs/description/)

To solve the problem of restoring the original array from its adjacent pairs, we can use a **graph-based approach**. Here's the thought process:

### Key Observations:
1. **Each number (element) in `nums` will appear exactly twice**, except for the two numbers that are at the start and end of the original array (they will appear only once). This is because every number in between must be adjacent to two other numbers.
2. **The problem forms a graph** where each element is a node, and an edge exists between two nodes if they are adjacent in the original array.

### Plan:
1. **Build an adjacency list**: We'll construct a dictionary where each key is a number, and its value is a list of numbers it is adjacent to. For each pair `[u, v]` in `adjacentPairs`, add `v` to `u`'s adjacency list and `u` to `v`'s adjacency list.
2. **Identify the start or end element**: The element at the start or the end of the array will have only one neighbor in the adjacency list (because it's only adjacent to one other number).
3. **Reconstruct the array**: Starting from a number with only one neighbor, we can reconstruct the array by following the adjacency relationships.

### Algorithm:
1. Create the adjacency list from the input `adjacentPairs`.
2. Find a number with exactly one adjacent number (this will be the start or end of the array).
3. Use a **depth-first search (DFS)** or **breadth-first search (BFS)** to traverse the graph, reconstructing the original array by visiting each node and its neighbors.

### Code Implementation:

```python
from collections import defaultdict, deque

class Solution:
    def restoreArray(self, adjacentPairs: List[List[int]]) -> List[int]:
        # Step 1: Build the adjacency list
        adj = defaultdict(list)
        for u, v in adjacentPairs:
            adj[u].append(v)
            adj[v].append(u)
        
        # Step 2: Find the starting element (it has only one adjacent number)
        start = None
        for key in adj:
            if len(adj[key]) == 1:
                start = key
                break
        
        # Step 3: Reconstruct the array using BFS/DFS
        # We'll use BFS here
        res = []
        visited = set()
        q = deque([start])  # Initialize the queue with the start element
        
        while q:
            node = q.popleft()
            res.append(node)
            visited.add(node)
            
            # Visit the neighbors
            for neighbor in adj[node]:
                if neighbor not in visited:
                    q.append(neighbor)
        
        return res

# Example Usage
solution = Solution()

# Test case 1
adjacentPairs = [[2,1],[3,4],[3,2]]
print(solution.restoreArray(adjacentPairs))  # Output: [1,2,3,4] or any valid variant

# Test case 2
adjacentPairs = [[4,-2],[1,4],[-3,1]]
print(solution.restoreArray(adjacentPairs))  # Output: [-2,4,1,-3] or any valid variant

# Test case 3
adjacentPairs = [[100000,-100000]]
print(solution.restoreArray(adjacentPairs))  # Output: [100000,-100000]
```

### Explanation of the Code:
1. **Adjacency List Construction**:
   - We use a `defaultdict(list)` to store the adjacency list. For each pair `[u, v]`, both `u` and `v` are made adjacent to each other.
   
2. **Finding the Starting Element**:
   - We identify the starting element by finding a key in the adjacency list that has only one adjacent element (i.e., `len(adj[key]) == 1`).

3. **Reconstructing the Array**:
   - We use **BFS** to traverse the graph starting from the identified start node. At each step, we visit all unvisited adjacent nodes and add them to the result list.

### Time Complexity:
- **O(n)**: Building the adjacency list takes O(n) time, as each edge (pair in `adjacentPairs`) is processed once. The BFS traversal also takes O(n) time, as it visits each node exactly once.

### Space Complexity:
- **O(n)**: The adjacency list takes O(n) space, and the BFS queue and visited set also take O(n) space in the worst case.

This solution is efficient and works within the problem's constraints.
