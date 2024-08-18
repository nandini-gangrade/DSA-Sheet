# [CHOCOLA - Chocolate](https://www.spoj.com/problems/CHOCOLA/)

To solve this problem, we need to determine the minimum cost of breaking a chocolate bar into individual squares given the costs associated with breaking along vertical and horizontal lines. 

### Strategy:

The problem can be approached by recognizing that we need to choose the order in which we make the breaks to minimize the total cost. This is a typical **Greedy Algorithm** problem, where we choose the next step that seems to offer the most immediate benefit (lowest cost) at each stage.

### Key Points:
1. **Initial Setup**:
   - We have `m-1` vertical cuts and `n-1` horizontal cuts.
   - Each time we make a cut, we increase the number of parts along that dimension.
   - If we make a horizontal cut first, subsequent vertical cuts will cost more since they will now apply to all the parts along the horizontal dimension that we’ve just increased.

2. **Greedy Approach**:
   - We should start by making the cut that has the highest cost because this will minimize the added cost due to further cuts.
   - Sort the vertical cuts and horizontal cuts in descending order.
   - Start making the most expensive cut first, whether it’s vertical or horizontal.
   - Maintain the count of how many vertical and horizontal parts we currently have, and calculate the cost accordingly.

### Implementation:
```python
def min_cost_to_break_chocolate(m, n, vertical_costs, horizontal_costs):
    # Sort the costs in descending order
    vertical_costs.sort(reverse=True)
    horizontal_costs.sort(reverse=True)
    
    # We start with 1 part in each direction
    vertical_parts = 1
    horizontal_parts = 1
    
    total_cost = 0
    
    i, j = 0, 0
    
    while i < len(vertical_costs) and j < len(horizontal_costs):
        if vertical_costs[i] >= horizontal_costs[j]:
            total_cost += vertical_costs[i] * horizontal_parts
            vertical_parts += 1
            i += 1
        else:
            total_cost += horizontal_costs[j] * vertical_parts
            horizontal_parts += 1
            j += 1
    
    # Add the remaining cuts if any
    while i < len(vertical_costs):
        total_cost += vertical_costs[i] * horizontal_parts
        i += 1
        
    while j < len(horizontal_costs):
        total_cost += horizontal_costs[j] * vertical_parts
        j += 1
    
    return total_cost

def solve():
    t = int(input().strip())  # number of test cases
    results = []
    
    for _ in range(t):
        input()  # read the blank line
        
        m, n = map(int, input().strip().split())
        vertical_costs = [int(input().strip()) for _ in range(m-1)]
        horizontal_costs = [int(input().strip()) for _ in range(n-1)]
        
        result = min_cost_to_break_chocolate(m, n, vertical_costs, horizontal_costs)
        results.append(result)
    
    for result in results:
        print(result)

```

### Explanation:
1. **Sorting**:
   - We first sort the vertical and horizontal cut costs in descending order to maximize the early returns when making cuts.
   
2. **Greedy Selection**:
   - We iteratively choose the higher cost between the next available vertical and horizontal cuts.
   - If we make a vertical cut, it increases the number of vertical segments, thus increasing the future cost of any horizontal cut. The same applies vice versa.

3. **Complexity**:
   - Sorting the cuts takes `O(m log m + n log n)` time.
   - The remaining part of the algorithm runs in linear time, `O(m + n)`.

### Example:
For the given input:
```
1
6 4
2
1
3
1
4
4
1
2
```
- Vertical costs: `[2, 1, 3, 1, 4]` → Sorted: `[4, 3, 2, 1, 1]`
- Horizontal costs: `[4, 1, 2]` → Sorted: `[4, 2, 1]`
- The optimal order of cuts leads to the total minimal cost of `42`.

This solution ensures that the minimal cost to break the chocolate into single squares is computed efficiently.
