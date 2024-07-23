# [169. Majority Element](https://leetcode.com/problems/majority-element/description/)
[Leetcode](https://leetcode.com/problems/majority-element/solutions/5525064/best-solution-challenge-day-1-revisewitharsh)

You are given an array `nums` of size `n`. You need to return the majority element, which is defined as the element that appears more than ⌊n / 2⌋ times. You can assume that the majority element always exists in the array.

### Examples

**Example 1:**

- **Input:**  
  `nums = [3, 2, 3]`
  
- **Output:**  
  `3`

**Example 2:**

- **Input:**  
  `nums = [2, 2, 1, 1, 1, 2, 2]`
  
- **Output:**  
  `2`

### Constraints

- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

## Intuition

The majority element appears more than ⌊n / 2⌋ times, which means that it occupies more than half of the array. If we were to "cancel out" each occurrence of the majority element with a different element, the majority element would still remain. The Boyer-Moore Voting Algorithm exploits this property to identify the majority element with a single pass through the array.

## Approach

1. **Initialize Variables:**
   - `count`: This will track the net count of the current candidate for the majority element.
   - `candidate`: This will store the potential majority element.

2. **Iterate Through the Array:**
   - If `count` is 0, update the `candidate` to the current element.
   - If the current element is the same as the `candidate`, increment `count`.
   - Otherwise, decrement `count`.

3. **Return the Candidate:**
   - After one pass through the array, the `candidate` will be the majority element.

## Code

Here is the implementation of the Boyer-Moore Voting Algorithm:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = 0
        candidate = None

        for num in nums:
            if count == 0:
                candidate = num
            count += (1 if num == candidate else -1)

        return candidate
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm makes a single pass through the array, resulting in linear time complexity.

- **Space Complexity:** \(O(1)\)  
  The algorithm uses a constant amount of additional space, independent of the input size.

This efficient solution takes advantage of the properties of the majority element to determine the answer in linear time with minimal space usage.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/majority-element/solutions/5525064/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

`Let's tackle these coding challenges together! 🚀
`
