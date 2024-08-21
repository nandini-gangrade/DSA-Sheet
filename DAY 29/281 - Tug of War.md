# [Tug of War](https://www.geeksforgeeks.org/tug-of-war/)

The problem you're describing is known as the "Tug of War" problem, where the goal is to divide a set of integers into two subsets such that the absolute difference between their sums is minimized. Let's break down the approach to solve this problem using a backtracking algorithm.

### Problem Description
Given a set of `n` integers:
- If `n` is even, divide the set into two subsets of size `n/2` each.
- If `n` is odd, divide the set into two subsets with sizes `(n-1)/2` and `(n+1)/2`.

The objective is to minimize the absolute difference between the sums of the two subsets.

### Approach

#### 1. **Backtracking Algorithm**:
   - Use a recursive function to explore all possible ways of dividing the set.
   - At each step, decide whether to include the current element in the first subset.
   - If the first subset reaches the required size, calculate the difference between the sums of the two subsets.
   - Keep track of the minimum difference found.

#### 2. **Base Case**:
   - When the first subset reaches the required size, compute the sum of both subsets and update the minimum difference if this partitioning is better.

#### 3. **Pruning**:
   - If at any point the current difference is greater than or equal to the current best difference, prune the search (i.e., do not continue exploring this branch).

### Implementation

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <climits>

using namespace std;

void tugOfWarUtil(vector<int>& arr, int n, vector<int>& currSet, int currSum, int currSize, int totalSum, vector<int>& bestSet, int& minDiff, int targetSize, int startIndex) {
    // Base case: if current set has reached the target size
    if (currSize == targetSize) {
        int otherSum = totalSum - currSum;
        int diff = abs(currSum - otherSum);

        if (diff < minDiff) {
            minDiff = diff;
            bestSet = currSet;
        }
        return;
    }

    // Recursive case: try including elements in the current set
    for (int i = startIndex; i < n; ++i) {
        currSet.push_back(arr[i]);
        tugOfWarUtil(arr, n, currSet, currSum + arr[i], currSize + 1, totalSum, bestSet, minDiff, targetSize, i + 1);
        currSet.pop_back(); // backtrack
    }
}

void tugOfWar(vector<int>& arr) {
    int n = arr.size();
    int totalSum = 0;
    for (int num : arr) {
        totalSum += num;
    }

    vector<int> currSet, bestSet;
    int minDiff = INT_MAX;

    int targetSize = n / 2;

    tugOfWarUtil(arr, n, currSet, 0, 0, totalSum, bestSet, minDiff, targetSize, 0);

    // Print the two subsets
    vector<int> subset1 = bestSet;
    vector<int> subset2;

    for (int num : arr) {
        if (find(subset1.begin(), subset1.end(), num) == subset1.end()) {
            subset2.push_back(num);
        }
    }

    cout << "Subset 1: ";
    for (int num : subset1) {
        cout << num << " ";
    }
    cout << endl;

    cout << "Subset 2: ";
    for (int num : subset2) {
        cout << num << " ";
    }
    cout << endl;

    cout << "Minimum Difference: " << minDiff << endl;
}

int main() {
    vector<int> arr = {3, 4, 5, -3, 100, 1, 89, 54, 23, 20};
    tugOfWar(arr);
    return 0;
}
```

### Explanation

1. **tugOfWarUtil Function**:
   - This is a recursive utility function that explores all possible combinations of elements to form one of the subsets (`currSet`).
   - It keeps track of the sum of elements in `currSet` and the number of elements added (`currSize`).
   - Once `currSet` reaches the target size, the difference between the sum of this subset and the other subset is calculated and compared to the minimum difference found so far (`minDiff`).

2. **tugOfWar Function**:
   - Initializes the recursion by calling `tugOfWarUtil`.
   - After finding the best subset (`bestSet`), it constructs the second subset by excluding the elements of `bestSet` from the original array.
   - Finally, it prints the two subsets and the minimum difference.

### Complexity Analysis

- **Time Complexity**: The algorithm explores all possible ways to partition the array into two subsets. The number of possible partitions is exponential, specifically \( O(2^n) \), where \( n \) is the size of the array. However, the recursive backtracking approach prunes many of these possibilities, making it efficient for small inputs.
  
- **Space Complexity**: The space complexity is \( O(n) \) due to the recursion stack and the space required to store the subsets.

This approach efficiently solves the "Tug of War" problem for small to medium-sized arrays. For larger arrays, more advanced optimization techniques like dynamic programming might be necessary.
