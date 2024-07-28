# [168. Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/description/)

To convert an integer `columnNumber` to its corresponding column title as it appears in an Excel sheet, we can use the following approach, which is similar to converting a number to a base-26 numeral system with a slight twist, due to the alphabet-based index.

## Intuition

- Excel columns use a 1-based index rather than a typical 0-based index. Therefore, when converting, we treat each column as a base-26 digit, where 'A' corresponds to 1, 'B' to 2, ..., 'Z' to 26.
- This means that for every decrement of the column number, we need to find the modulo 26 to determine the character at that place.
- To handle the fact that there's no "zero" digit in the alphabetic representation (A = 1, B = 2, ..., Z = 26), we adjust by subtracting 1 from `columnNumber` before performing modulo operations.

## Approach

1. **Initialize an empty result string**: This will store the column title as we build it.
2. **Iterate while `columnNumber` is greater than 0**:
   - Decrement `columnNumber` by 1 to make it zero-based.
   - Find the current digit using modulo 26.
   - Convert this digit to a character by adding the ASCII value of 'A' and append it to the result string.
   - Divide `columnNumber` by 26 to move to the next digit.
3. **Reverse the result**: Since we've built the string from the least significant digit to the most significant, reverse it to get the correct column title.

## Code

```python
class Solution:
    def convertToTitle(self, columnNumber):
        result = []
        while columnNumber > 0:
            columnNumber -= 1  # Adjust to zero-based index
            digit = columnNumber % 26
            # Convert to corresponding ASCII character
            result.append(chr(digit + ord('A')))
            # Move to the next digit
            columnNumber //= 26

        # Reverse the result and join to form the final string
        return ''.join(reversed(result))
```

## Complexity Analysis

- **Time Complexity**: \(O(\log_{26}(n))\), where \(n\) is the input `columnNumber`. The number of iterations is proportional to the number of digits in the base-26 representation of the column number.
- **Space Complexity**: \(O(\log_{26}(n))\), as we store the resulting column title in a list that may grow up to the number of base-26 digits. 

This solution efficiently computes the column title for any given integer within the constraints, using basic arithmetic operations and character manipulations.
