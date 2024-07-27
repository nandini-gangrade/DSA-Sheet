# [71. Simplify Path](https://leetcode.com/problems/simplify-path/description/)
[LeetCode Solution](https://leetcode.com/problems/simplify-path/solutions/5544547/easy-solution-challenge-day-4-revisewitharsh) 

- **Single Period (.)**: This denotes the current directory and should be ignored.
- **Double Period (..)**: This signifies moving up one directory level. If we're already at the root, this has no effect.
- **Multiple Slashes**: Should be compressed into a single slash.
- **Other Sequences**: Considered as directory names and should be retained in the path.

## Approach

1. **Split the Path**: Break the path into components using '/' as the delimiter.
2. **Use a Stack**: Traverse the components, using a stack to manage the directory structure:
   - If the component is `..`, pop from the stack if it's not empty.
   - If the component is `.` or empty, do nothing.
   - Otherwise, push the component onto the stack.
3. **Construct the Simplified Path**: Join the elements in the stack with '/' to form the simplified path.

## Implementation

#### Python

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        stack = []
        components = path.split('/')
        
        for component in components:
            if component == '' or component == '.':
                continue
            elif component == '..':
                if stack:
                    stack.pop()
            else:
                stack.append(component)
        
        # Join the stack components to form the canonical path
        return '/' + '/'.join(stack)
```

#### C++

```cpp
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> stack;
        stringstream ss(path);
        string component;
        
        while (getline(ss, component, '/')) {
            if (component == "" || component == ".") {
                continue;
            } else if (component == "..") {
                if (!stack.empty()) {
                    stack.pop_back();
                }
            } else {
                stack.push_back(component);
            }
        }
        
        string result = "/";
        for (const auto& dir : stack) {
            result += dir + "/";
        }
        
        if (result.size() > 1) {
            result.pop_back(); // Remove trailing slash if not root
        }
        
        return result;
    }
};
```

#### Java

```java
class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        String[] components = path.split("/");
        
        for (String component : components) {
            if (component.isEmpty() || component.equals(".")) {
                continue;
            } else if (component.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                stack.push(component);
            }
        }
        
        StringBuilder result = new StringBuilder();
        for (String dir : stack) {
            result.append("/").append(dir);
        }
        
        return result.length() > 0 ? result.toString() : "/";
    }
}
```

#### JavaScript

```javascript
var simplifyPath = function(path) {
    const stack = [];
    const components = path.split('/');
    
    for (const component of components) {
        if (component === '' || component === '.') {
            continue;
        } else if (component === '..') {
            if (stack.length > 0) {
                stack.pop();
            }
        } else {
            stack.push(component);
        }
    }
    
    return '/' + stack.join('/');
};
```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the path. We process each character in the path once.
- **Space Complexity**: \(O(n)\), where \(n\) is the length of the path, as we might store all directory names in the stack.

This approach efficiently handles path simplification by leveraging a stack to track valid directory paths and eliminating unnecessary navigation elements.
