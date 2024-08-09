# [1376. Time Needed to Inform All Employees](https://leetcode.com/problems/time-needed-to-inform-all-employees/description/)

To solve this problem, we need to determine the time required for the head of the company to inform all employees about the urgent news. We can represent the employee-manager relationships as a tree structure, where the head is the root node. Each node has a weight representing the time required to inform its direct subordinates. We need to calculate the longest path from the head to any leaf node (an employee without subordinates) in this tree, which will give us the total time needed to inform all employees.

### Approach

1. **Build an Adjacency List:**
   - Create an adjacency list to represent the tree. Each employee will have a list of direct subordinates.

2. **Depth-First Search (DFS):**
   - Perform a DFS starting from the head of the company. For each employee, calculate the time required to inform all subordinates recursively.
   - For each employee, the total time needed to inform all their subordinates is the inform time of that employee plus the maximum time required by any of their subordinates to inform their subordinates.

3. **Base Case:**
   - If an employee has no subordinates, the time required to inform all subordinates is zero.

### Complexity

- **Time Complexity:** \(O(n)\), where \(n\) is the number of employees, because each employee and their subordinates are visited once.
- **Space Complexity:** \(O(n)\) for storing the adjacency list and the recursive call stack.

### Code Implementation

Here's the Python code implementing the above approach:

```python
from typing import List

class Solution:
    def numOfMinutes(self, n: int, headID: int, manager: List[int], informTime: List[int]) -> int:
        # Step 1: Build the adjacency list
        adj = [[] for _ in range(n)]
        for emp in range(n):
            if manager[emp] != -1:
                adj[manager[emp]].append(emp)
        
        # Step 2: DFS function to calculate the time needed
        def dfs(emp: int) -> int:
            # Base case: if no subordinates, return 0
            if not adj[emp]:
                return 0
            
            max_time = 0
            # Check time for all subordinates
            for sub in adj[emp]:
                max_time = max(max_time, dfs(sub))
            
            # Total time is own inform time + maximum time among subordinates
            return informTime[emp] + max_time
        
        # Step 3: Start DFS from the head of the company
        return dfs(headID)

# Example usage
solution = Solution()
print(solution.numOfMinutes(6, 2, [2, 2, -1, 2, 2, 2], [0, 0, 1, 0, 0, 0]))  # Output: 1
```

### Explanation of the Code

- **Adjacency List:** We first create an adjacency list `adj` where each manager points to their direct subordinates.
- **DFS Function:** The `dfs` function calculates the total time needed for an employee to inform all of their subordinates by recursively visiting each subordinate and calculating the maximum inform time needed.
- **Result Calculation:** We call the `dfs` function starting from the head of the company, which returns the total time required to inform all employees.

This approach efficiently calculates the time needed to inform all employees using DFS, leveraging the tree structure of the manager-subordinate relationships.
