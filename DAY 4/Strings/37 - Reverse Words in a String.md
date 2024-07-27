# [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)
[Leetcode Solution](https://leetcode.com/problems/reverse-words-in-a-string/solutions/5544710/easy-solution-challenge-day-4-revisewitharsh)

1. **Trim Leading and Trailing Spaces**: Remove any extra spaces at the beginning and end of the string.
2. **Split the String into Words**: Use whitespace as the delimiter to split the string into individual words.
3. **Reverse the Words**: Reverse the order of the words.
4. **Join the Words**: Concatenate the reversed words with a single space between each.

## Approach
1. **Trim**: Use a trimming function to remove leading and trailing spaces.
2. **Split**: Split the string by whitespace using a splitting function that handles multiple spaces.
3. **Reverse**: Reverse the list of words.
4. **Join**: Join the reversed list of words with a single space.

## Code

```python []
class Solution:
    def reverseWords(self, s: str) -> str:
        # Trim leading and trailing spaces, split by whitespace, reverse the list, and join with a single space
        return ' '.join(s.strip().split()[::-1])
```

```cpp []
#include <iostream>
#include <sstream>
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    string reverseWords(string s) {
        // Trim leading and trailing spaces
        size_t start = s.find_first_not_of(' ');
        size_t end = s.find_last_not_of(' ');
        if (start == string::npos) return ""; // Edge case: empty string

        // Extract the relevant substring
        s = s.substr(start, end - start + 1);
        
        istringstream iss(s);
        vector<string> words;
        string word;
        
        // Split the string into words
        while (iss >> word) {
            words.push_back(word);
        }
        
        // Reverse the vector of words
        reverse(words.begin(), words.end());
        
        // Join words with a single space
        string result;
        for (const auto& w : words) {
            if (!result.empty()) result += ' ';
            result += w;
        }
        
        return result;
    }
};

```

```java []
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Solution {
    public String reverseWords(String s) {
        // Trim leading and trailing spaces and split by whitespace
        String[] words = s.trim().split("\\s+");
        List<String> wordList = new ArrayList<>();
        
        // Add words to the list
        Collections.addAll(wordList, words);
        
        // Reverse the list of words
        Collections.reverse(wordList);
        
        // Join words with a single space
        return String.join(" ", wordList);
    }

```

```javascript []
class Solution {
    reverseWords(s) {
        // Trim leading and trailing spaces, split by whitespace, reverse the array, and join with a single space
        return s.trim().split(/\s+/).reverse().join(' ');
    }
}

```

## Complexity Analysis

- **Time Complexity**: \(O(n)\), where \(n\) is the length of the input string. This includes trimming, splitting, reversing, and joining operations.
- **Space Complexity**: \(O(n)\), where \(n\) is the length of the input string. This accounts for the space used to store the split words and the final result.

All implementations handle edge cases like extra spaces and ensure that the output is a single space-separated string of words in reverse order.

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
