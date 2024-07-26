# [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
[LeetCode Solution](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/solutions/5540533/short-best-solution-challenge-day-3-revisewitharsh)

You need to determine the starting index of the first occurrence of `needle` in `haystack`. If `needle` is not found, return `-1`.

## Intuition

- **Substring Search**: This problem is essentially about finding the index of a substring within a larger string.
- **Edge Cases**: Consider cases where either `needle` or `haystack` is empty. According to constraints, both strings are non-empty.

## Approach

1. **Built-in Methods**: Utilize Python's string method `.find()`, C++'s `std::string::find()`, Java's `String.indexOf()`, and JavaScript's `String.indexOf()` for simplicity.
2. **Manual Search**: Implement a substring search algorithm if required to avoid built-in methods.

## Code 

#### Python

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.find(needle)
```

#### C++

```cpp
#include <string>
using namespace std;

class Solution {
public:
    int strStr(string haystack, string needle) {
        size_t found = haystack.find(needle);
        return (found != string::npos) ? static_cast<int>(found) : -1;
    }
};
```

#### Java

```java
class Solution {
    public int strStr(String haystack, String needle) {
        return haystack.indexOf(needle);
    }
}
```

#### JavaScript

```javascript
var strStr = function(haystack, needle) {
    return haystack.indexOf(needle);
};
```

## Complexity Analysis

- **Time Complexity**: \(O(n.m)\) in the worst case, where \(n\) is the length of `haystack` and \(m\) is the length of `needle`. However, with efficient built-in methods, this is usually \(O(n)\) for average cases.
- **Space Complexity**: \(O(1)\) for the built-in methods. If implementing manually, the space complexity could be \(O(m)\) due to the additional space required for substring comparison.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
