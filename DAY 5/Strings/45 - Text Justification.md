# [68. Text Justification](https://leetcode.com/problems/text-justification/description/)

## Problem Explanation

The task is to format a given array of words into lines of text such that each line has exactly `maxWidth` characters and is fully justified. The justification should be done as follows:

1. **Full Justification**: Each line (except possibly the last one) should be justified by evenly distributing spaces between words. If extra spaces are needed, distribute them starting from the leftmost space between words.

2. **Left Justification**: The last line should be left-justified, meaning words are aligned to the left, and spaces are added at the end of the line if needed.

3. **Greedy Approach**: Pack as many words as you can into each line, without exceeding the `maxWidth`.

## Examples

### Example 1:

- **Input**: `words = ["This", "is", "an", "example", "of", "text", "justification."]`, `maxWidth = 16`
- **Output**:
  ```
  [
     "This    is    an",
     "example  of text",
     "justification.  "
  ]
  ```

### Example 2:

- **Input**: `words = ["What", "must", "be", "acknowledgment", "shall", "be"]`, `maxWidth = 16`
- **Output**:
  ```
  [
     "What   must   be",
     "acknowledgment  ",
     "shall be        "
  ]
  ```

### Example 3:

- **Input**: `words = ["Science", "is", "what", "we", "understand", "well", "enough", "to", "explain", "to", "a", "computer.", "Art", "is", "everything", "else", "we", "do"]`, `maxWidth = 20`
- **Output**:
  ```
  [
     "Science  is  what we",
     "understand      well",
     "enough to explain to",
     "a  computer.  Art is",
     "everything  else  we",
     "do                  "
  ]
  ```

## Intuition and Approach

1. **Initial Setup**: Start by iterating through the words to construct lines one by one. Use a greedy approach to add as many words as possible to the current line without exceeding `maxWidth`.

2. **Line Construction**: For each line:
   - Count the total number of characters of the words and the number of spaces needed.
   - If it is the last line or contains only one word, left justify it by joining the words with a single space and padding the end with spaces if necessary.
   - Otherwise, fully justify the line by distributing spaces evenly between the words. If there are extra spaces, distribute them starting from the leftmost space.

3. **Space Calculation**: Calculate the number of spaces between each pair of words and any leftover spaces that should be added starting from the left.

4. **Final Assembly**: Construct each line according to the rules above and add it to the result.

5. **Complexity**: The algorithm iterates through the list of words once, making it O(n) time complexity, where n is the total number of characters in all words combined.

## Python Solution

```python
class Solution:
    def fullJustify(self, words, maxWidth):
        res = []  # Resultant list of justified lines
        current_line = []  # Words in the current line
        current_length = 0  # Length of words in the current line

        for word in words:
            # Check if adding the new word exceeds the max width
            if current_length + len(word) + len(current_line) > maxWidth:
                # Create the line with justified text
                for i in range(maxWidth - current_length):
                    # Distribute spaces evenly
                    current_line[i % (len(current_line) - 1 or 1)] += ' '
                # Add the justified line to result
                res.append(''.join(current_line))
                # Reset for the next line
                current_line, current_length = [], 0
            # Add the current word to the line
            current_line.append(word)
            current_length += len(word)

        # Handle the last line, which is left-justified
        res.append(' '.join(current_line).ljust(maxWidth))
        return res
```

## C++ Solution

```cpp
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> res;
        vector<string> current_line;
        int current_length = 0;

        for (const string& word : words) {
            if (current_length + word.length() + current_line.size() > maxWidth) {
                for (int i = 0; i < maxWidth - current_length; ++i) {
                    current_line[i % (current_line.size() - 1 ? current_line.size() - 1 : 1)] += ' ';
                }
                string line = "";
                for (const string& w : current_line) {
                    line += w;
                }
                res.push_back(line);
                current_line.clear();
                current_length = 0;
            }
            current_line.push_back(word);
            current_length += word.length();
        }

        string last_line = "";
        for (int i = 0; i < current_line.size(); ++i) {
            last_line += current_line[i];
            if (i != current_line.size() - 1) last_line += ' ';
        }
        last_line.append(maxWidth - last_line.length(), ' ');
        res.push_back(last_line);

        return res;
    }
};
```

## Java Solution

```java
import java.util.*;

class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<>();
        List<String> currentLine = new ArrayList<>();
        int currentLength = 0;

        for (String word : words) {
            if (currentLength + word.length() + currentLine.size() > maxWidth) {
                for (int i = 0; i < maxWidth - currentLength; i++) {
                    currentLine.set(i % (currentLine.size() - 1 > 0 ? currentLine.size() - 1 : 1), currentLine.get(i % (currentLine.size() - 1 > 0 ? currentLine.size() - 1 : 1)) + " ");
                }
                StringBuilder line = new StringBuilder();
                for (String w : currentLine) {
                    line.append(w);
                }
                res.add(line.toString());
                currentLine.clear();
                currentLength = 0;
            }
            currentLine.add(word);
            currentLength += word.length();
        }

        StringBuilder lastLine = new StringBuilder();
        for (int i = 0; i < currentLine.size(); i++) {
            lastLine.append(currentLine.get(i));
            if (i != currentLine.size() - 1) lastLine.append(" ");
        }
        while (lastLine.length() < maxWidth) {
            lastLine.append(" ");
        }
        res.add(lastLine.toString());

        return res;
    }
}
```

## JavaScript Solution

```javascript
var fullJustify = function(words, maxWidth) {
    const res = [];
    let currentLine = [];
    let currentLength = 0;

    for (let word of words) {
        if (currentLength + word.length + currentLine.length > maxWidth) {
            for (let i = 0; i < maxWidth - currentLength; i++) {
                currentLine[i % (currentLine.length - 1 || 1)] += ' ';
            }
            res.push(currentLine.join(''));
            currentLine = [];
            currentLength = 0;
        }
        currentLine.push(word);
        currentLength += word.length;
    }

    const lastLine = currentLine.join(' ') + ' '.repeat(maxWidth - currentLine.join(' ').length);
    res.push(lastLine);

    return res;
};
```

### Time Complexity

The time complexity of the solution is \(O(n)\), where \(n\) is the total number of characters in all the words combined. Here's a breakdown of the operations involved:

1. **Iteration Over Words**: The algorithm iterates over each word in the `words` array once. For each word, it checks if adding the word to the current line will exceed `maxWidth`.

2. **Line Construction**: For each line that is fully justified (not the last line), the algorithm distributes the spaces among the words. The maximum number of words that can fit in a line is determined by `maxWidth` and the minimum word length. Thus, the space distribution is bounded by `maxWidth`.

3. **Last Line Justification**: The last line is processed by simply joining the words and adding spaces to the end, which is linear in terms of the number of words in the line.

Since each word is processed once and the operations per line are proportional to `maxWidth`, the overall time complexity is \(O(n)\).

### Space Complexity

The space complexity is \(O(m)\), where \(m\) is the number of lines generated in the result. Here's why:

1. **Storage for Result**: The output requires storing all the lines generated. Each line can be up to `maxWidth` characters long.

2. **Temporary Storage**: During the line construction, temporary storage for `current_line` is used to accumulate words before finalizing each line. This storage is proportional to the number of words that can fit within `maxWidth`.

Thus, the space complexity primarily depends on the number of lines formed and their respective lengths, making it \(O(m)\).


This solution is efficient and suitable for the problem constraints, providing optimal performance for formatting the text as required.

## Conclusion

The solution efficiently handles the problem by iterating through the words and constructing lines based on the justification rules. It uses a greedy approach to ensure each line has the maximum number of words possible and distributes spaces evenly for full justification. The handling of the last line with left justification is done separately to adhere to the problem requirements. This solution is optimal in terms of time complexity, with a single pass through the list of words and additional operations proportional to the number of lines formed.
