# [Smallest window in a string containing all the characters of another string](https://www.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string-1587115621/1)
[GFG Solution](https://discuss.geeksforgeeks.org/comment/9e592e06-5122-4589-bb16-e724bd0a387b/practice)

Given two strings `S` and `P`, find the smallest window in `S` that contains all characters of `P`, including duplicates. If there are multiple smallest windows, return the one with the lowest starting index. Return "-1" if no such window exists.

## Intuition
The problem requires us to find a substring of `S` that contains all characters of `P` with their respective frequencies. We need to efficiently track which characters are in our current window and check if it satisfies the requirement of containing all characters of `P`.

## Approach
1. **Use a sliding window** to traverse `S` with two pointers (`left` and `right`).
2. **Track character frequencies**: Use two maps (or arrays) to count the characters in `P` and the current window in `S`.
3. **Expand the window** by moving `right` to include more characters from `S` until the window contains all characters of `P`.
4. **Contract the window** by moving `left` to find the smallest valid window.
5. **Update the result** whenever a valid window (one containing all characters of `P`) is found.
6. Return the smallest window or "-1" if no such window exists.

## Code Implementation

### Python
```python
from collections import Counter

class Solution:
    def smallestWindow(self, s: str, p: str) -> str:
        if not s or not p or len(p) > len(s):
            return "-1"

        # Frequency map for characters in P
        char_count = Counter(p)
        required = len(char_count)
        left, right = 0, 0
        formed = 0

        # Current window character counts
        window_counts = {}

        # Result variables
        min_length = float('inf')
        min_window = (-1, -1)

        while right < len(s):
            char = s[right]
            window_counts[char] = window_counts.get(char, 0) + 1

            if char in char_count and window_counts[char] == char_count[char]:
                formed += 1

            while left <= right and formed == required:
                char = s[left]

                window_length = right - left + 1
                if window_length < min_length:
                    min_length = window_length
                    min_window = (left, right)

                window_counts[char] -= 1
                if char in char_count and window_counts[char] < char_count[char]:
                    formed -= 1

                left += 1

            right += 1

        if min_window[0] == -1:
            return "-1"
        else:
            return s[min_window[0]:min_window[1] + 1]

# Example usage
S1 = "timetopractice"
P1 = "toc"
solution = Solution()
print(solution.smallestWindow(S1, P1))  # Output: "toprac"
```

### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <climits>

using namespace std;

class Solution {
public:
    string smallestWindow(string s, string p) {
        if (s.empty() || p.empty() || p.length() > s.length()) {
            return "-1";
        }

        unordered_map<char, int> char_count;
        for (char c : p) {
            char_count[c]++;
        }

        int required = char_count.size();
        int left = 0, right = 0, formed = 0;
        unordered_map<char, int> window_counts;

        int min_length = INT_MAX;
        int min_left = 0;

        while (right < s.length()) {
            char c = s[right];
            window_counts[c]++;

            if (char_count.find(c) != char_count.end() && window_counts[c] == char_count[c]) {
                formed++;
            }

            while (left <= right && formed == required) {
                char c = s[left];

                if (right - left + 1 < min_length) {
                    min_length = right - left + 1;
                    min_left = left;
                }

                window_counts[c]--;
                if (char_count.find(c) != char_count.end() && window_counts[c] < char_count[c]) {
                    formed--;
                }

                left++;
            }

            right++;
        }

        return min_length == INT_MAX ? "-1" : s.substr(min_left, min_length);
    }
};

// Example usage
int main() {
    Solution solution;
    string S1 = "timetopractice";
    string P1 = "toc";
    cout << solution.smallestWindow(S1, P1) << endl;  // Output: "toprac"
    return 0;
}
```

### Java
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public String smallestWindow(String s, String p) {
        if (s.isEmpty() || p.isEmpty() || p.length() > s.length()) {
            return "-1";
        }

        Map<Character, Integer> charCount = new HashMap<>();
        for (char c : p.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }

        int required = charCount.size();
        int left = 0, right = 0, formed = 0;
        Map<Character, Integer> windowCounts = new HashMap<>();

        int minLength = Integer.MAX_VALUE;
        int minLeft = 0;

        while (right < s.length()) {
            char c = s.charAt(right);
            windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);

            if (charCount.containsKey(c) && windowCounts.get(c).equals(charCount.get(c))) {
                formed++;
            }

            while (left <= right && formed == required) {
                c = s.charAt(left);

                if (right - left + 1 < minLength) {
                    minLength = right - left + 1;
                    minLeft = left;
                }

                windowCounts.put(c, windowCounts.get(c) - 1);
                if (charCount.containsKey(c) && windowCounts.get(c) < charCount.get(c)) {
                    formed--;
                }

                left++;
            }

            right++;
        }

        return minLength == Integer.MAX_VALUE ? "-1" : s.substring(minLeft, minLeft + minLength);
    }

    // Example usage
    public static void main(String[] args) {
        Solution solution = new Solution();
        String S1 = "timetopractice";
        String P1 = "toc";
        System.out.println(solution.smallestWindow(S1, P1));  // Output: "toprac"
    }
}
```

### JavaScript
```javascript
class Solution {
    smallestWindow(s, p) {
        if (!s || !p || p.length > s.length) {
            return "-1";
        }

        const charCount = new Map();
        for (const char of p) {
            charCount.set(char, (charCount.get(char) || 0) + 1);
        }

        const required = charCount.size;
        let left = 0;
        let right = 0;
        let formed = 0;
        const windowCounts = new Map();

        let minLength = Infinity;
        let minLeft = 0;

        while (right < s.length) {
            const char = s[right];
            windowCounts.set(char, (windowCounts.get(char) || 0) + 1);

            if (charCount.has(char) && windowCounts.get(char) === charCount.get(char)) {
                formed++;
            }

            while (left <= right && formed === required) {
                if (right - left + 1 < minLength) {
                    minLength = right - left + 1;
                    minLeft = left;
                }

                const charLeft = s[left];
                windowCounts.set(charLeft, windowCounts.get(charLeft) - 1);
                if (charCount.has(charLeft) && windowCounts.get(charLeft) < charCount.get(charLeft)) {
                    formed--;
                }

                left++;
            }

            right++;
        }

        return minLength === Infinity ? "-1" : s.substring(minLeft, minLeft + minLength);
    }
}

// Example usage
const solution = new Solution();
const S1 = "timetopractice";
const P1 = "toc";
console.log(solution.smallestWindow(S1, P1));  // Output: "toprac"
```

## Complexity Analysis

- **Time Complexity**: \(O(|S| + |P|)\)
  - Each character in \( S \) is processed at most twice (once by `right` and once by `left`).
  - Constructing the frequency map for \( P \) takes \( O(|P|) \).

- **Space Complexity**: \(O(|P|)\)
  - The hash map `char_count` stores the frequency of each character in \( P \).
  - The `window_counts` map stores the current counts of characters in the window.

The implementations efficiently find the smallest window using the sliding window technique and hash maps, making them suitable for large input sizes as specified in the constraints.
