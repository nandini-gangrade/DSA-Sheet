# [The Celebrity Problem](https://www.geeksforgeeks.org/problems/the-celebrity-problem/1)

To solve the celebrity problem, we need to identify the person who is known by everyone else but doesn't know anyone. The provided solution uses two arrays to count the number of people each person knows (`iknow`) and the number of people who know each person (`knowme`).

The solution checks each element in the matrix to determine if a person could be a celebrity by fulfilling these two conditions:

1. **Condition 1:** `knowme[i] == n-1` - The person must be known by everyone else.
2. **Condition 2:** `iknow[i] == 0` - The person must not know anyone else.

### Python Implementation

```python
class Solution:
    def celebrity(self, mat):
        n = len(mat)
        knowme = [0] * n  # Number of people who know person i
        iknow = [0] * n   # Number of people person i knows

        # Fill knowme and iknow arrays
        for i in range(n):
            for j in range(n):
                if mat[i][j] == 1:
                    knowme[j] += 1
                    iknow[i] += 1

        # Find the celebrity
        for i in range(n):
            if knowme[i] == n - 1 and iknow[i] == 0:
                return i

        return -1

# Example usage
sol = Solution()
mat1 = [[0, 1, 0], [0, 0, 0], [0, 1, 0]]
mat2 = [[0, 1], [1, 0]]
print(sol.celebrity(mat1))  # Output: 1
print(sol.celebrity(mat2))  # Output: -1
```

### Explanation

- **Initialization:**
  - `knowme[i]` is initialized to 0 and stores the count of how many people know person `i`.
  - `iknow[i]` is initialized to 0 and stores the count of how many people person `i` knows.

- **Matrix Traversal:**
  - For each `i` and `j`, if `mat[i][j] == 1`, it means person `i` knows person `j`.
  - We increment `knowme[j]` because person `j` is known by person `i`.
  - We increment `iknow[i]` because person `i` knows person `j`.

- **Celebrity Check:**
  - After populating `knowme` and `iknow`, iterate through each person.
  - If a person satisfies both conditions of being a celebrity, return their index.
  - If no such person is found, return `-1`.

### Complexity

- **Time Complexity:** \(O(n^2)\) because we iterate through the matrix, which is \(n \times n\).
- **Space Complexity:** \(O(n)\) for the `knowme` and `iknow` arrays used to track knowledge relationships. 

This solution efficiently determines if there is a celebrity by counting how many people each person knows and is known by.
