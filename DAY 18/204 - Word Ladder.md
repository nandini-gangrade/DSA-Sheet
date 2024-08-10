# [127. Word Ladder](https://leetcode.com/problems/word-ladder/description/)

To solve the problem of finding the shortest transformation sequence from `beginWord` to `endWord` using a dictionary of words, we can use the Breadth-First Search (BFS) algorithm. This problem is essentially finding the shortest path in an unweighted graph where nodes are words, and edges exist between words that differ by a single letter.

Here's a step-by-step approach to solving the problem:

### Steps to Solve the Problem

1. **Check if End Word Exists**: First, check if the `endWord` is present in the `wordList`. If it's not, return `0` since no valid transformation sequence exists.

2. **Create a Set for Fast Lookup**: Convert `wordList` into a set for O(1) average time complexity checks during BFS.

3. **Initialize BFS**: Use a queue to keep track of the current word and the current transformation length. Initialize the queue with the `beginWord` and a transformation length of `1`.

4. **BFS Traversal**:
   - For each word, generate all possible transformations by changing each letter to any letter from 'a' to 'z'.
   - For each transformed word, check if it is the `endWord`. If it is, return the current transformation length + 1.
   - If the transformed word is in the set, add it to the queue and mark it as visited by removing it from the set.

5. **Return the Result**: If the queue is exhausted without finding the `endWord`, return `0`.

### Python Implementation

Here's a Python implementation of the above approach:

```python
from collections import deque
from typing import List

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        # Step 1: Check if endWord is in the wordList
        if endWord not in wordList:
            return 0
        
        # Step 2: Create a set of words for O(1) lookups
        wordSet = set(wordList)
        
        # Step 3: Initialize BFS
        queue = deque([(beginWord, 1)])  # (current_word, current_length)
        
        while queue:
            current_word, length = queue.popleft()
            
            # Generate all possible transformations
            for i in range(len(current_word)):
                for char in 'abcdefghijklmnopqrstuvwxyz':
                    next_word = current_word[:i] + char + current_word[i+1:]
                    
                    if next_word == endWord:
                        return length + 1
                    
                    if next_word in wordSet:
                        wordSet.remove(next_word)  # Mark as visited
                        queue.append((next_word, length + 1))
        
        return 0
```

### Explanation

1. **Initialization**:
   - The `wordSet` helps in fast lookups and ensures that we only consider valid transformations.
   - The `queue` is used to manage the BFS traversal, storing the current word and its transformation length.

2. **BFS Process**:
   - For each word, generate all possible transformations by changing each letter to every letter from 'a' to 'z'.
   - If a valid transformation equals the `endWord`, return the length of the path.
   - If a valid transformation exists in the `wordSet`, enqueue it and continue the search.

3. **Completion**:
   - If the queue is empty and no transformation sequence reaches the `endWord`, return `0`.

### Complexity

- **Time Complexity**: O(N * L * 26), where N is the number of words in the `wordList`, and L is the length of each word. The factor of 26 accounts for the number of possible character transformations.
- **Space Complexity**: O(N * L) due to the storage of words in the set and the queue.

This solution efficiently finds the shortest path using BFS and handles the problem constraints effectively.
