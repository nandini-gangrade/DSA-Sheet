# [857. Minimum Cost to Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers/description/)

To solve the problem of finding the minimum cost to hire exactly `k` workers such that their pay is proportional to their quality, we can use a combination of sorting and a min-heap to efficiently manage the workers' costs. Here's a step-by-step explanation of the approach:

### Approach

1. **Calculate the Pay Ratio:**
   - For each worker, calculate the ratio of their wage to their quality. This ratio represents the minimum pay rate per unit quality required to hire that worker. If a worker's quality is `q` and their wage is `w`, the ratio is `w / q`.

2. **Sort Workers by Ratio:**
   - Sort all workers by their pay ratio (`w / q`). This sorting helps in processing workers starting from the least expensive in terms of the proportional pay rate.

3. **Use a Min-Heap to Manage Quality:**
   - As we iterate through the sorted workers, we maintain a min-heap to keep track of the `k` highest qualities seen so far. This allows us to efficiently compute the total cost for any group of `k` workers.

4. **Calculate Minimum Cost:**
   - For each worker in the sorted list, compute the total cost to hire exactly `k` workers including this worker. The cost for hiring `k` workers with a specific pay ratio is given by multiplying the sum of the `k` highest qualities by the current ratio.

5. **Return the Minimum Cost:**
   - Track the minimum cost encountered during the iteration and return it as the result.

### Implementation

Here's the Python code implementing the above approach:

```python
import heapq

class Solution:
    def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
        n = len(quality)
        workers = [(w / q, q) for q, w in zip(quality, wage)]
        
        # Sort workers by their ratio w/q
        workers.sort()
        
        # Min-heap to maintain the largest k qualities
        min_heap = []
        sum_quality = 0
        min_cost = float('inf')
        
        for ratio, q in workers:
            # Add current worker's quality to the min-heap
            heapq.heappush(min_heap, -q)
            sum_quality += q
            
            # If we have more than k workers in the heap, remove the smallest quality
            if len(min_heap) > k:
                sum_quality += heapq.heappop(min_heap)  # Remove smallest quality
            
            # If we have exactly k workers, calculate the cost
            if len(min_heap) == k:
                min_cost = min(min_cost, ratio * sum_quality)
        
        return min_cost
```

### Explanation

1. **Sorting by Ratio:**
   - We first calculate the ratio of wage to quality for each worker and sort workers based on this ratio. This sorting allows us to consider workers with the least pay rate per unit quality first.

2. **Min-Heap for Quality:**
   - We use a min-heap to keep track of the largest `k` qualities. This heap allows us to efficiently manage and compute the sum of the top `k` qualities.

3. **Iterating and Computing Costs:**
   - As we process each worker, we update the heap with the current worker's quality and adjust the sum of the top `k` qualities accordingly. We then calculate the cost of hiring `k` workers with the current ratio and update the minimum cost if this cost is lower.

### Complexity

- **Time Complexity:** \(O(n \log k)\), where \(n\) is the number of workers. Sorting takes \(O(n \log n)\) and maintaining the heap takes \(O(n \log k)\).
- **Space Complexity:** \(O(k)\) for the heap.

This approach efficiently handles the problem constraints and ensures that we find the minimum cost for hiring exactly `k` workers with the required conditions.
