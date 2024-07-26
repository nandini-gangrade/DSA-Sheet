# [79. Word Search](https://leetcode.com/problems/word-search/description/)
[LeetCode Solution](https://leetcode.com/problems/word-search/solutions/5539919/step-by-step-explanation-challenge-day-3-revisewitharsh)

Given an \(m \times n\) grid of characters `board` and a string `word`, return `true` if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Examples

**Example 1:**

- **Input:** `board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "ABCCED"`
- **Output:** `true`

**Example 2:**

- **Input:** `board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "SEE"`
- **Output:** `true`

**Example 3:**

- **Input:** `board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "ABCB"`
- **Output:** `false`

### Constraints

- \(m\) (number of rows) and \(n\) (number of columns) are between 1 and 6.
- The length of `word` is between 1 and 15.
- `board` and `word` consist of only lowercase and uppercase English letters.

## Intuition

To determine if the word exists in the grid, we can use a recursive depth-first search (DFS) algorithm. We will start from each cell in the grid and attempt to find the word by checking all possible paths formed by adjacent cells. If a path does not lead to the solution, we backtrack and try another path.

## Approach

1. **Recursive DFS Function:**
   - Create a recursive function `dfs` that will explore the grid.
   - If the current character in the path matches the corresponding character in the word, proceed to check its adjacent cells.
   - Use a `visited` set to keep track of the cells that are part of the current path to avoid using the same cell more than once.

2. **Backtracking:**
   - For each cell, recursively explore all four possible directions (right, down, left, up).
   - If a direction does not lead to a solution, backtrack and try another direction.

3. **Base Cases:**
   - If the entire word is matched, return `true`.
   - If the current cell is out of bounds or already visited or does not match the current character of the word, return `false`.

4. **Iterate Over the Grid:**
   - Start the DFS from each cell in the grid. If any of the DFS calls returns `true`, the word exists in the grid.

## Python Code

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not board:
            return False
        
        m, n = len(board), len(board[0])
        
        def dfs(x, y, index):
            if index == len(word):
                return True
            if x < 0 or x >= m or y < 0 or y >= n or board[x][y] != word[index]:
                return False
            
            temp = board[x][y]
            board[x][y] = '#'  # Mark the cell as visited
            
            # Explore in all four directions
            found = (dfs(x + 1, y, index + 1) or
                     dfs(x - 1, y, index + 1) or
                     dfs(x, y + 1, index + 1) or
                     dfs(x, y - 1, index + 1))
            
            board[x][y] = temp  # Unmark the cell (backtrack)
            
            return found
        
        for i in range(m):
            for j in range(n):
                if dfs(i, j, 0):  # Start the DFS from each cell
                    return True
        
        return False
```

## Complexity Analysis

- **Time Complexity:** \(O(m \times n \times 4^L)\), where \(m\) is the number of rows, \(n\) is the number of columns, and \(L\) is the length of the word. In the worst case, each cell could be the start of a DFS that explores four directions for each character in the word.

- **Space Complexity:** \(O(L)\), where \(L\) is the length of the word, due to the recursion stack in the DFS call. The grid is modified in-place to mark visited cells, so no additional space is used for tracking visited cells.

This backtracking approach efficiently checks all possible paths in the grid to determine if the word can be formed.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
