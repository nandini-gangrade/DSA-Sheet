# [12. Integer to Roman](https://leetcode.com/problems/integer-to-roman/description/)
[LeetCode Solution](https://leetcode.com/problems/integer-to-roman/solutions/5544454/easy-solution-challenge-day-4-revisewitharsh)

Given an integer, convert it to a Roman numeral using the following rules:

1. Roman numerals are formed by combining symbols from the largest to the smallest.
2. Subtractive forms are used for numbers starting with 4 or 9 in a decimal place.
3. The symbols for 5 (V), 50 (L), and 500 (D) cannot be repeated; instead, subtractive forms must be used.

## Approach

1. **Create a Mapping**: Define a list of tuples that map integer values to their corresponding Roman numeral symbols. This list should be ordered from the largest to the smallest value, including both standard and subtractive forms.

2. **Iterate through the Mapping**: Initialize an empty string to store the Roman numeral. Traverse the mapping, and for each integer value, append the corresponding Roman numeral symbol to the result string as many times as the number can be divided by the integer value.

3. **Subtract and Continue**: Subtract the integer value times the count from the number and continue to the next pair in the mapping until the number is reduced to zero.

## Implementation

#### Python

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        # Mapping of Roman numerals in descending order of values
        value_map = [
            (1000, "M"),
            (900, "CM"),
            (500, "D"),
            (400, "CD"),
            (100, "C"),
            (90, "XC"),
            (50, "L"),
            (40, "XL"),
            (10, "X"),
            (9, "IX"),
            (5, "V"),
            (4, "IV"),
            (1, "I"),
        ]
        
        roman = []
        
        # Construct the Roman numeral
        for value, symbol in value_map:
            if num == 0:
                break
            count, num = divmod(num, value)
            roman.append(symbol * count)
        
        return ''.join(roman)
```

#### C++

```cpp
class Solution {
public:
    string intToRoman(int num) {
        // Mapping of Roman numerals in descending order of values
        vector<pair<int, string>> valueMap = {
            {1000, "M"},
            {900, "CM"},
            {500, "D"},
            {400, "CD"},
            {100, "C"},
            {90, "XC"},
            {50, "L"},
            {40, "XL"},
            {10, "X"},
            {9, "IX"},
            {5, "V"},
            {4, "IV"},
            {1, "I"}
        };
        
        string roman;
        
        // Construct the Roman numeral
        for (auto& [value, symbol] : valueMap) {
            if (num == 0) break;
            int count = num / value;
            num %= value;
            while (count--) {
                roman += symbol;
            }
        }
        
        return roman;
    }
};
```

#### Java

```java
class Solution {
    public String intToRoman(int num) {
        // Mapping of Roman numerals in descending order of values
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        
        StringBuilder roman = new StringBuilder();
        
        // Construct the Roman numeral
        for (int i = 0; i < values.length && num > 0; i++) {
            while (num >= values[i]) {
                roman.append(symbols[i]);
                num -= values[i];
            }
        }
        
        return roman.toString();
    }
}
```

#### JavaScript

```javascript
var intToRoman = function(num) {
    // Mapping of Roman numerals in descending order of values
    const valueMap = [
        [1000, "M"],
        [900, "CM"],
        [500, "D"],
        [400, "CD"],
        [100, "C"],
        [90, "XC"],
        [50, "L"],
        [40, "XL"],
        [10, "X"],
        [9, "IX"],
        [5, "V"],
        [4, "IV"],
        [1, "I"],
    ];
    
    let roman = "";
    
    // Construct the Roman numeral
    for (const [value, symbol] of valueMap) {
        if (num === 0) break;
        const count = Math.floor(num / value);
        num %= value;
        roman += symbol.repeat(count);
    }
    
    return roman;
};
```

## Complexity Analysis

- **Time Complexity**: \(O(1)\). The algorithm always performs a fixed number of operations since there are only 13 Roman numeral symbols to check. 
- **Space Complexity**: \(O(1)\). The space used to store the Roman numeral string is constant with respect to the size of the input `num` because Roman numerals have a fixed representation.

This approach ensures that we efficiently convert any integer from 1 to 3999 into its corresponding Roman numeral by leveraging the predefined symbol-value mapping and iterating through it systematically.
