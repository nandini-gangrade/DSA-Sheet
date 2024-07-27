# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/)
[LeetCode Solution](https://leetcode.com/problems/generate-parentheses/solutions/5544515/easy-solution-challenge-day-4-revisewitharsh)

Given `n` pairs of parentheses, generate all combinations of well-formed parentheses. A combination is well-formed if:
- Every open parenthesis `(` has a corresponding closed parenthesis `)`.
- At no point in the combination should the number of closed parentheses `)` exceed the number of open parentheses `(`.

## Intuition

The key to generating well-formed parentheses is to maintain the balance between the number of open and closed parentheses. We can use a recursive backtracking approach to explore all possible combinations, making sure to only add a closing parenthesis if it would not result in an invalid sequence.

## Approach

1. **Recursive Backtracking**: Start with an empty string and build it by adding either an open parenthesis `(` or a close parenthesis `)` at each step.
2. **Constraints**:
   - Only add an open parenthesis if we have not yet used all `n` open parentheses.
   - Only add a close parenthesis if it would not exceed the number of open parentheses used so far.
3. **Base Case**: When the constructed string reaches a length of `2 * n`, add it to the result list as a valid combination.

## Implementation

#### Python

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        def backtrack(current: str, open_count: int, close_count: int):
            # Base case: if the current string is valid and complete
            if len(current) == 2 * n:
                result.append(current)
                return
            
            # If we can add an open parenthesis, add it and recurse
            if open_count < n:
                backtrack(current + "(", open_count + 1, close_count)
            
            # If we can add a close parenthesis, add it and recurse
            if close_count < open_count:
                backtrack(current + ")", open_count, close_count + 1)

        result = []
        backtrack("", 0, 0)
        return result
```

#### C++

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> result;
        function<void(string, int, int)> backtrack = [&](string current, int openCount, int closeCount) {
            // Base case: if the current string is valid and complete
            if (current.size() == 2 * n) {
                result.push_back(current);
                return;
            }
            
            // If we can add an open parenthesis, add it and recurse
            if (openCount < n) {
                backtrack(current + "(", openCount + 1, closeCount);
            }
            
            // If we can add a close parenthesis, add it and recurse
            if (closeCount < openCount) {
                backtrack(current + ")", openCount, closeCount + 1);
            }
        };
        
        backtrack("", 0, 0);
        return result;
    }
};
```

#### Java

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        
        backtrack(result, "", 0, 0, n);
        
        return result;
    }
    
    private void backtrack(List<String> result, String current, int openCount, int closeCount, int max) {
        // Base case: if the current string is valid and complete
        if (current.length() == max * 2) {
            result.add(current);
            return;
        }
        
        // If we can add an open parenthesis, add it and recurse
        if (openCount < max) {
            backtrack(result, current + "(", openCount + 1, closeCount, max);
        }
        
        // If we can add a close parenthesis, add it and recurse
        if (closeCount < openCount) {
            backtrack(result, current + ")", openCount, closeCount + 1, max);
        }
    }
}
```

#### JavaScript

```javascript
var generateParenthesis = function(n) {
    const result = [];
    
    const backtrack = (current, openCount, closeCount) => {
        // Base case: if the current string is valid and complete
        if (current.length === 2 * n) {
            result.push(current);
            return;
        }
        
        // If we can add an open parenthesis, add it and recurse
        if (openCount < n) {
            backtrack(current + "(", openCount + 1, closeCount);
        }
        
        // If we can add a close parenthesis, add it and recurse
        if (closeCount < openCount) {
            backtrack(current + ")", openCount, closeCount + 1);
        }
    };
    
    backtrack("", 0, 0);
    return result;
};
```

## Complexity Analysis

- **Time Complexity**: \(O(4^n/\sqrt{n})\). This is based on the [Catalan number](https://en.wikipedia.org/wiki/Catalan_number) sequence, which counts the number of valid parentheses sequences.
- **Space Complexity**: \(O(4^n/\sqrt{n})\) for storing the result list. The recursive call stack uses \(O(n)\) space for each valid sequence being constructed.

The backtracking approach efficiently generates all valid combinations by maintaining the balance between open and close parentheses, ensuring well-formedness at each step.
