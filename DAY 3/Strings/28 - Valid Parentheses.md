# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)
[LeetCode Solution](https://leetcode.com/problems/largest-rectangle-in-histogram/solutions/5540315/best-solution-challenge-day-3-revisewitharshttps://leetcode.com/problems/valid-parentheses/solutions/5540421/best-solution-challenge-day-3-revisewitharsh)

The string is valid if:
1. Every open bracket has a corresponding closing bracket of the same type.
2. Brackets are properly nested and closed in the correct order.

## Intuition

Use a stack to track the open brackets as you traverse the string:
1. Push each opening bracket onto the stack.
2. For each closing bracket, check if it matches the bracket at the top of the stack. If it does, pop the stack; otherwise, the string is invalid.
3. At the end of the string, if the stack is empty, all opening brackets were properly matched with closing brackets.

## Approach

1. Initialize an empty stack.
2. Traverse each character in the string:
   - If it's an opening bracket ('(', '{', '['), push it onto the stack.
   - If it's a closing bracket (')', '}', ']'):
     - Check if the stack is empty. If it is, the string is invalid.
     - Otherwise, pop the top of the stack and check if it matches the corresponding opening bracket for the current closing bracket.
3. After traversing the string, if the stack is empty, the string is valid. Otherwise, it's invalid.

## Code

**py**
```python []
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        mapping = {')': '(', '}': '{', ']': '['}
        
        for char in s:
            if char in mapping:
                top_element = stack.pop() if stack else '#'
                if mapping[char] != top_element:
                    return False
            else:
                stack.append(char)
        
        return not stack
```
**cpp**
```cpp []
#include <stack>
#include <unordered_map>
#include <string>

class Solution {
public:
    bool isValid(std::string s) {
        std::stack<char> stack;
        std::unordered_map<char, char> mapping = {{')', '('}, {'}', '{'}, {']', '['}};
        
        for (char& c : s) {
            if (mapping.find(c) != mapping.end()) {
                char topElement = stack.empty() ? '#' : stack.top();
                stack.pop();
                if (mapping[c] != topElement) {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        
        return stack.empty();
    }
};
```
**java**
```java []
import java.util.Stack;
import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        Map<Character, Character> mapping = new HashMap<>();
        mapping.put(')', '(');
        mapping.put('}', '{');
        mapping.put(']', '[');
        
        for (char c : s.toCharArray()) {
            if (mapping.containsKey(c)) {
                char topElement = stack.isEmpty() ? '#' : stack.pop();
                if (mapping.get(c) != topElement) {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        
        return stack.isEmpty();
    }
}
```
**js**
```javascript []
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    let stack = [];
    let mapping = {')': '(', '}': '{', ']': '['};
    
    for (let char of s) {
        if (mapping[char]) {
            let topElement = stack.length === 0 ? '#' : stack.pop();
            if (mapping[char] !== topElement) {
                return false;
            }
        } else {
            stack.push(char);
        }
    }
    
    return stack.length === 0;
};
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. Each character is processed once, and each push and pop operation on the stack is \(O(1)\).
- **Space Complexity**: \(O(n)\) in the worst case, where \(n\) is the length of the string. This is due to the space used by the stack to store the open brackets.

This approach ensures that the solution is efficient and straightforward for checking the validity of bracket sequences.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
