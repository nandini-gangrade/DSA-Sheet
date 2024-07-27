# [65. Valid Number](https://leetcode.com/problems/valid-number/description/)
[Leetcode Solution](https://leetcode.com/problems/valid-number/solutions/5545088/easy-solution-challenge-day-4-revisewitharsh) 

To determine if a string represents a valid number, we need to validate the string according to several rules that cover integers, decimal numbers, and scientific notation. We can use regular expressions for this task due to their capability to match complex patterns efficiently. However, I'll explain both a regular expression approach and a manual parsing approach for completeness.

## Approach

1. **Regular Expression Approach**:
   Use a regular expression to match the entire string against a pattern that covers all possible valid formats of a number.

2. **Manual Parsing Approach**:
   Parse the string manually to handle all possible formats and scenarios (integers, decimals, exponents) step by step.

### Regular Expression Approach

A regular expression (regex) can succinctly capture the definition of a valid number. Here is a regex pattern that matches the criteria:

```regex
^[+-]?((\d+(\.\d*)?)|(\.\d+))([eE][+-]?\d+)?$
```

- `^[+-]?` : Optional sign at the beginning.
- `(\d+(\.\d*)?)` : Digits followed by an optional dot and optional digits (e.g., `123`, `123.`, `123.456`).
- `(\.\d+)` : Or a dot followed by digits (e.g., `.456`).
- `([eE][+-]?\d+)?` : Optional exponent part (e.g., `e10`, `E-5`).

## Code

```python []
import re

class Solution:
    def isNumber(self, s: str) -> bool:
        # Regex pattern for validating numbers
        pattern = r'^[+-]?((\d+(\.\d*)?)|(\.\d+))([eE][+-]?\d+)?$'
        return re.match(pattern, s) is not None
```


## Complexity

- **Time Complexity**: The regex approach generally runs in \(O(n)\), where \(n\) is the length of the string.
- **Space Complexity**: The regex approach uses constant space for pattern matching.

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
