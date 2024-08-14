# [Job Sequencing Problem](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

To solve the **Job Scheduling Problem**, the objective is to maximize the profit by scheduling the jobs such that each job is completed on or before its deadline, and only one job can be scheduled at a time.

### Approach:

1. **Sort Jobs by Profit**:
   - Since we want to maximize the profit, the first step is to sort the jobs in decreasing order of profit. This ensures that higher-profit jobs are considered first for scheduling.

2. **Use a Slot Array**:
   - Use a `slot` array to keep track of which time slots are occupied. Since each job takes 1 unit of time, and jobs must be scheduled before their deadline, the length of this slot array is the maximum deadline in the input jobs.

3. **Greedy Assignment**:
   - For each job, try to schedule it in the latest possible slot (i.e., just before its deadline). If a slot is available, mark it as occupied and add the job's profit to the total profit. Repeat this for all jobs in decreasing order of profit.

### Steps:
1. **Sort the jobs** based on profit in descending order.
2. **Iterate through the jobs** and try to find an available slot (from the job's deadline backwards).
3. **If an available slot is found**, assign the job to that slot, increase the count of jobs done, and add the job's profit to the total profit.

### Code Implementation:

```cpp
#include<bits/stdc++.h>
using namespace std;

struct Job {
    int id;      // Job Id
    int dead;    // Deadline of job
    int profit;  // Profit if job is over before or on deadline
};

// Comparator function to sort jobs by decreasing profit
bool compare(Job a, Job b) {
    return a.profit > b.profit;
}

class Solution {
    public:
    // Function to find the maximum profit and the number of jobs done.
    vector<int> JobScheduling(Job arr[], int n) { 
        // Sort jobs by descending profit
        sort(arr, arr + n, compare);
        
        // Find the maximum deadline to create a slots array
        int maxDeadline = 0;
        for (int i = 0; i < n; i++) {
            maxDeadline = max(maxDeadline, arr[i].dead);
        }
        
        // Create a slots array to track available time slots, initially all free (-1)
        vector<int> slot(maxDeadline + 1, -1);
        
        int numJobs = 0, maxProfit = 0;
        
        // Process each job in the sorted order
        for (int i = 0; i < n; i++) {
            // Try to find a slot for this job from its deadline backwards
            for (int j = arr[i].dead; j > 0; j--) {
                if (slot[j] == -1) { // If the slot is free
                    slot[j] = arr[i].id;  // Assign this job to the slot
                    numJobs++;            // Increment the number of jobs done
                    maxProfit += arr[i].profit;  // Add the profit of this job
                    break;                // Exit the loop as the job is assigned
                }
            }
        }
        
        return {numJobs, maxProfit};
    } 
};

// Driver code
int main() {
    int n = 5;
    Job arr[] = { {1, 2, 100}, {2, 1, 19}, {3, 2, 27}, {4, 1, 25}, {5, 1, 15} };
    
    Solution s;
    vector<int> result = s.JobScheduling(arr, n);
    cout << "Number of jobs done: " << result[0] << "\n";
    cout << "Maximum profit: " << result[1] << "\n";
    return 0;
}
```

### Explanation:

1. **Job Structure**:
   - We define a `Job` structure to represent each job with three fields:
     - `id`: Job ID
     - `dead`: Deadline of the job
     - `profit`: Profit for completing the job before or on its deadline.

2. **Sorting**:
   - The jobs are sorted in descending order based on their profit using the `compare` function.

3. **Slot Array**:
   - The `slot` array is initialized with `-1` indicating all slots are initially free.
   - The length of the slot array is `maxDeadline + 1` to ensure it can hold all possible slots (from 0 to maxDeadline).

4. **Job Assignment**:
   - For each job, starting from the highest profit, we try to assign it to the latest available time slot before its deadline. If a slot is found, it is marked as occupied, the job is considered done, and its profit is added to the total profit.

5. **Result**:
   - The function returns a vector with two values:
     - The number of jobs done.
     - The maximum profit obtained.

### Time Complexity:
- **Sorting**: O(n log n) due to sorting the jobs by profit.
- **Greedy Assignment**: O(n * d) where `d` is the maximum deadline. In the worst case, this can be O(n^2) if the maximum deadline is proportional to `n`.
  
### Space Complexity:
- O(n) due to the `slot` array.

### Example:

1. **Input**: `Jobs = {{1, 2, 100}, {2, 1, 19}, {3, 2, 27}, {4, 1, 25}, {5, 1, 15}}`
   - Output: `2 127`
   - Explanation: Two jobs can be done (`Job 1` with profit 100 and `Job 3` with profit 27), for a total profit of 127.

2. **Input**: `Jobs = {{1, 4, 20}, {2, 1, 1}, {3, 1, 40}, {4, 1, 30}}`
   - Output: `2 60`
   - Explanation: Two jobs can be done (`Job 1` and `Job 3`), for a total profit of 60.

This algorithm efficiently schedules jobs to maximize profit while respecting deadlines.
