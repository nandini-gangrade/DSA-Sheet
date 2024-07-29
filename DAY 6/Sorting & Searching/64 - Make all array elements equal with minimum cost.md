# [Make all array elements equal with minimum cost](https://www.geeksforgeeks.org/make-array-elements-equal-minimum-cost/)

To solve the problem of minimizing the cost of making all elements in an array equal to a single integer, where the cost is given by the absolute difference between the elements and the target value, we can leverage the following observations:

1. **Understanding the Cost Function:**
   The cost of changing all elements in the array to a target value \( t \) is computed as:
   \[
   \text{Cost} = \sum_{i=1}^{n} |arr[i] - t|
   \]
   This function is a U-shaped curve with respect to \( t \). As \( t \) increases, the cost decreases to a certain point and then starts to increase. This is because moving \( t \) closer to the median of the array minimizes the sum of absolute differences.

2. **Optimal Target Value:**
   To minimize the cost, the target value \( t \) should ideally be the median of the array. The median minimizes the sum of absolute deviations from the center. Hence, the median is the best candidate for the target value to minimize cost.

3. **Steps to Solve:**
   - **Sort the Array:** To find the median.
   - **Find the Median:** Depending on whether the number of elements is odd or even, the median can be a single value (if odd) or any value between the two middle elements (if even).
   - **Calculate the Cost:** Using the median as the target, compute the total cost.

## Code

```python
from typing import List

def minCostToEqualize(arr: List[int]) -> int:
    # Sort the array to find the median
    arr.sort()
    n = len(arr)
    
    # Find the median
    if n % 2 == 1:
        median = arr[n // 2]
    else:
        # For even number of elements, any value between the two middle values is optimal
        # Taking the lower middle value as the median
        median = arr[n // 2 - 1]
    
    # Calculate the total cost of changing all elements to the median
    cost = sum(abs(x - median) for x in arr)
    
    return cost

# Example usage
arr1 = [1, 100, 101]
arr2 = [4, 6]
print(minCostToEqualize(arr1))  # Output: 100
print(minCostToEqualize(arr2))  # Output: 2
```

## Explanation:
1. **Sorting the Array:** This ensures that we can easily access the median.
2. **Finding the Median:**
   - If the number of elements \( n \) is odd, the median is the middle element.
   - If \( n \) is even, we can use either of the two middle elements as the median. In this code, I chose the lower middle element for simplicity.
3. **Calculating the Cost:** Compute the sum of absolute differences between each element and the median.

## Complexity:
- **Time Complexity:** \(O(n \log n)\) due to sorting.
- **Space Complexity:** \(O(1)\) additional space, excluding the input and output.

This approach efficiently finds the minimum cost by leveraging the median, which is the optimal target value for minimizing the sum of absolute deviations.
