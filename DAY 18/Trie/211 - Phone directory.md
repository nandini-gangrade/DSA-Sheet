# [Phone directory](https://www.geeksforgeeks.org/problems/phone-directory4628/1)

To solve the problem of finding all distinct contacts that match a given query string with prefixes, we'll use a Trie data structure (also known as a prefix tree). Here's a step-by-step breakdown of the approach:

### Approach

1. **Insert Contacts into Trie**:
   - Create a Trie and insert all contacts into it. Each node in the Trie represents a character of the contacts, and branches represent different possible continuations of a string.

2. **Query the Trie**:
   - For each prefix of the query string, search the Trie for all words that start with that prefix. Collect all matching words and sort them lexicographically.

3. **Handle Missing Matches**:
   - If no words match a particular prefix, return "0".

### Implementation Details

1. **Trie Node Definition**:
   - Each node contains a character, an array of child nodes (one for each possible character), and a boolean to indicate if the node marks the end of a word.

2. **Insertion in Trie**:
   - Insert each contact into the Trie. Traverse through each character of the contact and create nodes as needed.

3. **Suggestion Generation**:
   - For each prefix, traverse the Trie. If the traversal ends successfully, collect all words from that node onward. Otherwise, return "0".

### Python Implementation

Here's a Python implementation of the above approach:

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_terminal = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_terminal = True
    
    def get_suggestions(self, prefix):
        node = self.root
        suggestions = []
        
        # Traverse to the end of the prefix
        for char in prefix:
            if char in node.children:
                node = node.children[char]
            else:
                return []
        
        # Collect all words starting from the current node
        self._collect_words(node, prefix, suggestions)
        return sorted(suggestions)
    
    def _collect_words(self, node, prefix, suggestions):
        if node.is_terminal:
            suggestions.append(prefix)
        for char, child_node in node.children.items():
            self._collect_words(child_node, prefix + char, suggestions)

class Solution:
    def displayContacts(self, n, contact, s):
        trie = Trie()
        for word in contact:
            trie.insert(word)
        
        results = []
        prefix = ""
        for char in s:
            prefix += char
            suggestions = trie.get_suggestions(prefix)
            if suggestions:
                results.append(suggestions)
            else:
                results.append(["0"])
        
        return results
```

### Explanation of the Implementation

1. **TrieNode Class**:
   - Represents each node in the Trie with a dictionary of children nodes and a boolean flag indicating if it's the end of a word.

2. **Trie Class**:
   - **`insert` Method**: Inserts a word into the Trie by creating necessary nodes.
   - **`get_suggestions` Method**: Retrieves all words starting with a given prefix.
   - **`_collect_words` Method**: Recursively collects all words starting from the given node.

3. **Solution Class**:
   - **`displayContacts` Method**: 
     - Initializes a Trie and inserts all contacts.
     - For each prefix of the query string, retrieves suggestions and formats the output.

### Complexity Analysis

- **Time Complexity**: \(O(\text{sum of lengths of all words} + \text{length of query string} \times \text{average length of matching words})\)
  - Inserting a word into the Trie takes \(O(\text{length of the word})\).
  - Collecting suggestions involves traversing the Trie and can take time proportional to the number of words and their lengths.

- **Space Complexity**: \(O(\text{sum of lengths of all words})\)
  - The Trie stores all unique prefixes and their continuations.

This approach ensures efficient prefix-based querying and adheres to the constraints of the problem.
