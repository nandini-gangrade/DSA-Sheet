# [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)
[LeetCode Solution](https://leetcode.com/problems/largest-rectangle-in-histogram/solutions/5540315/best-solution-challenge-day-3-revisewitharsh)

Given an array `heights` representing the heights of bars in a histogram where the width of each bar is 1, your task is to find the area of the largest rectangle that can be formed in this histogram.

## Intuition

To solve this problem efficiently, we need to maximize the area of rectangles that can be formed. The height of the rectangle is determined by the shortest bar in the histogram within the rectangle. Therefore, we need to find a way to efficiently calculate the maximum area that can be formed with each bar as the smallest bar (or height) of the rectangle.

## Approach

The most efficient approach to solve this problem is to use a stack-based method. This approach ensures that each bar is processed in constant time, resulting in an overall time complexity of \(O(n)\).

1. **Use a Stack to Keep Track of Bars:**
   - Iterate through the heights array and use a stack to keep track of indices of the bars in increasing order of heights.
   - When a bar with a smaller height than the bar represented by the index at the top of the stack is encountered, pop from the stack. The popped bar is the height of the largest rectangle that ends with this bar.
   - The width of this rectangle is determined by the difference between the current index and the index from the new top of the stack after popping.
   - Continue this until the stack is empty or the height of the current bar is greater than the height of the bar at the top of the stack.
   - Push the current index onto the stack.

2. **Process Remaining Bars:**
   - After processing all bars in the heights array, there may still be indices left in the stack. These bars form rectangles that extend to the end of the histogram.

## Code

```python []
from typing import List

class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        max_area = 0
        index = 0
        
        while index < len(heights):
            if not stack or heights[index] >= heights[stack[-1]]:
                stack.append(index)
                index += 1
            else:
                top_of_stack = stack.pop()
                area = (heights[top_of_stack] * 
                        ((index - stack[-1] - 1) if stack else index))
                max_area = max(max_area, area)
        
        while stack:
            top_of_stack = stack.pop()
            area = (heights[top_of_stack] * 
                    ((index - stack[-1] - 1) if stack else index))
            max_area = max(max_area, area)
        
        return max_area
```

```cpp []
#include <vector>
#include <stack>
#include <algorithm>

class Solution {
public:
    int largestRectangleArea(std::vector<int>& heights) {
        std::stack<int> s;
        int max_area = 0;
        int index = 0;
        
        while (index < heights.size()) {
            if (s.empty() || heights[index] >= heights[s.top()]) {
                s.push(index++);
            } else {
                int top_of_stack = s.top();
                s.pop();
                int area = heights[top_of_stack] * (s.empty() ? index : index - s.top() - 1);
                max_area = std::max(max_area, area);
            }
        }
        
        while (!s.empty()) {
            int top_of_stack = s.top();
            s.pop();
            int area = heights[top_of_stack] * (s.empty() ? index : index - s.top() - 1);
            max_area = std::max(max_area, area);
        }
        
        return max_area;
    }
};
```

```java []
import java.util.Stack;

class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int index = 0;
        
        while (index < heights.length) {
            if (stack.isEmpty() || heights[index] >= heights[stack.peek()]) {
                stack.push(index++);
            } else {
                int topOfStack = stack.pop();
                int area = heights[topOfStack] * (stack.isEmpty() ? index : index - stack.peek() - 1);
                maxArea = Math.max(maxArea, area);
            }
        }
        
        while (!stack.isEmpty()) {
            int topOfStack = stack.pop();
            int area = heights[topOfStack] * (stack.isEmpty() ? index : index - stack.peek() - 1);
            maxArea = Math.max(maxArea, area);
        }
        
        return maxArea;
    }
}
```

```javascript []
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function(heights) {
    let stack = [];
    let maxArea = 0;
    let index = 0;
    
    while (index < heights.length) {
        // If stack is empty or current bar is higher than the bar at stack's top
        if (stack.length === 0 || heights[index] >= heights[stack[stack.length - 1]]) {
            stack.push(index++);
        } else {
            // Pop the top bar from stack and calculate the area
            let topOfStack = stack.pop();
            let area = heights[topOfStack] * (stack.length === 0 ? index : index - stack[stack.length - 1] - 1);
            maxArea = Math.max(maxArea, area);
        }
    }
    
    // Process remaining bars in stack
    while (stack.length > 0) {
        let topOfStack = stack.pop();
        let area = heights[topOfStack] * (stack.length === 0 ? index : index - stack[stack.length - 1] - 1);
        maxArea = Math.max(maxArea, area);
    }
    
    return maxArea;
};

```


### Complexity

- **Time Complexity:** \(O(n)\). Each bar is pushed and popped from the stack exactly once.
- **Space Complexity:** \(O(n)\). The stack may store up to `n` indices.

### Summary

The stack-based approach provides an efficient way to solve the problem of finding the largest rectangle in a histogram, with an overall time complexity of \(O(n)\) and space complexity of \(O(n)\). This approach is implemented in Python, C++, Java, and JavaScript to cater to different programming environments.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
