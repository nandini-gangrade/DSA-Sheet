# [901. Online Stock Span](https://leetcode.com/problems/online-stock-span/description/)

The span of a stock price for a given day is the number of consecutive days (including the current day) the stock price has been less than or equal to the price on the current day. By using a stack, we can keep track of prices and calculate the span in constant time for each price.

### Approach

1. **Data Structure**: Use a stack to store pairs of `(price, span)`.
   - Each element in the stack represents a stock price and its calculated span.
   
2. **Calculate Span**: For each new stock price:
   - Initialize the span to 1 (the current day itself).
   - While the stack is not empty and the current price is greater than or equal to the price at the top of the stack, pop the stack and add the span of the popped element to the current span. This is because the current price is greater than all the prices in the popped elements, thus extending the span.
   - Push the current price and its calculated span onto the stack.

3. **Return Result**: Return the calculated span.

## Code Implementation

```python
class StockSpanner:
    def __init__(self):
        self.stack = []  # Stack to store pairs of (price, span)

    def next(self, price):
        span = 1  # Start with a span of 1 for the current day
        # Calculate the span by popping all elements with price <= current price
        while self.stack and self.stack[-1][0] <= price:
            span += self.stack.pop()[1]  # Add the span of the popped element
        # Push the current price and calculated span onto the stack
        self.stack.append((price, span))
        return span
```

## Complexity Analysis

- **Time Complexity**: Each call to `next` has an average time complexity of \(O(1)\). This is because each element is pushed and popped from the stack at most once, leading to an amortized constant time complexity.
- **Space Complexity**: \(O(n)\), where \(n\) is the number of prices processed. This is due to the space used by the stack to store prices and spans.

This approach efficiently calculates the span by leveraging the properties of stacks to keep track of the necessary state, ensuring that each operation is performed in constant time on average.
