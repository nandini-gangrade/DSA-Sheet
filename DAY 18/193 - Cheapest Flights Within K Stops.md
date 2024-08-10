# [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/description/)

To solve the problem of finding the cheapest price from a source city (`src`) to a destination city (`dst`) with at most `k` stops using flights, we can use a modified version of the Breadth-First Search (BFS) algorithm, often referred to as a BFS-based approach or Dijkstra's algorithm with a priority queue. However, in this problem, the BFS approach is more appropriate due to the need to limit the number of stops.

### Approach

1. **Graph Representation**:
   - We represent the graph using an adjacency list, where each city points to its neighboring cities along with the cost of the flight to those neighbors.

2. **Breadth-First Search (BFS) with Priority Queue**:
   - Use a priority queue (min-heap) to explore the cities, prioritizing the paths with the lowest cost first.
   - Each entry in the priority queue will store the current cost, the current city, and the number of stops made so far.
   - As we explore the cities, we check if we have reached the destination city (`dst`). If so, we return the current cost.
   - If the number of stops exceeds `k`, we do not continue exploring from that city.

3. **Edge Cases**:
   - If the `src` is the same as `dst`, the cost is `0`.
   - If no valid route exists within the given constraints, return `-1`.

### Code Implementation

```cpp
#include <vector>
#include <queue>
#include <unordered_map>
#include <climits>

using namespace std;

class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        // Create the adjacency list for the graph
        unordered_map<int, vector<pair<int, int>>> adj;
        for (auto& flight : flights) {
            int u = flight[0], v = flight[1], price = flight[2];
            adj[u].push_back({v, price});
        }

        // Priority queue (min-heap) to store (cost, current city, stops)
        priority_queue<vector<int>, vector<vector<int>>, greater<vector<int>>> pq;
        pq.push({0, src, 0}); // {cost, city, stops}

        // Array to store the minimum cost to reach each city with a certain number of stops
        vector<vector<int>> minCost(n, vector<int>(k + 2, INT_MAX));
        minCost[src][0] = 0;

        while (!pq.empty()) {
            auto current = pq.top();
            pq.pop();
            int cost = current[0];
            int city = current[1];
            int stops = current[2];

            // If the destination is reached with the allowed stops, return the cost
            if (city == dst) {
                return cost;
            }

            // If the number of stops exceeds k, we can't continue from this point
            if (stops > k) {
                continue;
            }

            // Explore neighboring cities
            for (auto& [nextCity, price] : adj[city]) {
                int newCost = cost + price;
                if (newCost < minCost[nextCity][stops + 1]) {
                    minCost[nextCity][stops + 1] = newCost;
                    pq.push({newCost, nextCity, stops + 1});
                }
            }
        }

        return -1; // If no route is found within the constraints
    }
};
```

### Explanation

- **Graph Construction**: We first create an adjacency list to represent the flight connections between cities.
  
- **Priority Queue**: 
  - We use a priority queue to explore paths, prioritizing the cheapest path first.
  - Each element in the queue is a triplet `(current cost, current city, number of stops)`.

- **BFS Exploration**:
  - We explore the neighboring cities from the current city.
  - If the current city is the destination city (`dst`) and we have not exceeded the allowed number of stops, we return the current cost.
  - If we exceed `k` stops, we stop exploring further from that city.

- **Tracking Costs**: 
  - We maintain a `minCost` table to keep track of the minimum cost to reach each city with a certain number of stops. This helps in pruning unnecessary paths and ensuring that we don't explore more costly paths.

- **Return**:
  - If we find a valid path within the constraints, we return its cost.
  - If no such path is found, we return `-1`.

### Time and Space Complexity

- **Time Complexity**: `O(E + n log n)`, where `E` is the number of flights. The priority queue operations and BFS traversal dictate this complexity.
- **Space Complexity**: `O(n * k)`, due to the storage required for the `minCost` table.

This approach efficiently finds the cheapest flight route with at most `k` stops, making it suitable for this problem's constraints.
