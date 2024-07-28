# [Print Anagrams Together](https://www.geeksforgeeks.org/problems/print-anagrams-together/1)

To solve the problem of grouping anagrams from a list of words, we can use a hash map (dictionary in Python) to organize the words into groups. Each group will consist of words that are anagrams of each other. The approach involves sorting each word to generate a key that is used to identify its anagram group.

Here is how you can implement this solution in Python:

### Approach

1. **Initialize a Hash Map**: Use a dictionary to map each sorted word (anagram key) to a list of its anagrams.

2. **Iterate Over Words**: For each word in the list, sort the characters of the word to create a key. Use this key to store the word in the appropriate anagram group in the dictionary.

3. **Collect Results**: Once all words have been processed, collect the values (anagram groups) from the dictionary. These represent the groups of anagrams.

4. **Lexicographic Order**: The final output will be sorted lexicographically by the group, not by the words within each group. This will be handled outside the function as per the problem statement.

### Code Implementation

Here's the implementation in Python:

```python
class Solution:
    def Anagrams(self, words, n):
        # Create a dictionary to store groups of anagrams
        anagram_groups = {}
        
        for word in words:
            # Sort the word to create a key for the anagram group
            key = ''.join(sorted(word))
            
            # Add the word to the appropriate anagram group
            if key in anagram_groups:
                anagram_groups[key].append(word)
            else:
                anagram_groups[key] = [word]
        
        # Collect and return all groups of anagrams
        result = list(anagram_groups.values())
        return result
```

### Explanation

- **Sorting Each Word**: Sorting each word allows us to create a unique key for each group of anagrams. For example, "act", "cat", and "tac" all become "act" when sorted.

- **Hash Map Storage**: The dictionary stores each anagram group as a list of words that correspond to the same sorted key.

- **Efficiency**: This approach efficiently groups words using sorting and dictionary operations, making it suitable for the given constraints.

### Complexity Analysis

- **Time Complexity**: \(O(N |S| \log|S|)\), where \(N\) is the number of words and \(|S|\) is the average length of words. Sorting each word takes \(O(|S| \log|S|)\), and we do this for all \(N\) words.

- **Space Complexity**: \(O(N |S|)\) is required to store the words in the dictionary.

This solution effectively groups the anagrams by leveraging the sorted representation of each word as a unique key, allowing us to use dictionary operations to efficiently manage the anagram groups.
