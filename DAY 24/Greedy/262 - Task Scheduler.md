# [621. Task Scheduler](https://leetcode.com/problems/task-scheduler/description/)

The problem requires determining the minimum number of intervals needed to execute all tasks while respecting the cooling period `n` between identical tasks. Let's walk through a structured approach to solving it:

### Approach:

1. **Task Frequency**:
   - First, calculate the frequency of each task. The most frequent task will determine the overall structure of the intervals.

2. **Organizing Tasks**:
   - The key observation is that the most frequent task will dictate the minimum length of the schedule. If `A` is the most frequent task with frequency `f`, you will need at least `f - 1` blocks, each containing `n + 1` slots, to separate the `A` tasks adequately. The remaining tasks will fill in these blocks.

3. **Idle Time**:
   - If there are fewer tasks than required to fill the slots between two identical tasks, there will be "idle" times.
   - The overall interval count is determined by either filling all slots (with or without idle times) or by the total number of tasks if we don’t need to insert any idle times.

### Strategy:
1. **Calculate task frequencies**.
2. **Find the task with the maximum frequency**.
3. **Calculate the idle slots required**.
4. **Fill idle slots with the remaining tasks**.
5. **Determine the total number of intervals needed**.

### Solution Steps:

1. **Task Frequency Calculation**:
   - We count how many times each task appears.

2. **Max Frequency and Idle Slots**:
   - Identify the maximum frequency. This gives the "skeleton" of the schedule.
   - Idle slots will be formed between these high-frequency tasks, which need to be filled with other tasks.

3. **Result Calculation**:
   - The final result will either be the total number of tasks (if no idle slots are needed) or the number of slots filled by both tasks and idle periods.

### Formula:
- The basic idea is to calculate:
  \[
  \text{max\_intervals} = (f\_max - 1) \times (n + 1) + \text{count of tasks with frequency } f\_max
  \]
  where `f_max` is the maximum frequency of any task.

- The final answer is the maximum of:
  - The number of total tasks (if they can be arranged without idle slots), and
  - The calculated `max_intervals`.

### Code Implementation:

```python
from collections import Counter

class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        # Step 1: Calculate frequency of each task
        task_counts = Counter(tasks)
        max_freq = max(task_counts.values())
        
        # Step 2: Count how many tasks have the maximum frequency
        max_freq_count = sum(1 for task, freq in task_counts.items() if freq == max_freq)
        
        # Step 3: Calculate the minimum intervals needed
        part_count = max_freq - 1
        part_length = n + 1
        empty_slots = part_count * part_length
        total_slots = empty_slots + max_freq_count
        
        # Step 4: The result is either the total number of tasks or the calculated total_slots
        return max(len(tasks), total_slots)

# Example Usage
solution = Solution()

# Test case 1
tasks = ["A", "A", "A", "B", "B", "B"]
n = 2
print(solution.leastInterval(tasks, n))  # Output: 8

# Test case 2
tasks = ["A", "C", "A", "B", "D", "B"]
n = 1
print(solution.leastInterval(tasks, n))  # Output: 6

# Test case 3
tasks = ["A", "A", "A", "B", "B", "B"]
n = 3
print(solution.leastInterval(tasks, n))  # Output: 10
```

### Explanation:

1. **Task Frequency Calculation**:
   - We use `Counter` to get the frequency of each task.

2. **Max Frequency**:
   - We determine `max_freq`, the highest task frequency, and also count how many tasks have this maximum frequency (`max_freq_count`).

3. **Interval Calculation**:
   - We calculate the number of "parts" that need to be filled with other tasks or idle time.
   - The formula `(max_freq - 1) * (n + 1) + max_freq_count` calculates the total number of intervals needed if there are idle times.

4. **Final Answer**:
   - The final number of intervals is either the total number of tasks (if no idle time is needed) or the calculated number of intervals.

### Time Complexity:
- **O(n)**: Counting the frequency of tasks takes linear time, and determining the max frequency also takes linear time relative to the size of `tasks`.

### Space Complexity:
- **O(1)**: We only use constant extra space (ignoring the input and output), as the frequency table is bounded by the size of the alphabet (26 for uppercase English letters).

This approach efficiently handles the constraints and provides the correct solution for the given problem.
