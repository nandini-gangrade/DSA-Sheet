# [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

To implement the `WordDictionary` class, which supports adding words and searching with potential wildcard characters ('.'), a Trie (prefix tree) is a suitable data structure. Here's a step-by-step explanation and implementation of the `WordDictionary` class using a Trie.

### Trie Data Structure

A Trie is a tree-like data structure used to efficiently store and retrieve keys in a dataset of strings. It is particularly useful for problems involving prefix-based queries. For this problem, a Trie will allow us to:

1. **Add words**: Insert words into the Trie with each character representing a node in the Trie.
2. **Search words**: Support exact matches and pattern matching where '.' can represent any character.

### Key Components

1. **Trie Node**: Each node contains:
   - `children`: A dictionary mapping characters to their corresponding child nodes.
   - `is_end_of_word`: A boolean indicating if the node marks the end of a valid word.

2. **Trie Operations**:
   - **Insert**: Add a word to the Trie.
   - **Search**: Search for a word or pattern where '.' can match any character.

### Implementation

Here's the implementation of the `WordDictionary` class using a Trie:

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class WordDictionary:

    def __init__(self):
        self.root = TrieNode()
    
    def addWord(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
    
    def search(self, word: str) -> bool:
        def search_in_node(word: str, node: TrieNode) -> bool:
            if not word:
                return node.is_end_of_word
            
            char = word[0]
            if char == '.':
                # Explore all possible children
                for child in node.children.values():
                    if search_in_node(word[1:], child):
                        return True
                return False
            else:
                if char in node.children:
                    return search_in_node(word[1:], node.children[char])
                return False
        
        return search_in_node(word, self.root)

# Example usage:
wordDictionary = WordDictionary()
wordDictionary.addWord("bad")
wordDictionary.addWord("dad")
wordDictionary.addWord("mad")
print(wordDictionary.search("pad"))  # Output: False
print(wordDictionary.search("bad"))  # Output: True
print(wordDictionary.search(".ad"))  # Output: True
print(wordDictionary.search("b.."))  # Output: True
```

### Explanation

1. **Initialization (`__init__`)**:
   - Initialize the `WordDictionary` with an empty root TrieNode.

2. **Adding Words (`addWord`)**:
   - Traverse the Trie, creating new nodes as needed for each character in the word.
   - Mark the end of the word by setting `is_end_of_word` to `True`.

3. **Searching Words (`search`)**:
   - Implement a helper function `search_in_node` to handle the recursion for pattern matching.
   - For '.' characters, recursively search all possible children nodes.
   - For other characters, continue searching along the corresponding child node.

### Time Complexity

- **Adding a word**: O(L), where L is the length of the word. Each character is processed once.
- **Searching a word**: O(L * 3^D), where L is the length of the word and D is the number of '.' characters (each '.' can lead to up to 3 possible children nodes to explore).

### Space Complexity

- **Space for Trie**: O(N * L), where N is the number of words and L is the average length of the words. Each node in the Trie represents a unique character in the words added.

This implementation efficiently handles the constraints and provides a clear and concise way to manage and search for words and patterns in the `WordDictionary`.
