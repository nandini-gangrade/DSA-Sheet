# [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
[LeetCode Solution](https://leetcode.com/problems/two-sum/solutions/5525028/best-solution-challenge-day-1-revisewitharsh)

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the target. You must ensure that:
- Each input has exactly one solution.
- You may not use the same element twice.
- The answer can be returned in any order.

### Examples

**Example 1:**

- **Input:**  
  `nums = [2,7,11,15]`, `target = 9`
  
- **Output:**  
  `[0,1]`

- **Explanation:**  
  `nums[0] + nums[1] = 2 + 7 = 9`. Therefore, return `[0, 1]`.

**Example 2:**

- **Input:**  
  `nums = [3,2,4]`, `target = 6`

- **Output:**  
  `[1,2]`

- **Explanation:**  
  `nums[1] + nums[2] = 2 + 4 = 6`. Therefore, return `[1, 2]`.

**Example 3:**

- **Input:**  
  `nums = [3,3]`, `target = 6`

- **Output:**  
  `[0,1]`

- **Explanation:**  
  `nums[0] + nums[1] = 3 + 3 = 6`. Therefore, return `[0, 1]`.

### Constraints

- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- Only one valid answer exists.

## Intuition

The challenge is to find two indices in an array such that the sum of the values at those indices equals the target. A straightforward solution would involve checking all pairs of elements to see if they add up to the target, but this would result in a time complexity of \(O(n^2)\). We aim for a more efficient solution, ideally \(O(n)\), by using a hash table to store complements of the numbers we encounter.

## Approach

1. **Hash Map for Complements:**
   - Use a dictionary (hash map) to store the number needed to reach the target for each element (i.e., the complement of the current element).

2. **Iterate Through the Array:**
   - For each element `nums[i]`, calculate the complement needed to reach the target.
   - Check if the complement exists in the dictionary.
   - If it does, return the indices of the current element and the complement.
   - If it doesn't, store the current element in the dictionary with its index.

3. **Return Result:**
   - Once you find the two indices that sum to the target, return them as the result.

## Code

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Create a hash map to store the complement and its index
        num_to_index = {}
        
        # Iterate over the array
        for index, num in enumerate(nums):
            # Calculate the complement
            complement = target - num
            
            # Check if the complement exists in the map
            if complement in num_to_index:
                # Return the indices of the complement and current number
                return [num_to_index[complement], index]
            
            # Store the current number and its index in the map
            num_to_index[num] = index

        # If no solution is found, return an empty list (although guaranteed to have a solution)
        return []
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm iterates over the array once, performing constant-time operations for each element.

- **Space Complexity:** \(O(n)\)  
  The hash map stores each element in the worst case, leading to a linear space requirement.

This approach efficiently finds the indices of the two numbers that add up to the target by leveraging a hash map to quickly look up the necessary complements as we iterate through the array.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/two-sum/solutions/5525028/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
