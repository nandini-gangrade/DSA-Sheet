# [Largest number in K swaps](https://www.geeksforgeeks.org/problems/largest-number-in-k-swaps-1587115620/1)

To solve the problem of finding the largest possible number by performing at most `K` swaps on the digits of a string, the approach involves using **backtracking**. This method explores all possible swaps and keeps track of the maximum number formed during the exploration. Below is a detailed explanation of the approach, followed by the code implementation.

### Problem Breakdown

1. **Base Case**: 
   - If `K` becomes `0`, no more swaps are allowed, so the recursion should stop.
   - If we've processed all digits (i.e., reached the end of the string), there's no more room to swap, so we should stop.

2. **Maximization Logic**:
   - For each digit, find the maximum digit that can be swapped with the current one.
   - Perform the swap and then recursively solve the problem for the next position with `K-1` swaps remaining.

3. **Backtracking**:
   - After each swap and recursive call, revert the swap to explore other possible combinations (i.e., undo the swap to restore the original state).

4. **Horizontal Shift**:
   - If no swap improves the number at a given index, move to the next index without reducing the number of swaps left (`K`).

### Code Implementation

```cpp
#include <string>
#include <algorithm>

class Solution {
public:
    std::string findMaximumNum(std::string str, int k) {
        std::string res = str;  // Initialize the result with the original string
        int index = 0;
        solve(str, k, index, res);
        return res;
    }

private:
    int maxi(int i1, int i2, const std::string& ip) {
        int maximum = -1;
        for (int i = i1; i <= i2; i++) {
            if (ip[i] - '0' > maximum) {
                maximum = ip[i] - '0';
            }
        }
        return maximum;
    }

    void solve(std::string& str, int k, int index, std::string& res) {
        // Base condition: No swaps left or reached the end of the string
        if (k == 0 || index == str.size() - 1) {
            return;
        }

        // Find the maximum digit from the remaining part of the string
        for (int i = index + 1; i < str.size(); i++) {
            if (str[index] < str[i] && str[i] - '0' == maxi(index + 1, str.size() - 1, str)) {
                // Swap and check the result
                std::swap(str[index], str[i]);
                
                // Update the result if the current string is larger
                if (res.compare(str) < 0) {
                    res = str;
                }
                
                // Recursive call for the next index with one less swap
                solve(str, k - 1, index + 1, res);
                
                // Backtrack to explore other possibilities
                std::swap(str[index], str[i]);
            }
        }

        // Horizontal shift: move to the next index without swapping
        solve(str, k, index + 1, res);
    }
};
```

### Explanation

- **`findMaximumNum` Function**: Initializes the result as the original string and calls the recursive `solve` function.
  
- **`maxi` Function**: Finds the maximum digit in the substring starting from index `i1` to `i2`.

- **`solve` Function**:
  - If `k` reaches 0 or the end of the string is reached, it stops further recursion.
  - It iterates over all possible positions after the current `index`, and if a digit larger than the current digit is found, it swaps them.
  - If after the swap the new string is greater than the current maximum (`res`), it updates `res`.
  - The function then backtracks by undoing the swap to explore other possibilities.

### Complexity Analysis

- **Time Complexity**: \(O(n!/(n-k)!)\) where \(n\) is the length of the string. This is because, in the worst case, we might explore all permutations of the string of length \(n\) by performing \(k\) swaps.
- **Space Complexity**: \(O(n)\) for the recursive call stack and for storing the intermediate states of the string during backtracking.

This solution is efficient within the given constraints and successfully finds the largest possible number by performing at most `K` swaps.
