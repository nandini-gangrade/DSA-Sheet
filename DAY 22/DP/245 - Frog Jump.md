# [403. Frog Jump](https://leetcode.com/problems/frog-jump/description/)

To solve the problem of determining if the frog can cross the river by landing on the last stone, we need to use dynamic programming with a combination of depth-first search (DFS) and memoization.

### Problem Breakdown:
1. **Initial Conditions**: The frog starts on the first stone (`stones[0] == 0`), and the first jump must be 1 unit.
2. **Jump Rules**: If the frog's last jump was `k` units, the next jump can be `k-1`, `k`, or `k+1` units.
3. **Objective**: Determine if the frog can reach the last stone by making valid jumps as per the above rules.

### Approach:
1. **DFS with Memoization**: We can represent the problem as a depth-first search, where at each stone, we try to make jumps of `k-1`, `k`, and `k+1` units. We use memoization to store the results of subproblems (i.e., whether the frog can reach the last stone from the current stone with a certain jump).

2. **Base Cases**:
   - If the frog reaches the last stone, return `True`.
   - If the frog cannot make any valid jump, return `False`.

3. **Transition**:
   - For each stone, check if it can be reached with a valid jump size. If yes, recursively check if the frog can reach the last stone from this position.

### Code Implementation:

```python
class Solution:
    def canCross(self, stones: List[int]) -> bool:
        # Dictionary to store positions of stones and valid jumps to reach that position
        stone_positions = {stone: set() for stone in stones}
        stone_positions[0].add(0)  # Starting point with a jump of 0
        
        for stone in stones:
            for last_jump in stone_positions[stone]:
                for new_jump in [last_jump - 1, last_jump, last_jump + 1]:
                    if new_jump > 0 and (stone + new_jump) in stone_positions:
                        stone_positions[stone + new_jump].add(new_jump)
        
        # If the last stone's position has any valid jump, return True
        return bool(stone_positions[stones[-1]])

# Example usage
solution = Solution()
print(solution.canCross([0, 1, 3, 5, 6, 8, 12, 17]))  # Output: True
print(solution.canCross([0, 1, 2, 3, 4, 8, 9, 11]))  # Output: False
```

### Explanation of the Code:
1. **Initialization**: We create a dictionary `stone_positions` where each key is a stone position and the value is a set of valid jumps that can reach that stone.
2. **Filling the Dictionary**: We iterate over each stone and, for every valid jump that reaches that stone, we try to make the next jump (`k-1`, `k`, or `k+1`) to see if it lands on another stone. If it does, we add that jump size to the set of the target stone.
3. **Check Final Condition**: Finally, we check if the last stone in the `stones` list has any valid jumps that can reach it. If yes, the frog can cross the river; otherwise, it cannot.

### Complexity:
- **Time Complexity**: \(O(n^2)\), where \(n\) is the number of stones. In the worst case, every stone can be reachable with multiple jump sizes, and we might have to explore each possibility.
- **Space Complexity**: \(O(n^2)\) due to the use of the dictionary to store possible jumps for each stone.

This solution efficiently determines if the frog can cross the river under the given constraints.
