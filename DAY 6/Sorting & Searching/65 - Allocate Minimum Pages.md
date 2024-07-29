# [Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1)

You have `n` books, each with a certain number of pages given in an array `arr[]`. You need to allocate these books to `m` students such that:
- Each student gets at least one book.
- The books allocated to each student must be contiguous.
- You want to minimize the maximum number of pages assigned to any student.

## Intuition
To solve the problem, you need to allocate books in such a way that the maximum number of pages any student receives is minimized. This can be approached using binary search combined with a feasibility check:
1. **Binary Search**: We use binary search to find the smallest possible value of the maximum pages that any student can receive.
2. **Feasibility Check**: For each potential maximum page value (midpoint in binary search), check if it's possible to allocate books such that no student gets more than this number of pages.

### Approach
1. **Binary Search Initialization**:
   - **Start**: The maximum pages in a single book (`max(arr)`), because no student can get fewer pages than the largest book.
   - **End**: The total sum of pages (`sum(arr)`), as in the worst case, one student gets all the books.

2. **Feasibility Check**:
   - Traverse through the books while keeping a running total of pages assigned to the current student.
   - If adding the next book exceeds the current maximum pages (`mid`), allocate books to the next student and reset the running total.
   - Count the number of students needed. If more than `m`, then the current `mid` is too small.

3. **Binary Search Execution**:
   - Adjust the search range based on the feasibility check result:
     - If the current `mid` is feasible, try a smaller value (`end = mid - 1`).
     - If not feasible, try a larger value (`start = mid + 1`).

## Code

```python
class Solution:
    def possible(self, v, mid, member, n):
        cnt = 0
        running = 0
        for i in range(n):
            running += v[i]
            
            if running > mid:
                cnt += 1
                running = v[i]
                
        return cnt + 1 <= member  # Add 1 because the last segment might not be counted in cnt

    def findPages(self, n, arr, m):
        start = max(arr)  # Minimum possible maximum pages
        end = sum(arr)    # Maximum possible maximum pages
        
        if n < m:
            return -1  # Not enough books for each student
        
        while start <= end:
            mid = start + (end - start) // 2
            if self.possible(arr, mid, m, n):
                end = mid - 1
            else:
                start = mid + 1
        
        return start
```

## Complexity
- **Time Complexity**: \(O(n \log(\text{sum of pages}))\)
  - **Binary Search**: \(O(\log(\text{sum of pages}))\) iterations.
  - **Feasibility Check**: \(O(n)\) operations per iteration.
- **Space Complexity**: \(O(1)\)
  - No additional space proportional to input size is used.
