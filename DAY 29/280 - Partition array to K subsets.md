# [Partition array to K subsets](https://www.geeksforgeeks.org/problems/partition-array-to-k-subsets/1)

The problem is to determine if an integer array can be partitioned into `K` non-empty subsets such that the sum of the elements in each subset is equal. Let's break down the problem, the approach, and the implementation of the solution.

### Problem Breakdown

Given:
- An array `a[]` of size `N`.
- An integer `K` representing the number of subsets.

We need to check if it's possible to divide the array into `K` subsets where each subset has the same sum.

### Key Points to Consider

1. **Sum of Elements**:
   - The total sum of the array elements, say `S`, must be divisible by `K`. If not, it's impossible to split the array into `K` equal-sum subsets.

2. **Target Subset Sum**:
   - If `S` is divisible by `K`, then each subset should have a sum of `S/K`.

3. **Element Bound**:
   - If the largest element in the array is greater than `S/K`, it's impossible to include that element in any subset without exceeding the target sum, so we can immediately return `false`.

### Approach

1. **Sort and Greedy Check**:
   - Sort the array in non-increasing order.
   - Use a priority queue (max heap) to manage the current sum of elements in each subset.
   - Try to assign each element to the subset with the smallest current sum.

2. **Backtracking**:
   - For each element, try placing it in each subset recursively, backtrack if placing it in the current subset doesn't lead to a solution.

3. **Edge Cases**:
   - If the array has fewer elements than `K`, or if the sum isn't divisible by `K`, return `false`.

### Code Implementation

```cpp
#include <vector>
#include <numeric>
#include <algorithm>
#include <queue>

class Solution {
public:
    bool isKPartitionPossible(int a[], int n, int k) {
        int total = std::accumulate(a, a+n, 0);
        
        // Check if the total sum is divisible by K
        if (total % k != 0) return false;
        int partitionSum = total / k;

        // Sort the array in non-increasing order
        std::sort(a, a+n, std::greater<int>());

        // If the largest element is greater than partitionSum, return false
        if (a[0] > partitionSum) return false;

        // Use a priority queue to keep track of the current sum of each subset
        std::priority_queue<int> pq;
        for (int i = 0; i < k; i++) pq.push(0);

        // Attempt to place each element in one of the subsets
        for (int i = 0; i < n; i++) {
            int currSum = pq.top(); pq.pop();
            currSum += a[i];
            
            // If current sum of any subset exceeds partitionSum, return false
            if (currSum > partitionSum) return false;
            
            pq.push(currSum);
        }

        return true;
    }
};
```

### Explanation

- **Total Sum Calculation**: First, calculate the total sum of the array. If the total sum is not divisible by `K`, it's impossible to divide the array into `K` subsets with equal sums.
- **Sorting**: The array is sorted in non-increasing order to try placing the largest elements first, which helps in reducing the number of backtracking steps.
- **Priority Queue**: A max heap is used to track the current sum of elements in each subset. This approach is greedy, trying to keep the subsets balanced in terms of their sums.
- **Greedy Placement**: Each element is placed into the subset with the smallest current sum. If this sum exceeds the target, the function returns `false`.

### Complexity Analysis

- **Time Complexity**: The time complexity is dominated by the sorting step, which is \(O(N \log N)\), and subsequent operations in the loop are \(O(N \log K)\). Hence, the overall time complexity is \(O(N \log N + N \log K)\).
- **Space Complexity**: The space complexity is \(O(K)\) for the priority queue.

This approach efficiently checks whether the array can be divided into `K` subsets with equal sums using a combination of greedy placement and priority queue management.
