# [974. Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/description/)
[LeetCode Solution](https://leetcode.com/problems/subarray-sums-divisible-by-k/solutions/3071714/easy-video-explaination-step-by-step-explanation-challenge-day-2-revisewitharsh)

To solve the problem of finding the number of non-empty subarrays with a sum divisible by \(k\), we can use the prefix sum and remainder counting technique. This approach leverages the properties of prefix sums and modular arithmetic to efficiently count the number of such subarrays.

### Examples

**Example 1:**

- **Input:** `nums = [4,5,0,-2,-3,1]`, `k = 5`
- **Output:** `7`
- **Explanation:** There are 7 subarrays with a sum divisible by \(k = 5\):
  - `[4, 5, 0, -2, -3, 1]`
  - `[5]`
  - `[5, 0]`
  - `[5, 0, -2, -3]`
  - `[0]`
  - `[0, -2, -3]`
  - `[-2, -3]`

**Example 2:**

- **Input:** `nums = [5]`, `k = 9`
- **Output:** `0`

### Constraints

- \(1 \leq \text{nums.length} \leq 3 \times 10^4\)
- \(-10^4 \leq \text{nums}[i] \leq 10^4\)
- \(2 \leq k \leq 10^4\)

## Intuition

The idea is to use prefix sums to efficiently determine subarray sums. A subarray sum is divisible by \(k\) if the prefix sum up to the end of the subarray, modulo \(k\), is equal to the prefix sum up to the start of the subarray, modulo \(k\). This means the difference between the two prefix sums is divisible by \(k\).

## Approach

1. **Initialize a variable `count` to zero**: This will store the number of subarrays with sums divisible by \(k\).

2. **Initialize a variable `prefix_sum` to zero**: This will keep track of the cumulative sum of elements as we iterate through the array.

3. **Use a hashmap `remainder_count`**: This will store the frequency of each remainder when the `prefix_sum` is divided by \(k\).

4. **Iterate over the array `nums`**:
   - Update `prefix_sum` by adding the current element.
   - Compute the remainder of `prefix_sum` modulo \(k\). To handle negative remainders, adjust the remainder to be non-negative by using \((\text{remainder} + k) \% k\).
   - If the remainder is zero, it means the current subarray sum is divisible by \(k\), so increment `count`.
   - If the remainder exists in `remainder_count`, it means there are subarrays ending at the current index whose sums are divisible by \(k\). Add the count of such remainders to `count`.
   - Update `remainder_count` for the current remainder.

5. **Return the total `count`**.

## Code

```python
from collections import defaultdict

class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        count = 0  # Initialize the count of subarrays
        prefix_sum = 0  # Initialize the prefix sum
        remainder_count = defaultdict(int)  # Defaultdict for storing remainder counts
        
        remainder_count[0] = 1  # To handle subarrays starting from index 0

        for num in nums:
            prefix_sum += num  # Update the prefix sum
            remainder = (prefix_sum % k + k) % k  # Calculate the remainder
            
            if remainder in remainder_count:
                count += remainder_count[remainder]  # Add to count if remainder is found
            
            remainder_count[remainder] += 1  # Increment the count of this remainder

        return count  # Return the total count of subarrays
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm makes a single pass through the `nums` array, performing constant-time operations for each element.

- **Space Complexity:** \(O(k)\)  
  The space complexity is due to the hashmap storing at most \(k\) different remainders.
