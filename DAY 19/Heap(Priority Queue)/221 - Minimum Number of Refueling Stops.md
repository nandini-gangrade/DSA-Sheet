# [871. Minimum Number of Refueling Stops](https://leetcode.com/problems/minimum-number-of-refueling-stops/description/)

To solve the problem of determining the minimum number of refueling stops required to reach a destination given the initial fuel and a series of gas stations along the way, we can use a greedy approach with a priority queue (max-heap). Here's the detailed approach and explanation:

### Approach

1. **Initial Setup:**
   - We start with a certain amount of fuel (`startFuel`) and we need to reach a target distance.
   - We maintain a priority queue (max-heap) to keep track of the fuel available at gas stations we have passed.

2. **Iterate Through Stations:**
   - For each gas station, if it is reachable with the current fuel, we push its fuel amount into the priority queue.
   - If it is not reachable, we need to refuel. We will use the maximum fuel available from previously passed stations to extend our range.
   - Refuel until we either can reach the current station or run out of refuel options.

3. **Greedy Refueling:**
   - Each time we decide to refuel, we choose the gas station that provides the maximum fuel from our priority queue to maximize the distance we can travel.

4. **Final Check:**
   - After processing all stations, if the current fuel allows us to reach the target, we return the count of refuel stops.
   - If after exhausting all refueling options we cannot reach the target, return `-1`.

### Detailed Solution

Here's the implementation of the above approach:

```python
import heapq

class Solution:
    def minRefuelStops(self, target: int, startFuel: int, stations: List[List[int]]) -> int:
        # Add a final station at the target with 0 fuel
        stations.append([target, 0])
        
        # Priority queue (max-heap) to store the fuel amounts of stations passed
        max_heap = []
        heapq.heapify(max_heap)
        
        # Current position and fuel
        curr_position = 0
        curr_fuel = startFuel
        refuel_stops = 0
        
        for position, fuel in stations:
            # Calculate the distance from the current position to the next station
            distance = position - curr_position
            
            # While the current fuel is insufficient to reach the next station
            while curr_fuel < distance:
                if not max_heap:
                    return -1
                # Refuel using the station with the maximum fuel we have passed
                curr_fuel += -heapq.heappop(max_heap)
                refuel_stops += 1
            
            # Update current fuel and position
            curr_fuel -= distance
            curr_position = position
            
            # Add the current station's fuel to the heap
            heapq.heappush(max_heap, -fuel)
        
        return refuel_stops
```

### Explanation

1. **Heap Initialization:**
   - We initialize a max-heap (`max_heap`) to keep track of the fuel available from previously passed gas stations. The negative sign is used to simulate a max-heap using Python’s `heapq`, which is a min-heap by default.

2. **Processing Stations:**
   - For each station, calculate the distance to it from the current position.
   - If the current fuel is insufficient to reach the next station, refuel using the maximum available fuel from previously passed stations (managed by the heap).
   - Update the fuel and position after reaching the station and push the station's fuel into the heap.

3. **Final Check:**
   - After processing all stations, the car should either have enough fuel to reach the target or determine that it is impossible to reach it.

### Complexity Analysis

- **Time Complexity:** 
  - The time complexity is \(O(n \log n)\), where \(n\) is the number of stations. Each station is processed once, and each operation with the heap (push and pop) takes \(O(\log n)\).

- **Space Complexity:**
  - The space complexity is \(O(n)\) due to the storage requirements for the heap and the additional space needed to store station information.

This approach ensures that we efficiently manage the refueling process to minimize the number of refueling stops required to reach the destination.
