# [1642. Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach/description/)

To solve this problem, we need to find the furthest building we can reach by optimally using the given number of bricks and ladders. The key idea is to use ladders for the largest jumps between buildings and bricks for the smaller ones.

### Approach:

1. **Using a Min-Heap**:
   - We use a min-heap (priority queue) to track the largest jumps where a ladder should ideally be used.
   - As we progress from one building to the next, for every positive difference (i.e., height increase), we first assume we use bricks. We then push this difference into our min-heap.
   - If the size of the heap exceeds the number of ladders available, we pop the smallest jump from the heap and instead cover it with bricks (since it was initially covered by a ladder).
   - If we don't have enough bricks to cover the difference, then we can no longer proceed to the next building.

2. **Greedy Strategy**:
   - The greedy approach ensures that ladders are used for the largest jumps, allowing bricks to be used for smaller jumps where ladders would be inefficient.

### Python Implementation:

```python
import heapq

class Solution:
    def furthestBuilding(self, heights: List[int], bricks: int, ladders: int) -> int:
        min_heap = []
        
        for i in range(len(heights) - 1):
            diff = heights[i + 1] - heights[i]
            
            if diff > 0:
                heapq.heappush(min_heap, diff)
            
            # If the number of jumps exceeds the number of ladders, use bricks
            if len(min_heap) > ladders:
                bricks -= heapq.heappop(min_heap)
            
            # If we run out of bricks, return the current building index
            if bricks < 0:
                return i
        
        return len(heights) - 1
```

### Explanation:

1. **Heap Operations**:
   - For every height increase `diff` between two consecutive buildings, push it into the heap.
   - If the heap's size exceeds the number of ladders, pop the smallest value (which represents the smallest jump) and subtract it from the bricks.

2. **Bricks Management**:
   - When the smallest jump is popped from the heap and subtracted from bricks, if bricks go negative, we cannot proceed further. Hence, we return the current index.

3. **Final Step**:
   - If the loop completes without running out of bricks, it means we can reach the last building.

### Time Complexity:
- **Time Complexity**: \(O(n \log k)\) where \(n\) is the length of `heights` and \(k\) is the number of ladders. The logarithmic factor comes from the heap operations.
- **Space Complexity**: \(O(k)\) for storing the heap, where \(k\) is the number of ladders.

### Example Walkthrough:

- For `heights = [4, 2, 7, 6, 9, 14, 12], bricks = 5, ladders = 1`:
  - Start from building `0` and move to building `1` without using anything.
  - Move from building `1` to `2` using `5` bricks.
  - Move from building `2` to `3` without using anything.
  - Move from building `3` to `4` using the ladder.
  - No more resources available to move beyond building `4`.

Thus, the output is `4`.

This solution efficiently finds the furthest building you can reach by carefully balancing the use of bricks and ladders.
