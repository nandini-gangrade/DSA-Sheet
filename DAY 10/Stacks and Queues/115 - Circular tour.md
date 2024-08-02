# [Circular tour](https://www.geeksforgeeks.org/problems/circular-tour-1587115620/1)

Given `N` petrol pumps arranged in a circle, each petrol pump `i` provides `petrol[i]` liters of petrol, and the distance to the next petrol pump is `distance[i]` units. You need to find the starting pump index from which a truck can complete a full circle without running out of petrol.

## Intuition
The main idea is to ensure that the total petrol is sufficient to cover the total distance. If it is not, completing the circle is impossible, and we return `-1`. If the total petrol is sufficient, we need to find the correct starting point.
### Explanation with Example

Consider the example input:

- `N = 4`
- `Petrol = [4, 6, 7, 4]`
- `Distance = [6, 5, 3, 5]`

In pairs: `[(4, 6), (6, 5), (7, 3), (4, 5)]`.

1. **Check Total Petrol vs. Total Distance:** 
   - Total Petrol = 4 + 6 + 7 + 4 = 21
   - Total Distance = 6 + 5 + 3 + 5 = 19
   - Since 21 > 19, it’s possible to complete the circle.

2. **Finding Starting Point:**
   - Start from pump 0:
     - Balance: 4 - 6 = -2 (reset start to pump 1)
   - From pump 1:
     - Balance: 6 - 5 = 1
     - Balance: 1 + (7 - 3) = 5
     - Balance: 5 + (4 - 5) = 4

The truck can complete the tour starting from pump 1, which corresponds to the second petrol pump, hence the output is `1`.

## Approach
1. **Check Total Petrol vs. Total Distance:** First, calculate the total petrol and total distance. If the total petrol is less than the total distance, return `-1`.
2. **Find the Starting Point:**
   - Start iterating over the pumps.
   - Maintain a `current_petrol` balance as you iterate, adding petrol and subtracting distance.
   - If at any point `current_petrol` becomes negative, it means the current starting point is not feasible. Set the next pump as the potential starting point and reset `current_petrol`.
   - Keep track of the overall balance of petrol vs. distance (`total_petrol - total_distance`).
3. **Return the Starting Point:** Once you have found a starting point that maintains a non-negative `current_petrol`, that index is the answer.

## Code

```python
class Solution:
    def tour(self, lis, n):
        # Initialize variables
        start = 0
        current_petrol = 0
        total_petrol = 0
        total_distance = 0
        
        # Traverse through each petrol pump
        for i in range(n):
            petrol, distance = lis[i]
            total_petrol += petrol
            total_distance += distance
            current_petrol += petrol - distance
            
            # If current_petrol is negative, move start to the next pump
            if current_petrol < 0:
                start = i + 1
                current_petrol = 0
        
        # If total petrol is less than total distance, return -1
        if total_petrol < total_distance:
            return -1
        
        return start
```

## Complexity Analysis

- **Time Complexity:** \(O(N)\), where \(N\) is the number of petrol pumps. We traverse the list of petrol pumps once.
- **Space Complexity:** \(O(1)\), as we use a constant amount of extra space regardless of the input size.


This approach efficiently determines the feasible starting point by taking advantage of the circular nature of the problem and using a single pass to ensure the petrol balance remains non-negative.
