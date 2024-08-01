# [496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/)

To solve the problem of finding the next greater element efficiently, we can use a stack to keep track of the elements for which we haven't yet found the next greater element. This approach will allow us to solve the problem in \(O(n)\) time, where \(n\) is the length of `nums2`.

## Approach

1. **Use a Stack**: We'll use a stack to help find the next greater element. As we iterate through `nums2`, we'll maintain the stack such that the top of the stack is the last number for which we haven't found a next greater element.

2. **Map for Next Greater Elements**: We'll create a dictionary (`next_greater_map`) to store the next greater element for each number in `nums2`.

3. **Iterate through `nums2`**:
   - For each number, if the stack is not empty and the current number is greater than the number represented by the index on top of the stack, then the current number is the next greater element for that number. We'll pop the stack and update the map.
   - Push the current number onto the stack.

4. **Result Construction**: For each element in `nums1`, use the map to get the next greater element. If an element doesn't have a next greater element, it will not be in the map, and we'll return `-1` for it.

Here's the implementation in Python:

```python
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        # Dictionary to hold the next greater element for each element in nums2
        next_greater_map = {}
        stack = []

        # Iterate over nums2 to fill the next_greater_map
        for num in nums2:
            while stack and stack[-1] < num:
                # If the current number is greater than the top of the stack
                # it means the current number is the next greater for stack top
                next_greater_map[stack.pop()] = num
            stack.append(num)

        # If no next greater is found for any element in the stack, it remains -1
        while stack:
            next_greater_map[stack.pop()] = -1

        # Prepare the result for nums1 using the map
        return [next_greater_map[num] for num in nums1]

# Example usage
solution = Solution()
print(solution.nextGreaterElement([4, 1, 2], [1, 3, 4, 2]))  # Output: [-1, 3, -1]
print(solution.nextGreaterElement([2, 4], [1, 2, 3, 4]))     # Output: [3, -1]
```

### Explanation

- **Stack Usage**: As we iterate over `nums2`, we push each element onto the stack. Before pushing, we check if the current element is greater than the element corresponding to the top of the stack. If it is, we pop elements from the stack, since we have found the next greater element for these.

- **Map Construction**: We construct the `next_greater_map` in one pass over `nums2`. Each time we pop from the stack, it means we've found the next greater element for that popped element.

- **Result Construction**: Finally, we simply look up each element of `nums1` in the `next_greater_map` to build the result list.

## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the length of `nums2`. Each element is pushed and popped from the stack at most once.
- **Space Complexity**: \(O(n)\), due to the stack and the map that stores the next greater element for each element in `nums2`.

This solution efficiently finds the next greater element for each element in `nums1` using the above strategy, leveraging a stack and a map for fast lookups.
