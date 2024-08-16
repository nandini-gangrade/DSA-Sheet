# [Partition Equal Subset Sum](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1)

The problem is asking whether it is possible to partition an array into two subsets such that the sum of elements in both subsets is the same. This is a variation of the **Subset Sum Problem** and can be approached using **dynamic programming**.

### Approach:

#### 1. Problem Understanding:
- If the sum of all elements is odd, it's impossible to partition the array into two subsets with equal sum (since integers can't be divided evenly into two equal integer parts).
- If the sum of all elements is even, we check if it's possible to find a subset whose sum is half of the total sum. If we can, the other subset will naturally have the same sum.

#### 2. Dynamic Programming:
We can solve this problem by reducing it to a **subset sum problem**:
- Let the total sum of the array be `S`. If `S` is odd, return `0` (as partitioning is impossible).
- If `S` is even, we need to check if there exists a subset with sum `S / 2`.

We can define a DP table where:
- `dp[i][j]` is `True` if there is a subset of the first `i` elements that sums to `j`.

The state transition will be:
- `dp[i][j] = dp[i-1][j]` (i.e., excluding the current element `arr[i-1]`) OR
- `dp[i][j] = dp[i-1][j-arr[i-1]]` (i.e., including the current element `arr[i-1]`).

The base case is:
- `dp[0][0] = True` because a sum of 0 can always be achieved with an empty subset.

### Solution:

```java
class Solution{
    static int equalPartition(int n, int arr[]){
        int sum = 0;
        
        // Calculate the total sum of elements
        for(int i = 0; i < n; i++){
            sum += arr[i];
        }
        
        // If the sum is odd, it's impossible to partition into two equal parts
        if(sum % 2 != 0) {
            return 0;
        }
        
        // We need to find if there's a subset with sum equal to sum / 2
        int target = sum / 2;
        
        // DP array where dp[j] means whether a sum j is possible with the current elements
        boolean dp[] = new boolean[target + 1];
        
        // A sum of 0 is always possible with an empty subset
        dp[0] = true;
        
        // Fill the DP array
        for(int i = 0; i < n; i++){
            // Traverse backwards to ensure we don't overwrite results for the current iteration
            for(int j = target; j >= arr[i]; j--){
                dp[j] = dp[j] || dp[j - arr[i]];
            }
        }
        
        // The answer is whether we can form the subset with sum equal to target
        return dp[target] ? 1 : 0;
    }
}
```

### Explanation:
1. **Total Sum Calculation**: We calculate the total sum of all elements in the array. If the sum is odd, we return `0` immediately because an odd sum can't be split into two equal integers.
2. **DP Array Initialization**: We use a 1D DP array `dp[]` where `dp[j]` will be `True` if there is a subset of the array that sums to `j`. Initially, `dp[0]` is set to `True` because we can always form a sum of `0` with an empty subset.
3. **Filling DP Table**: For each element in the array, we update the `dp[]` array by checking whether the current element can contribute to forming the sum `j`. We iterate the `dp[]` array backwards to avoid using the same element multiple times.
4. **Final Check**: After processing all elements, if `dp[target]` (where `target = sum / 2`) is `True`, then it's possible to partition the array into two subsets with equal sum. Otherwise, it's not.

### Time Complexity:
- The time complexity is `O(n * target)`, where `n` is the number of elements in the array, and `target` is `sum / 2`. In the worst case, `target` can be as large as `500,000` based on the constraints.

### Example Walkthrough:

#### Example 1:
Input: `arr = {1, 5, 11, 5}`
- Total sum = 22, target = 11.
- After filling the DP table, `dp[11]` will be `True`, so the output is `1` (partition possible).

#### Example 2:
Input: `arr = {1, 3, 5}`
- Total sum = 9 (odd), so partitioning is impossible. The output is `0`.

This approach efficiently checks whether partitioning the array into two subsets with equal sum is possible.
