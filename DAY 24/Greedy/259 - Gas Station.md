# [134. Gas Station](https://leetcode.com/problems/gas-station/description/)

To solve this problem, the goal is to determine whether you can complete the entire circular journey starting from any gas station, and if so, return the index of the starting gas station.

### Key Insights:
1. **Total Gas and Cost**:
   - If the total amount of gas available in all stations (`sum(gas)`) is less than the total amount of gas required to travel between the stations (`sum(cost)`), it is **impossible** to complete the journey. In this case, the result will be `-1`.
   
2. **Greedy Approach**:
   - Even if the total gas is enough to cover the total cost, starting at the wrong station might cause you to run out of gas mid-journey. Therefore, the key observation here is to track local failures.
   - If you fail at some station (i.e., you run out of gas), it means that starting from any station before this point would also fail. Thus, the next potential starting point should be the station immediately after the failure.

### Algorithm:
1. **Track Total and Current Gas**:
   - Maintain two variables: `total_tank` (to track if there's enough gas for the entire trip) and `current_tank` (to track the gas left while traveling from one station to the next).
   
2. **Check Feasibility**:
   - Traverse through the gas stations:
     - At each station, update `current_tank` (the remaining gas after reaching the next station). If `current_tank` becomes negative, it indicates that starting from the current starting point isn't possible.
     - Reset `current_tank` to 0 and set the next station as the new potential starting point.
   
3. **Final Check**:
   - If the total gas (`total_tank`) is greater than or equal to the total cost, then a solution exists, and the last valid starting station is returned. Otherwise, return `-1`.

### Code Implementation:

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        total_tank, current_tank = 0, 0
        start_station = 0
        
        for i in range(len(gas)):
            total_tank += gas[i] - cost[i]
            current_tank += gas[i] - cost[i]
            
            # If current_tank is negative, we cannot start from the previous start_station
            if current_tank < 0:
                # Set the new starting station
                start_station = i + 1
                # Reset current_tank
                current_tank = 0
        
        # If total_tank is negative, it's impossible to complete the circuit
        return start_station if total_tank >= 0 else -1
```

### Explanation:

1. **Initialization**:
   - `total_tank`: This keeps track of the overall surplus or deficit of gas after accounting for costs.
   - `current_tank`: This keeps track of the gas available in the current segment of the journey.
   - `start_station`: This tracks the potential starting point for the journey.

2. **Main Loop**:
   - For each station `i`, we calculate the difference between gas and cost (`gas[i] - cost[i]`), and add this to both `total_tank` and `current_tank`.
   - If `current_tank` goes negative, it means we can't reach station `i` from the current starting point, so we move the starting point to `i + 1` and reset `current_tank`.

3. **Final Check**:
   - If `total_tank` is negative, it means there isn't enough gas overall to complete the journey, so we return `-1`.
   - Otherwise, we return the `start_station`, which will be the valid starting point that allows the car to complete the journey.

### Time Complexity:
- **O(n)**: We only traverse the `gas` and `cost` arrays once.

### Space Complexity:
- **O(1)**: We only use a few extra variables (`total_tank`, `current_tank`, `start_station`), so the space complexity is constant.

### Example Walkthrough:

#### Example 1:
```plaintext
gas  = [1, 2, 3, 4, 5]
cost = [3, 4, 5, 1, 2]
```
- Starting at station `3` (index 3):
  - Initial tank = `0 + 4 = 4` units of gas.
  - Travel to station 4: tank = `4 - 1 + 5 = 8`.
  - Travel to station 0: tank = `8 - 2 + 1 = 7`.
  - Travel to station 1: tank = `7 - 3 + 2 = 6`.
  - Travel to station 2: tank = `6 - 4 + 3 = 5`.
  - Travel back to station 3: tank = `5 - 5 = 0` (just enough gas).
  
Result: Starting at index `3` works, so return `3`.

#### Example 2:
```plaintext
gas  = [2, 3, 4]
cost = [3, 4, 3]
```
- Try starting at any station:
  - Start at station 2 (index 2): tank becomes negative at station 1, so it is impossible.
  
Result: No valid solution, so return `-1`.
