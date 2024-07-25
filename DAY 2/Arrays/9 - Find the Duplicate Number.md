# 287. Find the Duplicate Number
[LeetCode Solution](https://leetcode.com/problems/find-the-duplicate-number/solutions/5528716/best-solution-challenge-day-2-revisewitharsh/)

Given an array `nums` containing \(n + 1\) integers where each integer is in the range \([1, n]\), find the duplicate number. The duplicate number is guaranteed to exist.

### Examples

**Example 1:**

- **Input:** `nums = [1,3,4,2,2]`
- **Output:** `2`
- **Explanation:** The number `2` is repeated.

**Example 2:**

- **Input:** `nums = [3,1,3,4,2]`
- **Output:** `3`
- **Explanation:** The number `3` is repeated.

**Example 3:**

- **Input:** `nums = [3,3,3,3,3]`
- **Output:** `3`
- **Explanation:** The number `3` is repeated multiple times.

### Constraints

- \(1 \leq n \leq 10^5\)
- `nums.length == n + 1`
- \(1 \leq \text{nums}[i] \leq n\)
- All numbers appear only once except for one, which appears at least twice.

## Intuition

Since the numbers are in the range \([1, n]\) and the array has \(n + 1\) integers, there must be at least one number that repeats due to the pigeonhole principle. The challenge is to find this duplicate without modifying the array and using only constant extra space.

## Approach

We can solve this problem by treating the array as a linked list where the value at each index points to the next node in the list. This setup creates a cycle because there is one repeated number. The problem then becomes one of detecting the cycle, which can be efficiently done using Floyd's Tortoise and Hare algorithm.

**Floyd’s Tortoise and Hare Algorithm:**

1. **Initialize Two Pointers:**
   - Use two pointers, `tortoise` and `hare`. Initially, both start at the first element of the array.

2. **Finding the Intersection Point:**
   - Move `tortoise` one step at a time: `tortoise = nums[tortoise]`.
   - Move `hare` two steps at a time: `hare = nums[nums[hare]]`.
   - Continue until they meet, which indicates a cycle.

3. **Finding the Entrance to the Cycle:**
   - Reset `tortoise` to the beginning of the list, while `hare` remains at the meeting point.
   - Move both pointers one step at a time: `tortoise = nums[tortoise]` and `hare = nums[hare]`.
   - The point at which they meet is the start of the cycle, which is the duplicate number.

## Code

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        # Step 1: Find the intersection point
        tortoise = nums[0]
        hare = nums[0]
        
        # Move tortoise by 1 step and hare by 2 steps until they meet
        while True:
            tortoise = nums[tortoise]
            hare = nums[nums[hare]]
            if tortoise == hare:
                break
        
        # Step 2: Find the entrance to the cycle
        tortoise = nums[0]
        while tortoise != hare:
            tortoise = nums[tortoise]
            hare = nums[hare]
        
        return hare
```

## Complexity Analysis

- **Time Complexity:** \(O(n)\)  
  The algorithm runs in linear time because both the cycle detection and finding the entrance to the cycle involve simple linear traversals of the array.

- **Space Complexity:** \(O(1)\)  
  The solution uses only constant extra space, as it only maintains a few pointers.

This approach efficiently identifies the duplicate number by leveraging the properties of cycle detection, without needing to modify the input array or use extra space.

---

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/find-the-duplicate-number/solutions/5528716/best-solution-challenge-day-2-revisewitharsh/) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀
`
