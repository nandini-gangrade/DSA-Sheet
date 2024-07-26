# [Print all the duplicate characters in a string](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/)
[GFG Blog](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/)

Given a string, we need to identify characters that appear more than once and print each of these characters along with their frequency of occurrence.

## Intuition

1. **Count Frequencies**: Use a data structure to count the occurrences of each character.
2. **Identify Duplicates**: Iterate over the frequency counts and identify characters that have a count greater than 1.
3. **Print Results**: Output the duplicate characters and their counts.

## Approach

1. **Frequency Counting**: Use a dictionary to store the frequency of each character in the string.
2. **Filter Duplicates**: Iterate over the dictionary and filter out characters with a count of 1.
3. **Output**: Print the characters and their counts that are identified as duplicates.

## Code

```python
from collections import Counter

def printDuplicates(S: str):
    # Count the occurrences of each character using Counter
    freq = Counter(S)
    
    # Iterate over the frequency dictionary
    for char, count in freq.items():
        # Print characters that have more than one occurrence
        if count > 1:
            print(f"{char}, count = {count}")

# Example usage
S = "geeksforgeeks"
printDuplicates(S)
```

### Explanation of the Code

1. **Import `Counter`**: We use the `Counter` class from the `collections` module to easily count occurrences of each character.
2. **Count Frequencies**: `Counter(S)` creates a dictionary where keys are characters and values are their counts in the string `S`.
3. **Filter and Print**: Iterate through the dictionary items and print the character and its count if the count is greater than 1.

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. This is because counting frequencies and iterating over the dictionary both take linear time.
- **Space Complexity**: \(O(k)\), where \(k\) is the number of unique characters in the string. This space is used to store the frequency counts.

This approach ensures that the solution is both efficient and straightforward for identifying and printing duplicate characters in a string.
