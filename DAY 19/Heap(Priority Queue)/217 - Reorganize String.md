# [767. Reorganize String](https://leetcode.com/problems/reorganize-string/description/)

To solve the problem of rearranging the characters in the string `s` such that no two adjacent characters are the same, we can use a greedy approach with a max heap (priority queue). Here's how we can achieve this:

### Approach:

1. **Character Frequency Count**:
   - First, we'll count the frequency of each character in the string `s` using a hash map or `Counter` from the `collections` module.

2. **Max Heap**:
   - We use a max heap to always pick the character with the highest remaining frequency. In Python, since the default `heapq` is a min heap, we'll store negative frequencies to simulate a max heap.

3. **Rearranging Characters**:
   - We repeatedly pick the two most frequent characters from the heap and append them to the result string. This ensures that the most frequent characters are spaced out as much as possible.
   - After using a character, we decrease its frequency and push it back into the heap if its frequency is still greater than zero.

4. **Checking Feasibility**:
   - If at any point, the most frequent character has a frequency greater than half the remaining characters (plus one for odd lengths), it's impossible to rearrange the string to meet the criteria, and we return `""`.

### Python Implementation:

```python
import heapq
from collections import Counter

class Solution:
    def reorganizeString(self, s: str) -> str:
        # Step 1: Frequency count
        freq = Counter(s)
        
        # Step 2: Max heap (invert frequencies to use Python's min heap as max heap)
        max_heap = [(-value, key) for key, value in freq.items()]
        heapq.heapify(max_heap)
        
        # Step 3: Reorganize characters
        result = []
        prev_freq, prev_char = 0, ''
        
        while max_heap:
            freq, char = heapq.heappop(max_heap)
            result.append(char)
            
            # Since we're using the character, reduce its frequency
            if prev_freq < 0:
                heapq.heappush(max_heap, (prev_freq, prev_char))
            
            # Update the previous frequency and character
            prev_freq, prev_char = freq + 1, char  # Increase freq towards 0
        
        # Step 4: Check the result's validity
        rearranged_str = ''.join(result)
        if len(rearranged_str) != len(s):
            return ""
        
        return rearranged_str
```

### Explanation:

1. **Frequency Counting**:
   - We use `Counter` to get a dictionary of character frequencies.

2. **Heap Operations**:
   - Characters with higher frequencies are prioritized by storing them with negative frequencies in the heap.
   - We keep track of the previous character and its frequency to prevent placing the same character next to itself.

3. **Reorganizing**:
   - We build the result string by picking the character with the highest frequency and checking if the previous character (if any) can be reused.

4. **Final Check**:
   - If the length of the resulting string is equal to the original string, the rearrangement is valid. Otherwise, it's not possible to rearrange the string as required, so we return `""`.

### Time and Space Complexity:

- **Time Complexity**: \(O(n \log n)\), where \(n\) is the length of the string. This is due to the heap operations.
- **Space Complexity**: \(O(n)\) for storing the frequency map and the heap.

### Example:

- **Input**: `"aab"`
- **Output**: `"aba"`
- **Explanation**: The algorithm successfully rearranges the characters such that no two adjacent characters are the same.

- **Input**: `"aaab"`
- **Output**: `""`
- **Explanation**: It's impossible to rearrange the string so that no two adjacent characters are the same, so the function returns an empty string.

This solution ensures that we can handle strings with varying character distributions effectively and efficiently.
