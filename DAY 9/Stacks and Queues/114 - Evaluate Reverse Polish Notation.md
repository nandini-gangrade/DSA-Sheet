# [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)
[Leetcode Solution](https://leetcode.com/problems/evaluate-reverse-polish-notation/solutions/2992665/easy-solution-well-explained-comprehensible)

Given an array of strings `tokens` representing an arithmetic expression in Reverse Polish Notation, evaluate the expression and return the result. The valid operators are `+`, `-`, `*`, and `/`, and operands are integers. Division should truncate towards zero.

## Intuition
Reverse Polish Notation (RPN) uses a postfix format where operators follow their operands. This makes evaluating expressions straightforward using a stack data structure. The main idea is to process tokens from left to right, using the stack to keep track of operands and apply operators as they are encountered.

## Approach

1. **Initialize a Stack**: Use a stack to store operands and intermediate results.
2. **Process Each Token**:
   - If the token is an operator (`+`, `-`, `*`, `/`):
     - Pop the top two elements from the stack. These are the operands for the operation.
     - Perform the operation and push the result back onto the stack.
   - If the token is an operand (an integer), convert it from a string to an integer and push it onto the stack.
3. **Final Result**: After processing all tokens, the stack will contain one element, which is the result of the RPN expression.

## Code

``` python []
class Solution:
    def evalRPN(self, tokens):
        """
        :type tokens: List[str]
        :rtype: int
        """
        stack = []
        
        for token in tokens:
            if token in {'+', '-', '*', '/'}:
                # Pop the top two elements from the stack
                b = stack.pop()
                a = stack.pop()
                
                # Perform the appropriate operation
                if token == '+':
                    stack.append(a + b)
                elif token == '-':
                    stack.append(a - b)
                elif token == '*':
                    stack.append(a * b)
                elif token == '/':
                    # Handle division with truncation towards zero
                    stack.append(int(a / b))  # Python's int() truncates towards zero
            else:
                # Convert the token to an integer and push it onto the stack
                stack.append(int(token))
        
        # The final result will be the only element left in the stack
        return stack[-1]
```

``` cpp []
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        for(auto x: tokens){ // For Operator
            if(x=="+" || x=="-" || x=="/" ||x=="*"){
                int b = st.top(); st.pop(); 
                int a = st.top(); st.pop();
                if(x=="+"){
                    st.push(a+b);
                }
                if(x=="-"){
                    st.push(a-b);
                }
                if(x=="/"){
                    st.push(a/b);
                }
                if(x=="*"){
                    st.push(a*b);
                }
            }
            else{ //For Operand: Convert String to Integer
                stringstream ss(x);
                int data;
                ss >> data;
                st.push(data);
            }
        }
        return st.top();
    }
};

```
 
``` java []
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        for(int i = 0; i < tokens.length; i++){
            if(tokens[i].equals("+")){
                int b = stack.pop();
                int a = stack.pop();
                stack.push(a+b);
            }
            else if(tokens[i].equals("-")){
                int b = stack.pop();
                int a = stack.pop();
                stack.push(a-b);
            }
            else if(tokens[i].equals("*")){
                int b = stack.pop();
                int a = stack.pop();
                stack.push(a*b);
            }
            else if(tokens[i].equals("/")){
                int b = stack.pop();
                int a = stack.pop();
                stack.push(a/b);
            }
            else
                stack.push(Integer.parseInt(tokens[i]));
        }
        return stack.pop();
    }
}
```


## Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of tokens. Each token is processed once, and each stack operation (push and pop) takes constant time, \(O(1)\).

- **Space Complexity**: \(O(n)\), where \(n\) is the number of tokens. In the worst case, the stack can hold all operands, which makes the space complexity proportional to the number of tokens.

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
