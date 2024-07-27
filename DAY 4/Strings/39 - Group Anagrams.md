# [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)
[Leetcode Solution](https://leetcode.com/problems/group-anagrams/solutions/5544809/easy-solution-challenge-day-4-revisewitharsh) 

To group anagrams from a list of strings, we need to identify which words are anagrams of each other and group them together. An anagram is a word that can be formed by rearranging the letters of another word. For example, "eat", "tea", and "ate" are all anagrams.

## Approach

1. **Sorting Method**:
   - **Key Idea**: Two strings are anagrams if and only if their sorted forms are identical.
   - **Steps**:
     1. For each string in the list, sort the characters in the string.
     2. Use the sorted string as a key in a dictionary.
     3. Append the original string to the list corresponding to this key.
     4. The values of the dictionary will represent the groups of anagrams.

2. **Hashing Method** (alternative, not used here but worth mentioning):
   - **Key Idea**: Use a character frequency count to identify anagrams.
   - **Steps**:
     1. Create a frequency count of characters for each string.
     2. Use this frequency count as a key in a dictionary.
     3. Append the original string to the list corresponding to this key.

Here, I'll use the sorting method as it's straightforward and efficient enough given the constraints.

## Implementation

### Python

```python
class Solution:
    def groupAnagrams(self, strs):
        anagrams = {}
        
        for s in strs:
            # Sort the string to get the anagram key
            sorted_str = ''.join(sorted(s))
            # Group anagrams using the sorted string as a key
            if sorted_str in anagrams:
                anagrams[sorted_str].append(s)
            else:
                anagrams[sorted_str] = [s]
        
        # Return all grouped anagrams
        return list(anagrams.values())

# Example usage
solution = Solution()
print(solution.groupAnagrams(["eat","tea","tan","ate","nat","bat"]))  # Output: [["eat","tea","ate"],["tan","nat"],["bat"]]
print(solution.groupAnagrams([""]))  # Output: [[""]]
print(solution.groupAnagrams(["a"]))  # Output: [["a"]]
```

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> anagrams;
        
        for (const string& s : strs) {
            string sorted_str = s;
            sort(sorted_str.begin(), sorted_str.end());
            anagrams[sorted_str].push_back(s);
        }
        
        vector<vector<string>> result;
        for (auto& pair : anagrams) {
            result.push_back(pair.second);
        }
        
        return result;
    }
};

// Example usage
int main() {
    Solution solution;
    vector<string> input1 = {"eat","tea","tan","ate","nat","bat"};
    vector<vector<string>> result1 = solution.groupAnagrams(input1);
    for (const auto& group : result1) {
        for (const auto& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }
    
    vector<string> input2 = {""};
    vector<vector<string>> result2 = solution.groupAnagrams(input2);
    for (const auto& group : result2) {
        for (const auto& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }
    
    vector<string> input3 = {"a"};
    vector<vector<string>> result3 = solution.groupAnagrams(input3);
    for (const auto& group : result3) {
        for (const auto& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

### Java Implementation

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> anagrams = new HashMap<>();
        
        for (String s : strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String sortedStr = new String(chars);
            anagrams.computeIfAbsent(sortedStr, k -> new ArrayList<>()).add(s);
        }
        
        return new ArrayList<>(anagrams.values());
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String[] input1 = {"eat", "tea", "tan", "ate", "nat", "bat"};
        System.out.println(solution.groupAnagrams(input1)); // Output: [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
        
        String[] input2 = {""};
        System.out.println(solution.groupAnagrams(input2)); // Output: [[""]]
        
        String[] input3 = {"a"};
        System.out.println(solution.groupAnagrams(input3)); // Output: [["a"]]
    }
}
```

### JavaScript Implementation

```javascript
class Solution {
    groupAnagrams(strs) {
        const anagrams = {};
        
        for (const s of strs) {
            const sortedStr = s.split('').sort().join('');
            if (!anagrams[sortedStr]) {
                anagrams[sortedStr] = [];
            }
            anagrams[sortedStr].push(s);
        }
        
        return Object.values(anagrams);
    }
}

// Example usage
const solution = new Solution();
console.log(solution.groupAnagrams(["eat","tea","tan","ate","nat","bat"])); // Output: [["eat","tea","ate"],["tan","nat"],["bat"]]
console.log(solution.groupAnagrams([""])); // Output: [[""]]
console.log(solution.groupAnagrams(["a"])); // Output: [["a"]]
```

## Complexity Analysis

- **Time Complexity**: \(O(n \cdot k \log k)\), where \(n\) is the number of strings and \(k\) is the maximum length of a string. Sorting each string takes \(O(k \log k)\), and doing this for all strings results in \(O(n \cdot k \log k)\).
- **Space Complexity**: \(O(n \cdot k)\), as we store all the strings in the output and in the hash map.

The sorting method is efficient and straightforward for grouping anagrams, especially given the constraints.
