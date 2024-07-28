# [67. Add Binary](https://leetcode.com/problems/add-binary/description/)

To add two binary strings `a` and `b`, you can simulate the binary addition process, which is similar to adding decimal numbers but with base 2. Here's a detailed explanation of how to implement this in Python:

## Intuition

1. **Binary Addition**:
   - Binary addition works similarly to decimal addition, but it only involves two digits: 0 and 1.
   - The sum of two binary digits with a carry can be:
     - `0 + 0 + carry` = `0`
     - `1 + 0 + carry` = `1`
     - `1 + 1 + carry` = `10` (which is `0` with a carry of `1`)
     - `1 + 1 + 1 (carry)` = `11` (which is `1` with a carry of `1`)

2. **Carry**:
   - Keep track of the carry as you add each pair of bits from the end of both strings.

## Approach

1. **Initialize**:
   - Start from the end of both strings `a` and `b`.
   - Initialize a carry to 0.
   - Initialize an empty result list to store the sum bits.

2. **Iterate and Add**:
   - Use two pointers to iterate through both strings from the end to the start.
   - For each pair of bits, calculate the sum and update the carry.
   - Append the resulting bit to the result list.

3. **Handle Remaining Carry**:
   - If there's a carry left after processing all bits, append it to the result.

4. **Build the Final String**:
   - Reverse the result list and join the bits to form the final binary sum string.

## Code

```python
class Solution:
    def addBinary(self, a, b):
        # Initialize pointers for both strings
        i, j = len(a) - 1, len(b) - 1
        carry = 0
        result = []

        # Iterate through both strings from the end
        while i >= 0 or j >= 0 or carry:
            # Get the current bits and convert them to integers
            bit_a = int(a[i]) if i >= 0 else 0
            bit_b = int(b[j]) if j >= 0 else 0

            # Calculate the total and the carry
            total = bit_a + bit_b + carry
            carry = total // 2
            result.append(str(total % 2))

            # Move to the next pair of bits
            i -= 1
            j -= 1

        # Reverse the result list and join to form the final binary string
        return ''.join(reversed(result))
```

## Complexity Analysis

- **Time Complexity**: \(O(\max(n, m))\), where \(n\) and \(m\) are the lengths of the strings `a` and `b`, respectively. We iterate through both strings once.
- **Space Complexity**: \(O(\max(n, m))\) for storing the result, as the length of the result can be at most one more than the longer of the two input strings due to a possible carry. 

This approach efficiently handles binary addition without converting to and from decimal, making it suitable for large binary strings.
