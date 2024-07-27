# [Rabin-Karp Algorithm for Pattern Searching](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)
[GFG Solution](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)

1. **Hash Function**: Use a hash function to compute the hash value of the pattern and each substring of the text.
2. **Hash Comparison**: Compare the hash value of the pattern with the hash value of each substring.
3. **Character Matching**: When hash values match, verify by comparing characters to confirm the match.
4. **Sliding Window**: Slide the window over the text to check all possible substrings.

## Rabin-Karp Algorithm Steps
1. **Compute Hashes**:
   - Compute the hash value of the pattern.
   - Compute the hash values of all substrings of the text with the same length as the pattern.
2. **Compare Hashes**:
   - Compare the hash value of the pattern with the hash values of the substrings.
   - If a match is found, check the substring directly to handle hash collisions.
3. **Sliding Window**:
   - Update the hash value of the window as you slide over the text.

## Implementation

### Python
```python
class RabinKarp:
    def __init__(self, base=256, prime=101):
        self.base = base
        self.prime = prime
    
    def search(self, pattern, text):
        m = len(pattern)
        n = len(text)
        pattern_hash = 0
        text_hash = 0
        h = 1
        results = []
        
        # Compute the hash value of the pattern and the first window of text
        for i in range(m):
            pattern_hash = (self.base * pattern_hash + ord(pattern[i])) % self.prime
            text_hash = (self.base * text_hash + ord(text[i])) % self.prime
            if i < m - 1:
                h = (h * self.base) % self.prime
        
        # Slide the window over text
        for i in range(n - m + 1):
            # Check the hash values
            if pattern_hash == text_hash:
                # Check for hash collision by comparing characters
                if text[i:i + m] == pattern:
                    results.append(i)
            
            # Compute the hash value for the next window
            if i < n - m:
                text_hash = (self.base * (text_hash - ord(text[i]) * h) + ord(text[i + m])) % self.prime
                if text_hash < 0:
                    text_hash += self.prime
        
        return results

# Example usage
rk = RabinKarp()
print(rk.search("TEST", "THIS IS A TEST TEXT"))  # Output: [10]
print(rk.search("AABA", "AABAACAADAABAABA"))    # Output: [0, 9, 12]
```

### C++
```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class RabinKarp {
private:
    int base;
    int prime;
    
public:
    RabinKarp(int base = 256, int prime = 101) : base(base), prime(prime) {}

    vector<int> search(const string& pattern, const string& text) {
        int m = pattern.length();
        int n = text.length();
        int pattern_hash = 0;
        int text_hash = 0;
        int h = 1;
        vector<int> results;

        // Compute the hash value of the pattern and the first window of text
        for (int i = 0; i < m; ++i) {
            pattern_hash = (base * pattern_hash + pattern[i]) % prime;
            text_hash = (base * text_hash + text[i]) % prime;
            if (i < m - 1) {
                h = (h * base) % prime;
            }
        }

        // Slide the window over text
        for (int i = 0; i <= n - m; ++i) {
            // Check the hash values
            if (pattern_hash == text_hash) {
                // Check for hash collision by comparing characters
                if (text.substr(i, m) == pattern) {
                    results.push_back(i);
                }
            }

            // Compute the hash value for the next window
            if (i < n - m) {
                text_hash = (base * (text_hash - text[i] * h) + text[i + m]) % prime;
                if (text_hash < 0) {
                    text_hash += prime;
                }
            }
        }

        return results;
    }
};

// Example usage
int main() {
    RabinKarp rk;
    vector<int> result = rk.search("TEST", "THIS IS A TEST TEXT");
    for (int index : result) {
        cout << "Pattern found at index " << index << endl;
    }

    result = rk.search("AABA", "AABAACAADAABAABA");
    for (int index : result) {
        cout << "Pattern found at index " << index << endl;
    }

    return 0;
}
```

### Java
```java
import java.util.ArrayList;
import java.util.List;

class RabinKarp {
    private int base = 256;
    private int prime = 101;

    public List<Integer> search(String pattern, String text) {
        int m = pattern.length();
        int n = text.length();
        int patternHash = 0;
        int textHash = 0;
        int h = 1;
        List<Integer> results = new ArrayList<>();

        // Compute the hash value of the pattern and the first window of text
        for (int i = 0; i < m; i++) {
            patternHash = (base * patternHash + pattern.charAt(i)) % prime;
            textHash = (base * textHash + text.charAt(i)) % prime;
            if (i < m - 1) {
                h = (h * base) % prime;
            }
        }

        // Slide the window over text
        for (int i = 0; i <= n - m; i++) {
            // Check the hash values
            if (patternHash == textHash) {
                // Check for hash collision by comparing characters
                if (text.substring(i, i + m).equals(pattern)) {
                    results.add(i);
                }
            }

            // Compute the hash value for the next window
            if (i < n - m) {
                textHash = (base * (textHash - text.charAt(i) * h) + text.charAt(i + m)) % prime;
                if (textHash < 0) {
                    textHash += prime;
                }
            }
        }

        return results;
    }

    public static void main(String[] args) {
        RabinKarp rk = new RabinKarp();
        System.out.println(rk.search("TEST", "THIS IS A TEST TEXT")); // Output: [10]
        System.out.println(rk.search("AABA", "AABAACAADAABAABA")); // Output: [0, 9, 12]
    }
}
```

### JavaScript
```javascript
class RabinKarp {
    constructor(base = 256, prime = 101) {
        this.base = base;
        this.prime = prime;
    }

    search(pattern, text) {
        const m = pattern.length;
        const n = text.length;
        let patternHash = 0;
        let textHash = 0;
        let h = 1;
        const results = [];

        // Compute the hash value of the pattern and the first window of text
        for (let i = 0; i < m; i++) {
            patternHash = (this.base * patternHash + pattern.charCodeAt(i)) % this.prime;
            textHash = (this.base * textHash + text.charCodeAt(i)) % this.prime;
            if (i < m - 1) {
                h = (h * this.base) % this.prime;
            }
        }

        // Slide the window over text
        for (let i = 0; i <= n - m; i++) {
            // Check the hash values
            if (patternHash === textHash) {
                // Check for hash collision by comparing characters
                if (text.substring(i, i + m) === pattern) {
                    results.push(i);
                }
            }

            // Compute the hash value for the next window
            if (i < n - m) {
                textHash = (this.base * (textHash - text.charCodeAt(i) * h) + text.charCodeAt(i + m)) % this.prime;
                if (textHash < 0) {
                    textHash += this.prime;
                }
            }
        }

        return results;
    }
}

// Example usage
const rk = new RabinKarp();
console.log(rk.search("TEST", "THIS IS A TEST TEXT")); // Output: [10]
console.log(rk.search("AABA", "AABAACAADAABAABA")); // Output: [0, 9, 12]
```

## Complexity Analysis

- **Time Complexity**: \(O(n + m)\), where \(n\) is the length of the text and \(m\) is the length of the pattern. This is because we need to compute the hash for each substring and

 the pattern once, and sliding the window involves constant time operations.
- **Space Complexity**: \(O(1)\), since the space used is for hash values and indices, not dependent on the size of the input.

The Rabin-Karp algorithm is efficient for pattern searching in large texts with its average time complexity and straightforward hash-based approach.
