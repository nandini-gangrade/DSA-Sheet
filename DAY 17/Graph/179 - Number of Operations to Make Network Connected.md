# [1319. Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/description/)

To solve the problem of determining the minimum number of cable moves required to make all computers connected, we need to address a few key points:

1. **Connected Components Counting**: Determine the number of disconnected components in the network. Each disconnected component is essentially a subnetwork of computers that are connected internally but not to other subnetworks.

2. **Cable Check**: Verify if the number of available cables is sufficient to connect all the components. Specifically, to connect \( k \) disconnected components, we need at least \( k - 1 \) cables.

### Approach and Intuition

1. **Graph Representation**:
   - Use Union-Find (Disjoint Set Union, DSU) to keep track of the connected components in the network. This data structure helps efficiently determine and unite the components.

2. **Union-Find Operations**:
   - **Find**: Determine the root or representative of a component.
   - **Union**: Connect two components by merging their roots.

3. **Count Components**:
   - Traverse the connections and use Union-Find to unite the computers. Track the number of unique components at the end.

4. **Calculate the Result**:
   - If the number of connections is less than \( n - 1 \) (where \( n \) is the number of computers), it’s impossible to connect all computers, and return -1.
   - Otherwise, the minimum number of moves required is the number of disconnected components minus one.

### Complexity
- **Time Complexity**: \(O(n + E)\), where \(n\) is the number of computers and \(E\) is the number of connections. This is due to the union-find operations which are nearly linear with path compression and union by rank optimizations.
- **Space Complexity**: \(O(n)\), due to the storage required for the Union-Find structure.

### Code Implementation

Here’s how you can implement the solution in Python:

```python
class Solution:
    def makeConnected(self, n: int, connections: List[List[int]]) -> int:
        # Edge case: Not enough connections to even potentially connect all computers
        if len(connections) < n - 1:
            return -1

        # Union-Find (Disjoint Set Union) setup
        parent = list(range(n))
        rank = [0] * n

        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])  # Path compression
            return parent[x]

        def union(x, y):
            rootX = find(x)
            rootY = find(y)
            if rootX != rootY:
                # Union by rank
                if rank[rootX] > rank[rootY]:
                    parent[rootY] = rootX
                elif rank[rootX] < rank[rootY]:
                    parent[rootX] = rootY
                else:
                    parent[rootY] = rootX
                    rank[rootX] += 1
        
        # Apply union operations for each connection
        for u, v in connections:
            union(u, v)
        
        # Count unique components
        components = len(set(find(i) for i in range(n)))
        
        # Minimum moves required to connect all components
        return components - 1
```

### Explanation

1. **Union-Find Setup**:
   - Initialize parent and rank arrays for Union-Find operations.

2. **Union Operation**:
   - Use union operations for each given connection to unite the components.

3. **Count Components**:
   - After processing all connections, find the number of unique components.

4. **Result Calculation**:
   - If there are \( k \) components, at least \( k - 1 \) cables are needed to connect them all. 

This approach ensures that we efficiently determine the minimum number of moves required to make the entire network connected or detect if it's impossible.
