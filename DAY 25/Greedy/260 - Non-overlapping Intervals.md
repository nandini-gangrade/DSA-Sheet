# [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)

To solve the problem of removing the minimum number of overlapping intervals, we can use a **Greedy Algorithm** approach. The key idea here is to always try to keep as many intervals as possible without overlap. To do this, we focus on choosing intervals that end the earliest, as this gives us the best chance of fitting in more intervals later.

### Strategy:

1. **Sort by Ending Time**:
   - Sort the intervals based on their ending times. This ensures that the interval which ends the earliest is considered first, allowing for more space for subsequent intervals.

2. **Greedy Choice**:
   - We keep track of the end time of the last interval that was included in the non-overlapping set. If the start time of the current interval is greater than or equal to this end time, we can include it. Otherwise, we skip the current interval (which means removing it to avoid overlap).

3. **Count the Overlaps**:
   - Whenever we encounter an interval that overlaps with the previous one (i.e., its start is before the previous interval's end), we increment a counter for intervals to be removed.

### Steps:
1. Sort intervals by their end time.
2. Iterate through the sorted intervals, keeping track of the last included interval's end time.
3. Count and skip overlapping intervals.

### Python Code Implementation:

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return 0
        
        # Sort the intervals by their end times
        intervals.sort(key=lambda x: x[1])
        
        # Track the end time of the last added interval and the number of intervals to remove
        end = intervals[0][1]
        count = 0
        
        for i in range(1, len(intervals)):
            # If the current interval starts before the last interval ends, it overlaps
            if intervals[i][0] < end:
                count += 1  # Increment the removal count
            else:
                # Update the end time to the end of the current interval
                end = intervals[i][1]
        
        return count
```

### Explanation:

1. **Sorting**:
   - We sort the intervals by their ending times using `intervals.sort(key=lambda x: x[1])`. This ensures that we always consider the interval that finishes the earliest.
   
2. **Loop Through Intervals**:
   - We initialize the `end` variable to the end of the first interval (after sorting).
   - As we iterate through the remaining intervals, we check if the current interval's start time is less than the `end` time of the last interval. If it is, this means the intervals overlap, and we need to remove one, so we increase the count.
   - If the current interval doesn't overlap, we update the `end` variable to the end of the current interval.
   
3. **Counting Overlaps**:
   - The `count` variable keeps track of how many intervals are removed due to overlaps.

### Time Complexity:
- Sorting the intervals takes \(O(n \log n)\), where \(n\) is the number of intervals.
- The iteration through the sorted intervals takes \(O(n)\).

Thus, the overall time complexity is \(O(n \log n)\).

### Example Walkthrough:

1. **Example 1**: 
   ```python
   intervals = [[1,2],[2,3],[3,4],[1,3]]
   ```
   - After sorting: `[[1,2], [2,3], [1,3], [3,4]]`
   - We start with the first interval `[1, 2]` and set `end = 2`.
   - The next interval `[2, 3]` starts at 2, so it doesn't overlap. We update `end = 3`.
   - The interval `[1, 3]` starts at 1, which is before `end = 3`, so it overlaps. We increment the removal count to 1.
   - The last interval `[3, 4]` starts at 3, so it doesn't overlap. We update `end = 4`.
   - Output: `1` interval needs to be removed.

2. **Example 2**:
   ```python
   intervals = [[1,2],[1,2],[1,2]]
   ```
   - After sorting: `[[1,2], [1,2], [1,2]]`
   - The first interval is taken, with `end = 2`.
   - The second interval starts at 1, so it overlaps. We increment the count to 1.
   - The third interval also overlaps. We increment the count to 2.
   - Output: `2` intervals need to be removed.

3. **Example 3**:
   ```python
   intervals = [[1,2],[2,3]]
   ```
   - After sorting: `[[1,2], [2,3]]`
   - No intervals overlap, so no intervals are removed.
   - Output: `0`.

### Conclusion:
This approach efficiently calculates the minimum number of intervals to be removed in \(O(n \log n)\) time, making it suitable for large inputs, as required by the constraints.
