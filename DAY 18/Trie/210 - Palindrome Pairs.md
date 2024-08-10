# [336. Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/description/)

To solve the problem of finding all palindrome pairs in a list of unique strings, we need to identify pairs `(i, j)` such that the concatenation of `words[i]` and `words[j]` forms a palindrome.

### Approach

To achieve the required runtime complexity of \( O(\text{sum of words[i].length}) \), we can use a combination of a hash map and palindrome checking. The idea is to leverage the properties of palindromes and efficient string operations.

Here's a detailed plan:

1. **Use a Hash Map**:
   - Store each word and its index in a hash map. This allows us to quickly check if a specific substring exists in the list.

2. **Check for Palindromic Pairs**:
   - For each word, split it into two parts in every possible way. Check if one part is a palindrome and if the reverse of the other part exists in the hash map. This helps in identifying pairs where the concatenation is a palindrome.
   - Additionally, handle the case where the word is empty separately because it can create valid pairs with any palindrome.

### Detailed Implementation

Here's how you can implement this approach in Python:

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        return s == s[::-1]

    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        # Create a dictionary to store the words and their indices
        word_index = {word: i for i, word in enumerate(words)}
        result = []
        
        # Iterate through each word and check for palindrome pairs
        for i, word in enumerate(words):
            length = len(word)
            
            # Try splitting the word into two parts
            for j in range(length + 1):
                left = word[:j]
                right = word[j:]
                
                # Check if left part is a palindrome and reversed right part exists in the dictionary
                if self.isPalindrome(left):
                    reversed_right = right[::-1]
                    if reversed_right in word_index and word_index[reversed_right] != i:
                        result.append([word_index[reversed_right], i])
                
                # Check if right part is a palindrome and reversed left part exists in the dictionary
                if j != length and self.isPalindrome(right):  # avoid double-checking when left is empty
                    reversed_left = left[::-1]
                    if reversed_left in word_index and word_index[reversed_left] != i:
                        result.append([i, word_index[reversed_left]])
        
        return result
```

### Explanation

1. **Helper Function `isPalindrome`**:
   - This function checks if a string is a palindrome by comparing it with its reverse.

2. **Main Function `palindromePairs`**:
   - Build a hash map `word_index` to store each word's index for quick look-up.
   - Iterate through each word and attempt to split it into every possible pair of `left` and `right` substrings.
   - Check if the `left` substring is a palindrome and if the reversed `right` substring exists in the dictionary (and is not the same word).
   - Similarly, check if the `right` substring is a palindrome and if the reversed `left` substring exists in the dictionary (and is not the same word).
   - Avoid checking the same pair twice by ensuring the split is not redundant.

### Complexity

- **Time Complexity**: \( O(\text{sum of words[i].length}) \)
  - Checking each split takes linear time with respect to the length of the word.
  - Hash map operations (insertion and look-up) are average \( O(1) \).

- **Space Complexity**: \( O(n \cdot m) \)
  - Where \( n \) is the number of words and \( m \) is the average length of the words, due to the storage in the hash map and intermediate results.

This solution efficiently finds all palindrome pairs by leveraging string operations and hash map look-ups.
