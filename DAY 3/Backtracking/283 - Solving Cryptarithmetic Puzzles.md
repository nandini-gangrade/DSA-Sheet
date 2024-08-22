# [Solving Cryptarithmetic Puzzles](https://www.geeksforgeeks.org/solving-cryptarithmetic-puzzles/)

Crypt-arithmetic puzzles are fascinating problems that involve assigning digits to letters such that a given arithmetic equation holds true. The puzzle you provided, where the words "SEND" and "MORE" are added to yield "MONEY," is a classic example.

### Problem Breakdown

Given the crypt-arithmetic puzzle:

```
  SEND
+ MORE
--------
 MONEY
```

Each letter represents a unique digit from 0 to 9. The objective is to find a valid digit assignment for each letter that satisfies the arithmetic equation.

### Approach

To solve this problem, we can use backtracking. Here’s a step-by-step approach:

1. **Identify Unique Characters**: Identify all unique letters involved in the puzzle.
  
2. **Recursive Backtracking**: 
   - Try assigning digits to each character recursively.
   - Ensure that each digit is unique and not already assigned to another letter.
   - Check if the current assignment satisfies the partial sum. If it does, continue to the next character; if not, backtrack.

3. **Base Case**:
   - When all characters are assigned, check if the current assignment satisfies the equation.

### Implementation

Here’s the Python implementation for solving this crypt-arithmetic puzzle using backtracking:

```python
def is_valid_assignment(assignment, words, result):
    # Convert the words and result to numbers based on the current assignment
    def word_to_number(word):
        return int("".join(str(assignment[char]) for char in word))

    sum_words = sum(word_to_number(word) for word in words)
    return sum_words == word_to_number(result)

def solve(puzzle_chars, idx, digits, assignment, words, result):
    if idx == len(puzzle_chars):
        # All characters are assigned, check if it's a valid solution
        if is_valid_assignment(assignment, words, result):
            print(f"Solved: {assignment}")
            return True
        return False

    # Get the current character to assign a digit to
    current_char = puzzle_chars[idx]

    for digit in range(10):
        if digit not in digits:
            # Assign digit to current character
            assignment[current_char] = digit
            digits.add(digit)

            # Recur to assign the next character
            if solve(puzzle_chars, idx + 1, digits, assignment, words, result):
                return True

            # Backtrack: remove the digit and try the next one
            del assignment[current_char]
            digits.remove(digit)

    return False

def cryptarithmetic_solver(words, result):
    # Collect all unique characters from the words and result
    puzzle_chars = set("".join(words) + result)
    if len(puzzle_chars) > 10:
        return "No solution possible, more than 10 unique characters."

    # Convert the set to a list to work with indices
    puzzle_chars = list(puzzle_chars)

    # To store the digit assignment for each character
    assignment = {}

    # To keep track of which digits are already used
    digits = set()

    # Start the backtracking process
    if solve(puzzle_chars, 0, digits, assignment, words, result):
        return assignment
    else:
        return "No solution found."

# Example usage
words = ["SEND", "MORE"]
result = "MONEY"
solution = cryptarithmetic_solver(words, result)
print(f"Solution: {solution}")
```

### Explanation

- **`is_valid_assignment`**: Converts the words and the result into numbers based on the current character-to-digit assignment and checks if the sum of the words equals the result.
  
- **`solve`**: This is the core backtracking function that tries to assign digits to characters one by one. It checks each possible digit for the current character, recursively tries to solve the rest of the puzzle, and backtracks if necessary.
  
- **`cryptarithmetic_solver`**: Initializes the backtracking process by collecting all unique characters and starting the `solve` function.

### Example Output

For the input puzzle with `words = ["SEND", "MORE"]` and `result = "MONEY"`, the output could be:

```
Solved: {'M': 1, 'O': 0, 'N': 6, 'E': 5, 'Y': 2, 'S': 9, 'D': 7, 'R': 8}
```

This means:
```
  9567
+ 1085
-------
 10652
```

### Conclusion

This code effectively solves the crypt-arithmetic puzzle using a recursive backtracking approach. It finds a valid assignment of digits to letters such that the arithmetic equation holds true.

---

## OR

---

Crypt-arithmetic puzzles, like the one described, involve assigning digits to letters so that the resulting arithmetic operation is valid. Here, each letter represents a unique digit, and no two letters can represent the same digit. In this case, we are tasked with solving the crypt-arithmetic puzzle:

```
  SEND
+ MORE
------
 MONEY
```

### Steps to Solve:

1. **Identify all unique letters**: We need to assign unique digits to the letters: `S`, `E`, `N`, `D`, `M`, `O`, `R`, `Y`.
   
2. **Use backtracking to try all possible digit assignments**: For each letter, try assigning a digit (from 0-9) and ensure no digit is repeated.

3. **Check if the arithmetic holds**: Once all letters have been assigned digits, check if the arithmetic equation holds:
   - `SEND + MORE = MONEY`

### Approach:

1. **Extract all unique letters**: Create a list of unique characters that need digit assignments.
   
2. **Backtracking function**: Recursively assign digits to the characters, trying all possibilities for each unassigned character. If a valid assignment is found, return `True`.

3. **Check the solution**: After assigning all digits, evaluate if the summation is correct.

### Implementation in Python:

```python
from itertools import permutations

# Function to map a list of characters to their respective digits
def is_valid_solution(assignment, send, more, money):
    # Convert character lists to integers using the assignment
    send_value = int(''.join(str(assignment[ch]) for ch in send))
    more_value = int(''.join(str(assignment[ch]) for ch in more))
    money_value = int(''.join(str(assignment[ch]) for ch in money))

    # Check if the equation holds: SEND + MORE = MONEY
    return send_value + more_value == money_value

# Backtracking to solve the crypt-arithmetic puzzle
def solve_cryptarithmetic():
    # List of unique characters to assign digits to
    letters = ['S', 'E', 'N', 'D', 'M', 'O', 'R', 'Y']

    # Extract words as character lists
    send = ['S', 'E', 'N', 'D']
    more = ['M', 'O', 'R', 'E']
    money = ['M', 'O', 'N', 'E', 'Y']

    # Try all permutations of digits for these letters
    for perm in permutations(range(10), len(letters)):
        assignment = dict(zip(letters, perm))

        # Ensure that 'S' and 'M' don't get assigned 0, as they are leading digits
        if assignment['S'] != 0 and assignment['M'] != 0:
            if is_valid_solution(assignment, send, more, money):
                return assignment  # Return the successful assignment

    return None  # Return None if no valid solution was found

# Solve the puzzle and print the solution
solution = solve_cryptarithmetic()

if solution:
    print("Solution found!")
    print(solution)
else:
    print("No solution exists.")
```

### Explanation:

1. **Mapping Digits**: The `is_valid_solution` function converts the letters in `SEND`, `MORE`, and `MONEY` to their respective digits and checks whether the equation holds.
   
2. **Backtracking**: In `solve_cryptarithmetic`, the `permutations` function tries all possible digit assignments for the unique letters (while ensuring that leading letters are not assigned `0`).

3. **Output**: If a valid assignment is found, it is printed; otherwise, the algorithm reports that no solution exists.

### Example Output:

```
Solution found!
{'S': 9, 'E': 5, 'N': 6, 'D': 7, 'M': 1, 'O': 0, 'R': 8, 'Y': 2}
```

This means:
- `SEND = 9567`
- `MORE = 1085`
- `MONEY = 10652`
And indeed, `9567 + 1085 = 10652`.

### Time Complexity:
- **Factorial Complexity**: The time complexity of this solution is \(O(10!)\) since it tries every possible assignment of digits to letters. However, optimizations like skipping assignments where the leading digit is `0` reduce the search space slightly.

This is a classic backtracking problem where we attempt different combinations and backtrack when an invalid configuration is found.
