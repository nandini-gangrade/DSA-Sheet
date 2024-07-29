# [AGGRCOW - Aggressive cows](https://www.spoj.com/problems/AGGRCOW/)

Given `N` stalls at various positions and `C` cows, the goal is to maximize the smallest distance between any two cows placed in these stalls.

## Intuition

1. **Binary Search on Distance**:
   - To find the largest possible minimum distance between cows, use binary search on the distance.
   - The range of binary search will be from `0` to the maximum possible distance (`max_position - min_position`).

2. **Greedy Placement**:
   - For a given distance (midpoint in binary search), check if it’s possible to place all cows in the stalls such that each cow is at least this distance apart from the others.
   - Use a greedy approach to place cows in the stalls and validate if the current distance is feasible.

## Approach

1. **Sort the Stall Positions**:
   - First, sort the stall positions to facilitate easier distance calculations and placements.

2. **Binary Search**:
   - Initialize the search range: `low` is `1` and `high` is the difference between the maximum and minimum stall positions.
   - Use binary search to determine the maximum possible minimum distance. For each midpoint distance:
     - Use the greedy approach to check if it's feasible to place all cows such that each cow is at least `mid` distance apart from the others.

3. **Feasibility Check**:
   - Place the first cow in the first stall.
   - Try to place each subsequent cow in the next stall that is at least `mid` distance away from the last placed cow.
   - If all cows are placed successfully, the distance is feasible.

## Code

```python
def canPlaceCows(stalls, n, c, min_distance):
    count = 1  # Place the first cow in the first stall
    last_position = stalls[0]
    
    for i in range(1, n):
        if stalls[i] - last_position >= min_distance:
            count += 1
            last_position = stalls[i]
            if count == c:
                return True
    return False

def largestMinDistance(test_cases):
    results = []
    
    for test in test_cases:
        n, c, stalls = test
        stalls.sort()
        
        low, high = 1, stalls[-1] - stalls[0]
        best_distance = 0
        
        while low <= high:
            mid = (low + high) // 2
            if canPlaceCows(stalls, n, c, mid):
                best_distance = mid
                low = mid + 1
            else:
                high = mid - 1
        
        results.append(best_distance)
    
    return results

# Example usage
t = 1
test_cases = [
    (5, 3, [1, 2, 8, 4, 9])
]

results = largestMinDistance(test_cases)
for result in results:
    print(result)
```

## Complexity

- **Time Complexity**:
  - Sorting the stalls takes \(O(N \log N)\).
  - Binary search takes \(O(\log(\text{range}))\) where `range` is the maximum possible distance.
  - Each binary search iteration requires \(O(N)\) for checking feasibility.
  - Overall complexity: \(O(N \log N + N \log D)\), where \(D\) is the maximum possible distance between stalls.

- **Space Complexity**:
  - The space complexity is \(O(N)\) due to the storage of the stalls list and temporary variables.
