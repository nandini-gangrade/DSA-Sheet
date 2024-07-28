# [Boyer Moore Algorithm for Pattern Searching](https://www.geeksforgeeks.org/boyer-moore-algorithm-for-pattern-searching/)

The Boyer-Moore algorithm is a powerful pattern-searching algorithm that significantly reduces the number of comparisons required compared to naive approaches. It is particularly effective for long text and pattern sizes due to its ability to skip sections of the text, leveraging information from the pattern itself.

## Boyer-Moore Algorithm

### Key Concepts

The Boyer-Moore algorithm uses two main heuristics to improve the pattern-searching process:

1. **Bad Character Heuristic**: 
   - When a mismatch occurs between the text and the pattern, the algorithm looks for the last occurrence of the mismatched character in the pattern (if any) and shifts the pattern so that this character aligns with the mismatched character in the text.
   - If the mismatched character is not present in the pattern, the pattern is shifted entirely past the mismatched character.

2. **Good Suffix Heuristic**:
   - When a mismatch occurs, and a part of the pattern has matched, the algorithm tries to shift the pattern to align the previously matched suffix with another occurrence of it in the pattern.
   - If there’s no such occurrence, it shifts the pattern to align with the next potential matching suffix.

### Preprocessing Steps

1. **Bad Character Table**: Create an array (or hash table) that records the last occurrence of each character in the pattern. If a character is not present in the pattern, it is considered to have a last occurrence index of -1.

2. **Good Suffix Table**: Create a table that indicates how much to shift the pattern when a mismatch occurs after some characters have matched.

## Algorithm Steps

1. Preprocess the pattern to create the bad character and good suffix tables.
2. Start comparing the pattern with the text from the rightmost character of the pattern.
3. If a mismatch occurs, use the tables to determine the maximum shift to the right and apply it.
4. If a complete match of the pattern is found, record the position and shift the pattern based on the good suffix table.
5. Repeat the process until the pattern exceeds the bounds of the text.

### Example Implementation in Python

```python
def bad_character_heuristic(pattern, size):
    """
    Creates the bad character heuristic table.

    :param pattern: Pattern to be searched
    :param size: Size of the pattern
    :return: Bad character heuristic table
    """
    # Initialize all occurrences as -1
    bad_char = [-1] * 256

    # Fill the actual value of last occurrence
    for i in range(size):
        bad_char[ord(pattern[i])] = i

    return bad_char

def search(text, pattern):
    """
    Boyer-Moore pattern searching algorithm with the bad character heuristic.

    :param text: Text where pattern is to be searched
    :param pattern: Pattern to be searched
    """
    m = len(pattern)
    n = len(text)

    # Create the bad character heuristic table
    bad_char = bad_character_heuristic(pattern, m)

    # s is the shift of the pattern with respect to text
    s = 0
    while s <= n - m:
        j = m - 1

        # Keep reducing index j of pattern while characters of pattern and text are matching at this shift s
        while j >= 0 and pattern[j] == text[s + j]:
            j -= 1

        # If the pattern is present at the current shift, then index j will become -1 after the above loop
        if j < 0:
            print("Pattern found at index", s)

            # Shift the pattern so that the next character in text aligns with the last occurrence of it in pattern.
            # The condition s+m < n is necessary for the case when pattern occurs at the end of text
            s += (m - bad_char[ord(text[s + m])] if s + m < n else 1)
        else:
            # Shift the pattern so that the bad character in text aligns with the last occurrence of it in pattern.
            # The max function is used to make sure that we get a positive shift.
            s += max(1, j - bad_char[ord(text[s + j])])
```

### Explanation of the Example

- **Bad Character Heuristic**:
  - We create a table that maps each character in the pattern to its last occurrence index. If a mismatch occurs, this table helps determine how far the pattern can be shifted to the right.

- **Good Suffix Heuristic**:
  - In this basic implementation, we use only the bad character heuristic. However, the full Boyer-Moore algorithm includes the good suffix heuristic, which can further optimize shifts when a suffix has been matched.

- **Shift Calculation**:
  - If a mismatch occurs at index `j` of the pattern, calculate the shift as `max(1, j - bad_char[ord(text[s + j])])`. This ensures that the pattern is moved right enough to align with the text properly.

## Complexity Analysis

- **Time Complexity**: 
  - The average time complexity of the Boyer-Moore algorithm is \(O(n/m)\) for random text and pattern, and the worst-case time complexity is \(O(n + m)\), where \(n\) is the length of the text and \(m\) is the length of the pattern. The algorithm is sub-linear because it skips sections of the text rather than checking each character sequentially.

- **Space Complexity**:
  - The space complexity is \(O(m + \text{char\_set\_size})\), where `char_set_size` is the number of characters in the input character set (e.g., 256 for extended ASCII). This is due to the storage requirements for the bad character table.

## Conclusion

The Boyer-Moore algorithm is highly efficient for pattern searching, especially when the pattern is long compared to the text. By leveraging both the bad character and good suffix heuristics, it minimizes the number of comparisons needed, making it one of the fastest search algorithms available. This makes it particularly useful in applications where pattern matching needs to be performed on large volumes of text.
