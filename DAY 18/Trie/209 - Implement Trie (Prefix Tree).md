# [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/)

To implement a `Trie` (prefix tree), we need to handle three primary operations efficiently:

1. **Insert a word**: This operation involves adding a word to the trie and ensuring that all characters are stored in the appropriate nodes.
2. **Search for a word**: This operation checks if a given word exists in the trie.
3. **Check if any word starts with a given prefix**: This operation checks if there's any word in the trie that begins with a specified prefix.

### Data Structure Design

- **TrieNode**: Each node in the trie represents a single character. It will contain:
  - `children`: A dictionary mapping characters to their corresponding child nodes.
  - `is_end_of_word`: A boolean flag indicating if the current node represents the end of a valid word.

- **Trie**: The main trie data structure that will:
  - **Insert** words by traversing or creating nodes.
  - **Search** for exact matches of words.
  - **Check** for prefixes.

### Implementation

Here's how we can implement the `Trie` class in Python:

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
    
    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word
    
    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True

# Example usage:
trie = Trie()
trie.insert("apple")
print(trie.search("apple"))   # Output: True
print(trie.search("app"))     # Output: False
print(trie.startsWith("app")) # Output: True
trie.insert("app")
print(trie.search("app"))     # Output: True
```

### Explanation

1. **TrieNode Class**:
   - `children`: A dictionary where keys are characters and values are `TrieNode` instances.
   - `is_end_of_word`: Indicates if the node represents the end of a valid word.

2. **Trie Class**:
   - `insert(word)`: Traverse the trie, creating new nodes as needed. Mark the end of the word with `is_end_of_word`.
   - `search(word)`: Traverse the trie according to the characters of the word. Return `True` if the word is found and `is_end_of_word` is `True`.
   - `startsWith(prefix)`: Traverse the trie according to the characters of the prefix. Return `True` if the traversal completes successfully, indicating that some word starts with the given prefix.

### Complexity

- **Insert**: O(m), where m is the length of the word being inserted.
- **Search**: O(m), where m is the length of the word being searched.
- **startsWith**: O(p), where p is the length of the prefix being checked.

This implementation handles up to the constraints efficiently and provides the required functionality for the `Trie` data structure.
