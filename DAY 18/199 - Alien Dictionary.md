# [Alien Dictionary](https://www.geeksforgeeks.org/problems/alien-dictionary/1)

To solve the problem of finding the order of characters in an alien language given a sorted dictionary, you can use a graph-based approach, specifically Topological Sorting. Here's a detailed breakdown of the solution:

### Steps to Solve the Problem

1. **Build the Graph**:
   - Each character in the alien language can be represented as a node in a directed graph.
   - An edge from node `u` to node `v` indicates that character `u` comes before character `v` in the alien language.

2. **Determine the Order of Characters**:
   - Use the given dictionary to determine the relative order of characters.
   - For each consecutive pair of words in the dictionary, compare them to find the first character where they differ. This difference tells us the order of those characters.

3. **Topological Sort**:
   - Once the graph is built, perform a topological sort to get the order of characters. This will give us a valid ordering of characters.

4. **Handle Edge Cases**:
   - Ensure that the result is valid given the constraints of the problem.

### Detailed Solution

Here’s the implementation in C++ using the above approach:

```cpp
#include <vector>
#include <string>
#include <stack>
#include <algorithm>

using namespace std;

class Solution {
public:
    void topo(vector<int> adj[], stack<int>& st, vector<int>& vis, int src) {
        vis[src] = 1;
        for (auto it : adj[src]) {
            if (!vis[it]) {
                topo(adj, st, vis, it);
            }
        }
        st.push(src);
    }

    string findOrder(string dict[], int N, int K) {
        // Create an adjacency list and a visited array
        vector<int> adj[K];
        vector<int> vis(K, 0);
        string ans;

        // Build the graph
        for (int i = 0; i < N - 1; i++) {
            int j = 0;
            int n = dict[i].size();
            int m = dict[i + 1].size();
            int len = min(n, m);

            // Find the first different character
            while (j < len && dict[i][j] == dict[i + 1][j]) {
                j++;
            }

            // If we have found a different character, add an edge
            if (j < len) {
                adj[dict[i][j] - 'a'].push_back(dict[i + 1][j] - 'a');
            }
        }

        // Perform topological sort
        stack<int> st;
        for (int i = 0; i < K; i++) {
            if (!vis[i]) {
                topo(adj, st, vis, i);
            }
        }

        // Construct the result from the stack
        while (!st.empty()) {
            int f = st.top();
            st.pop();
            ans += (char)(f + 'a');
        }

        return ans;
    }
};
```

### Explanation of the Code

1. **Graph Construction**:
   - Build the adjacency list `adj` from the dictionary. Each time you find a differing character between two consecutive words, add a directed edge from the first differing character to the second.

2. **Topological Sorting**:
   - Use a depth-first search (DFS) approach to perform topological sorting. The `topo` function handles the DFS and populates the stack with characters in the correct order.

3. **Result Construction**:
   - Extract characters from the stack to form the final order of characters.

### Time Complexity

- **Building the Graph**: O(N * L), where N is the number of words and L is the maximum length of a word.
- **Topological Sort**: O(K + E), where K is the number of characters and E is the number of edges in the graph.

### Space Complexity

- **Graph Representation**: O(K + E)
- **Auxiliary Data Structures**: O(K), for the stack and visited array.

This solution is efficient and handles the constraints well, ensuring that the order of characters in the alien language is determined correctly.
