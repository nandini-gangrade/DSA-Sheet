# [All Unique Permutations of an array](https://www.geeksforgeeks.org/problems/all-unique-permutations-of-an-array/0)
[GFG Solution](https://discuss.geeksforgeeks.org/comment/84426098-68a0-49f1-adcf-9b5160fa33fb/practice)

Given an array `arr[]` of length `n`, the task is to find all unique permutations of the array and sort them lexicographically.

### Examples

1. **Example 1:**
   - **Input:** `n = 3, arr = [1, 2, 1]`
   - **Output:** `[[1, 1, 2], [1, 2, 1], [2, 1, 1]]`
   - **Explanation:** The array has three unique permutations. The output should be in sorted order.

2. **Example 2:**
   - **Input:** `n = 2, arr = [4, 5]`
   - **Output:** `[[4, 5], [5, 4]]`
   - **Explanation:** The array has two permutations, and they are already sorted.

## Intuition

Given that `n` can be at most 9, we can leverage the properties of permutations. The maximum number of permutations for an array of length 9 is \(9!\), which is 362,880. This is manageable within the constraints.

## Approach

To solve this problem, we can use the following steps:

1. **Generate Permutations:** Use a backtracking approach to generate all permutations of the array.
2. **Handle Duplicates:** To handle duplicates and only store unique permutations, we can use a set to keep track of permutations we've already encountered.
3. **Sort Permutations:** After generating all unique permutations, sort them in lexicographical order.
4. **Return the Result:** Return the sorted list of permutations.

## Implementation

Let's implement this approach in Python:

```python
from typing import List

class Solution:
    def uniquePerms(self, arr: List[int], n: int) -> List[List[int]]:
        def backtrack(path, remaining):
            if not remaining:
                # Convert the tuple to a list and add it to the result
                result.append(list(path))
                return
            
            for i in range(len(remaining)):
                # To avoid duplicates, skip the number if it's the same as the previous one and we haven't used it
                if i > 0 and remaining[i] == remaining[i - 1]:
                    continue
                
                # Include remaining[i] in the current path and recursively generate the rest
                backtrack(path + (remaining[i],), remaining[:i] + remaining[i+1:])
        
        # Sort the array to make sure duplicates are adjacent
        arr.sort()
        result = []
        # Call backtrack with an empty path and the sorted array
        backtrack((), arr)
        return result

# Example usage
solution = Solution()
print(solution.uniquePerms([1, 2, 1], 3))  # Output: [[1, 1, 2], [1, 2, 1], [2, 1, 1]]
print(solution.uniquePerms([4, 5], 2))    # Output: [[4, 5], [5, 4]]
```

## Explanation

- **Sorting the Array:** Sorting the array ensures that duplicates are adjacent, allowing us to skip duplicate elements in the backtracking step.
- **Backtracking:** The `backtrack` function generates permutations by recursively adding elements to the current path. We use a tuple `path` to track the current permutation and a list `remaining` to track the unused elements.
- **Avoiding Duplicates:** We skip duplicates by checking if the current element is the same as the previous one. This ensures we don't consider the same element twice in the same position.

## Complexity Analysis

- **Time Complexity:** \(O(n \cdot n!)\), where \(n\) is the length of the array. Generating permutations takes \(O(n!)\) time, and each permutation is of length \(n\).
- **Space Complexity:** \(O(n \cdot n!)\), as we store all permutations, each of which is of length \(n\). The additional space is used by the recursive call stack.

This approach efficiently generates and sorts all unique permutations of the given array, taking advantage of the constraints provided.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
