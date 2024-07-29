# [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/)
[LeetCode Solution](https://leetcode.com/problems/spiral-matrix/solutions/5535979/step-by-step-explanation-challenge-day-3-revisewitharsh)

Given an `m x n` matrix, return all elements of the matrix in spiral order.

### Examples

**Example 1:**

- **Input:** `matrix = [[1,2,3],[4,5,6],[7,8,9]]`
- **Output:** `[1,2,3,6,9,8,7,4,5]`

**Example 2:**

- **Input:** `matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]`
- **Output:** `[1,2,3,4,8,12,11,10,9,5,6,7]`

## Intuition

To traverse the matrix in spiral order, we need to keep track of four boundaries: `top`, `bottom`, `left`, and `right`. These boundaries define the current layer of the matrix we are processing. The traversal is done in four directions: right, down, left, and up.

1. **Right:** Traverse from the left boundary to the right boundary along the top boundary.
2. **Down:** Traverse from the top boundary to the bottom boundary along the right boundary.
3. **Left:** Traverse from the right boundary to the left boundary along the bottom boundary.
4. **Up:** Traverse from the bottom boundary to the top boundary along the left boundary.

After processing each direction, adjust the boundaries and switch the direction.

## Approach

1. **Initialize Variables:**
   - `result` to store the spiral order of elements.
   - Boundaries: `top`, `bottom`, `left`, `right` to define the current layer.
   - `dir` to keep track of the current direction (0: right, 1: down, 2: left, 3: up).

2. **Traversal Logic:**
   - Traverse in the current direction.
   - Update the boundary that has been processed.
   - Switch to the next direction.
   - Continue until all elements are visited.

## Code

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result = []
        if not matrix:
            return result
        
        m, n = len(matrix), len(matrix[0])
        top, bottom, left, right = 0, m - 1, 0, n - 1
        dir = 0  # 0: right, 1: down, 2: left, 3: up
        
        while top <= bottom and left <= right:
            if dir == 0:  # Going right
                for j in range(left, right + 1):
                    result.append(matrix[top][j])
                top += 1
            elif dir == 1:  # Going down
                for i in range(top, bottom + 1):
                    result.append(matrix[i][right])
                right -= 1
            elif dir == 2:  # Going left
                for j in range(right, left - 1, -1):
                    result.append(matrix[bottom][j])
                bottom -= 1
            else:  # Going up
                for i in range(bottom, top - 1, -1):
                    result.append(matrix[i][left])
                left += 1
            
            dir = (dir + 1) % 4
        
        return result
```

## Complexity Analysis

- **Time Complexity:** \(O(m  n)), where \(m\) is the number of rows and \(n\) is the number of columns. Each element of the matrix is processed exactly once.
- **Space Complexity:** \(O(1)\) if we exclude the space required for the output. The algorithm uses a constant amount of extra space for variables.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
