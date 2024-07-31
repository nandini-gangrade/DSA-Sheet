## #CrackYourInternship #CrackYourPlacement Challenge - #ReviseWithArsh!

Over the next 45 days, I’ll be working through a curated DSA sheet to sharpen my skills for upcoming interviews and assessments.
Huge thanks to Arsh Goyal for creating this fantastic [resource](https://lnkd.in/d35yKrSW)! 🙌


<!-- Easy Solution 🚀 | Challenge - Day 4 - #ReviseWithArsh 🙌
`#CrackYourInternship #CrackYourPlacement Challenge - #ReviseWithArsh
`

> DAY 4
1 - Longest Common Prefix
2 - Valid Palindrome II
3 - Integer to Roman
4 - Generate Parentheses
5 - Simplify Path
6 - Smallest window in a string containing all the characters of another string
7 - Reverse Words in a String.md
8 - Rabin-Karp Algorithm for Pattern Searching
9 - Group Anagrams
10 - Word Wrap
11 - Basic Calculator II
11 - Valid number


### Approach

1. **Initialization**:
   - **`need`**: A Counter to store the frequency of each character in `t`.
   - **`window`**: A defaultdict to store the frequency of each character in the current window of `s`.
   - **`have`**: A count of how many unique characters from `t` are currently in the window with the required frequency.
   - **`required`**: The number of unique characters needed in the window, which is the size of the `need` Counter.
   - **`res`**: A tuple to keep track of the minimum window length and its start and end indices.

2. **Sliding Window**:
   - Expand the window by moving the `right` pointer and update the `window` Counter.
   - If the window contains all the required characters with the correct frequencies, try to shrink the window from the left using the `left` pointer.
   - Keep track of the smallest valid window found.

3. **Edge Cases**:
   - If `t` is longer than `s`, immediately return an empty string because it's impossible to find such a window.

### Code Implementation

```python []
from collections import Counter, defaultdict

class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if not s or not t:
            return ""

        # Frequency count of characters in t
        need = Counter(t)
        window = defaultdict(int)
        
        # Number of unique characters that match the requirement
        have = 0
        required = len(need)
        
        # Result tuple (window length, left, right)
        res = float('inf'), None, None
        
        left = 0
        
        # Expand the window with the right pointer
        for right in range(len(s)):
            char = s[right]
            window[char] += 1
            
            # Check if the current character satisfies the requirement
            if char in need and window[char] == need[char]:
                have += 1
            
            # Shrink the window from the left as long as it's valid
            while have == required:
                # Update the result if the current window is smaller
                if (right - left + 1) < res[0]:
                    res = (right - left + 1, left, right)
                
                # Move the left pointer
                window[s[left]] -= 1
                if s[left] in need and window[s[left]] < need[s[left]]:
                    have -= 1
                left += 1
        
        # Return the smallest window found
        return "" if res[0] == float('inf') else s[res[1]:res[2] + 1]
```

### Explanation

- **Initialization**:
  - **`need`**: Tracks the count of each character required.
  - **`window`**: Keeps track of characters in the current window of `s`.
  - **`have`**: Counts how many unique characters from `t` are met in the current window with required frequency.
  - **`res`**: Stores the smallest valid window size and its position.

- **Sliding Window Mechanism**:
  - The right pointer (`right`) expands the window.
  - When the window is valid (i.e., contains all required characters with the correct frequency), the left pointer (`left`) is used to contract the window to find the minimum size.
  - The result is updated whenever a smaller valid window is found.

### Complexity

- **Time Complexity**: \(O(m + n)\)
  - The two pointers (`left` and `right`) traverse the string `s` at most once, and operations with hashmaps are constant time on average.

- **Space Complexity**: \(O(n)\)
  - The hashmaps `need` and `window` store character frequencies where `n` is the length of string `t`.

This approach is efficient and handles large inputs well within the given constraints.

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
-->

<!--

`#CrackYourInternship #CrackYourPlacement Challenge - #ReviseWithArsh
`

> DAY 5

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`

-->

### Coding Challenge Track

| Day   | Problem                                | Solution                                                                                  | Repo/Post Link                                   |
|-------|----------------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------|
| **Day 1** | [1. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | [LeetCode Solution](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solutions/5524617/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/1%20-%20Remove%20Duplicates%20from%20Sorted%20Array.md)|
|  | [2. Move Zeros](https://leetcode.com/problems/move-zeroes/description/) | [LeetCode Solution](https://leetcode.com/problems/move-zeroes/solutions/5524919/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/2%20-%20Move%20Zeroes.md)|
|  | [3. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/) | [LeetCode Solution](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/solutions/5524972/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/3%20-%20Best%20Time%20to%20Buy%20and%20Sell%20Stock.md)|
|  | [4. Chocolate Distribution Problem](https://www.geeksforgeeks.org/problems/chocolate-distribution-problem3825/1) | [GFG Solution](https://discuss.geeksforgeeks.org/comment/d0ca575e-1df7-4b5e-96cb-55941a171e06/practice) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/4%20-%20Chocolate%20Distribution%20Problem.md)|
|  | [5. Two Sum](https://leetcode.com/problems/two-sum/description/) | [LeetCode Solution](https://leetcode.com/problems/two-sum/solutions/5525028/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/5%20-%20Two%20Sum.md)|
|  | [6. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/) | [LeetCode Solution](https://leetcode.com/problems/merge-sorted-array/solutions/5525044/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/6%20-%20Merge%20Sorted%20Array.md)|
|  | [7. Majority Element](https://leetcode.com/problems/majority-element/description/) | [Leetcode Solution](https://leetcode.com/problems/majority-element/solutions/5525064/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/7%20-%20Majority%20Element.md)|
|  | [8. Set Matrix Zeroes](https://leetcode.com/problems/majority-element/description/) | [Leetcode Solution](https://leetcode.com/problems/set-matrix-zeroes/solutions/5527966/best-solution-challenge-day-1-revisewitharsh/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%201/Arrays/8%20-%20Set%20Matrrix%20Zero.md)|
|  |  |  |  |
| **Day 2** | [9. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/) | [LeetCode Solution](https://leetcode.com/problems/find-the-duplicate-number/solutions/5528716/best-solution-challenge-day-2-revisewitharsh/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/9%20-%20Find%20the%20Duplicate%20Number.md)|
| | [10. Sort Colors](https://leetcode.com/problems/sort-colors/description/) | [LeetCode Solution](https://leetcode.com/problems/sort-colors/solutions/5529132/best-solution-challenge-day-2-revisewitharsh/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/10%20-%20Sort%20Colors.md)|
| | [11. Subarray Sums Divisible by K](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/) | [LeetCode Solution](https://leetcode.com/problems/subarray-sums-divisible-by-k/solutions/3071714/easy-video-explaination-step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/12%20-%20Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.md)|
| | [12. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/) | [LeetCode Solution](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/solutions/5535198/best-solution-challenge-day-2-revisewitharsh/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/12%20-%20Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.md)|
| | [13. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/description/) | [LeetCode Solution](https://leetcode.com/problems/find-all-duplicates-in-an-array/solutions/5535347/step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/10%20-%20Sort%20Colors.md)|
| | [14. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/) | [LeetCode Solution](https://leetcode.com/problems/container-with-most-water/solutions/5535434/step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/14%20-%20Container%20With%20Most%20Water.md)|
| | [15. 3Sum](https://leetcode.com/problems/3sum/description/) | [LeetCode Solution](https://leetcode.com/problems/3sum/solutions/3697940/step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/15%20-%203Sum.md)|
| | [16. 4Sum](https://leetcode.com/problems/4sum/description/) | [LeetCode Solution](https://leetcode.com/problems/4sum/solutions/5535754/step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/16%20-%204Sum.md)|
| | [17. Maximum Points You Can Obtain from Cards](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/description/) | [LeetCode Solution](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/solutions/5535805/step-by-step-explanation-challenge-day-2-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%202/Arrays/17%20-%20Maximum%20Points%20You%20Can%20Obtain%20from%20Cards.md)|
|  |  |  |  |
| **Day 3** | [18. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/description/) | [LeetCode Solution](https://leetcode.com/problems/subarray-sum-equals-k/solutions/5535865/step-by-step-explanation-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/18%20-%20Subarray%20Sum%20Equals%20K.md)|
| | [19. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/) | [LeetCode Solution](https://leetcode.com/problems/spiral-matrix/solutions/5535979/step-by-step-explanation-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/19%20-%20Spiral%20Matrix.md)|
| | [20. Word Search](https://leetcode.com/problems/word-search/description/) | [LeetCode Solution](https://leetcode.com/problems/word-search/solutions/5539919/step-by-step-explanation-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/20%20-%20Word%20Search.md)|
| | [21. Jump Game](https://leetcode.com/problems/jump-game/description/) | [LeetCode Solution](https://leetcode.com/problems/jump-game/solutions/5539964/step-by-step-explanation-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/21%20-%20Jump%20Game.md)|
| | [22. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/description/) | [LeetCode Solution](https://leetcode.com/problems/reverse-pairs/solutions/5539989/step-by-step-explanation-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/22%20-%20Reverse%20Pairs.md)|
| | [23. All Unique Permutations of an array](https://www.geeksforgeeks.org/problems/all-unique-permutations-of-an-array/0) | [GFG Solution](https://discuss.geeksforgeeks.org/comment/84426098-68a0-49f1-adcf-9b5160fa33fb/practice) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/23%20-%20All%20Unique%20Permutations%20of%20an%20array.md)|
| | [24. Game of Life](https://leetcode.com/problems/game-of-life/description/) | [LeetCode Solution](https://leetcode.com/problems/game-of-life/solutions/5540092/best-solution-challenge-day-1-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/24%20-%20Game%20of%20Life.md)|
| | [25. Max Value of Equation](https://leetcode.com/problems/max-value-of-equation/description/) | [LeetCode Solution](https://leetcode.com/problems/max-value-of-equation/solutions/5540158/best-solution-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/25%20-%20Max%20Value%20of%20Equation.md)|
| | [26. Insert Delete GetRandom O(1) - Duplicates allowed](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/description/) | [LeetCode Solution](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/solutions/5540249/best-solution-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/26%20-%20Insert%20Delete%20GetRandom%20O(1)%20-%20Duplicates%20allowed.md)|
| | [27. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/) | [LeetCode Solution](https://leetcode.com/problems/largest-rectangle-in-histogram/solutions/5540315/best-solution-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/27%20-%20Largest%20Rectangle%20in%20Histogram.md)|
| | [28. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/) | [LeetCode Solution](https://leetcode.com/problems/largest-rectangle-in-histogram/solutions/5540315/best-solution-challenge-day-3-revisewitharshttps://leetcode.com/problems/valid-parentheses/solutions/5540421/best-solution-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Strings/28%20-%20Valid%20Parentheses.md)|
| | [29 - Print all the duplicate characters in a string.md](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/) | [GFG Blog](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Arrays/19%20-%20Spiral%20Matrix.md)|
| | [30 - Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/) | [LeetCode Solution](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/solutions/5540533/short-best-solution-challenge-day-3-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%203/Strings/30%20-%20Find%20the%20Index%20of%20the%20First%20Occurrence%20in%20a%20String.md)|
|  |  |  |  |
| **Day 4** | [31. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/) | [LeetCode Solution](https://leetcode.com/problems/longest-common-prefix/solutions/5544354/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/31.%20Longest%20Common%20Prefix.md)|
| | [32. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/description/) | [LeetCode Solution](https://leetcode.com/problems/valid-palindrome-ii/solutions/5544401/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/33%20-%20Integer%20to%20Roman.md)|
| | [33. Integer to Roman](https://leetcode.com/problems/integer-to-roman/description/) | [LeetCode Solution](https://leetcode.com/problems/integer-to-roman/solutions/5544454/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/32%20-%20Valid%20Palindrome%20II.md)|
| | [34. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/) | [LeetCode Solution](https://leetcode.com/problems/generate-parentheses/solutions/5544515/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/34%20-%20Generate%20Parentheses.md)|
| | [35. Simplify Path2](https://leetcode.com/problems/simplify-path/description/) | [LeetCode Solution](https://leetcode.com/problems/simplify-path/solutions/5544547/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/35%20-%20Simplify%20Path.md)|
| | [36. Smallest window in a string containing all the characters of another string](https://www.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string-1587115621/1) | [GFG Solution](https://discuss.geeksforgeeks.org/comment/9e592e06-5122-4589-bb16-e724bd0a387b/practice) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/36%20-%20Smallest%20window%20in%20a%20string%20containing%20all%20the%20characters%20of%20another%20string.md)|
| | [37. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/) | [Leetcode Solution](https://leetcode.com/problems/reverse-words-in-a-string/solutions/5544710/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/37%20-%20Reverse%20Words%20in%20a%20String.md)|
| | [38. Rabin-Karp Algorithm for Pattern Searching](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/) | [GFG Solution](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/38%20-%20Rabin-Karp%20Algorithm%20for%20Pattern%20Searching.md)|
| | [39. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/) | [Leetcode Solution](https://leetcode.com/problems/group-anagrams/solutions/5544809/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/39%20-%20Group%20Anagrams.md)|
| | [40. Word Wrap](https://www.geeksforgeeks.org/problems/word-wrap1646/1) | [GFG Solution](https://discuss.geeksforgeeks.org/comment/ea64e30a-90f0-4a3b-a053-7c9419a86dde/practice) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/40%20-%20Word%20Wrap.md)|
| | [41. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/description/) | [Leetcode Solution](https://leetcode.com/problems/basic-calculator-ii/solutions/5544990/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/41%20-%20Basic%20Calculator%20II.md)|
| | [42. Valid Number](https://leetcode.com/problems/valid-number/description/) | [Leetcode Solution](https://leetcode.com/problems/valid-number/solutions/5545088/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/42%20-%20Valid%20Number.md)|
| | [43. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/description/) | [Leetcode Solution](https://leetcode.com/problems/integer-to-english-words/solutions/5545280/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/43%20-%20Integer%20to%20English%20Words.md)|Minimum Window Substring
| | [44. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/) | [Leetcode Solution](https://leetcode.com/problems/integer-to-english-words/solutions/5545280/easy-solution-challenge-day-4-revisewitharsh) | [GitHub Solution Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%204/Strings/43%20-%20Integer%20to%20English%20Words.md)|

| Day   | Problem                                | GitHub Solution                                                                                              |
|-------|----------------------------------------|----------------------------------------------------------------------------------------------|
| **Day 5** | [45. Text Justification](https://leetcode.com/problems/text-justification/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/45%20-%20Text%20Justification.md) | 
|  | [46. Boyer Moore Algorithm for Pattern Searching](https://www.geeksforgeeks.org/boyer-moore-algorithm-for-pattern-searching/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/46%20-%20Boyer%20Moore%20Algorithm%20for%20Pattern%20Searching.md)
|  | [47. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/47%20-%20Distinct%20Subsequences.md)
|  | [48. Print Anagrams Together](https://www.geeksforgeeks.org/problems/print-anagrams-together/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/48%20-%20Print%20Anagrams%20Together.md)
|  | [49. Maximum size rectangle binary sub-matrix with all 1s](https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/49%20-%20Maximum%20size%20rectangle%20binary%20sub-matrix%20with%20all%201s.md)
|  | [50. Find the number of islands using DFS](https://www.geeksforgeeks.org/find-the-number-of-islands-using-dfs/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/50%20-%20Find%20the%20number%20of%20islands%20using%20DFS.md)
|  | [51. Given a matrix of ‘O’ and ‘X’, replace ‘O’ with ‘X’ if surrounded by ‘X’](https://www.geeksforgeeks.org/given-matrix-o-x-replace-o-x-surrounded-x/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/51%20-%20Given%20a%20matrix%20of%20%E2%80%98O%E2%80%99%20and%20%E2%80%98X%E2%80%99%2C%20replace%20%E2%80%98O%E2%80%99%20with%20%E2%80%98X%E2%80%99%20if%20surrounded%20by%20%E2%80%98X%E2%80%99.md)
|  | [52. Rotate Image](https://leetcode.com/problems/rotate-image/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/52-%20Rotate%20Image.md)
|  | [53. Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/52-%20Rotate%20Image.md)
|  | [54. Add Binary](https://leetcode.com/problems/add-binary/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/54%20-%20Add%20Binary.md)
|  | [55. Maximum Product of Three Numbers](https://leetcode.com/problems/maximum-product-of-three-numbers/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/55%20-%20Maximum%20Product%20of%20Three%20Numbers.md)
|  | [56. Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%205/Strings/56%20-%20Excel%20Sheet%20Column%20Title.md)
| **Day 6** | [57. Product array puzzle](https://www.geeksforgeeks.org/problems/product-array-puzzle4525/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Mathematical/57%20-%20Product%20array%20puzzle.md) | 
|  | [58. Permute two arrays such that sum of every pair is greater or equal to K](https://www.geeksforgeeks.org/permute-two-arrays-sum-every-pair-greater-equal-k/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/58%20-%20Permute%20two%20arrays%20such%20that%20sum%20of%20every%20pair%20is%20greater%20or%20equal%20to%20K.md)
|  | [59. Ceiling in a sorted array](https://www.geeksforgeeks.org/ceiling-in-a-sorted-array/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/59%20-%20Ceiling%20in%20a%20sorted%20array.md)
|  | [60. Find Pair Given Difference](https://www.geeksforgeeks.org/problems/find-pair-given-difference1559/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/60%20-%20Find%20Pair%20Given%20Difference.md)
|  | [61. Permutations in array](https://www.geeksforgeeks.org/problems/permutations-in-array1747/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/61%20-%20Permutations%20in%20array.md)
|  | [62. Check if reversing a sub array make the array sorted](https://www.geeksforgeeks.org/check-reversing-sub-array-make-array-sorted/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/62%20-%20Check%20if%20reversing%20a%20sub%20array%20make%20the%20array%20sorted.md)
|  | [63. Radix Sort – Data Structures and Algorithms Tutorials](https://www.geeksforgeeks.org/radix-sort/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/63%20-%20Radix%20Sort%20%E2%80%93%20Data%20Structures%20and%20Algorithms%20Tutorials.md)
|  | [64. Make all array elements equal with minimum cost](https://www.geeksforgeeks.org/make-array-elements-equal-minimum-cost/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/64%20-%20Make%20all%20array%20elements%20equal%20with%20minimum%20cost.md)
|  | [65. Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/65%20-%20Allocate%20Minimum%20Pages.md)
|  | [66. AGGRCOW - Aggressive cows](https://www.spoj.com/problems/AGGRCOW/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/66%20-%20AGGRCOW%20-%20Aggressive%20cows.md)
|  | [67 - Minimum Swaps to Sort](https://www.geeksforgeeks.org/problems/minimum-swaps/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/67%20-%20Minimum%20Swaps%20to%20Sort.md)
|  | [68 - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/68%20-%20Search%20in%20Rotated%20Sorted%20Array.md)
|  | [69 - Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/69%20-%20Count%20of%20Smaller%20Numbers%20After%20Self.md)
|  | [70 - Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/70%20-%20Split%20Array%20Largest%20Sum.md)
|  | [71 - Smallest Positive Missing](https://www.geeksforgeeks.org/problems/smallest-positive-missing-number-1587115621/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%206/Sorting%20%26%20Searching/71%20-%20Smallest%20Positive%20Missing.md)
| **Day 7** | [72 - Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/72%20-%20Middle%20of%20the%20Linked%20List.md) | 
|  | [73 - Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/73%20-%20Linked%20List%20Cycle.md)
|  | [74 - Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/74%20-%20Convert%20Binary%20Number%20in%20a%20Linked%20List%20to%20Integer.md)
|  | [75 - Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/75%20-%20Remove%20Duplicates%20from%20Sorted%20List.md)
|  | [76 - Sort a linked list of 0s, 1s and 2s](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/76%20-%20Sort%20a%20linked%20list%20of%200s%2C%201s%20and%202s.md)
|  | [77 - Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/77%20-%20Remove%20Linked%20List%20Elements.md)
|  | [78 - Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/78%20-%20Merge%20Two%20Sorted%20Lists.md)
|  | [79 - Multiply two linked lists](https://www.geeksforgeeks.org/problems/multiply-two-linked-lists/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/79%20-%20Multiply%20two%20linked%20lists.md)
|  | [80 -  Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/80%20-%20%20Intersection%20of%20Two%20Linked%20Lists.md)
|  | [81 - Delete nodes having greater value on right](https://www.geeksforgeeks.org/problems/delete-nodes-having-greater-value-on-right/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/81%20-%20Delete%20nodes%20having%20greater%20value%20on%20right.md)
|  | [82 - Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/82%20-%20Palindrome%20Linked%20List.md)
|  | [83 - Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/83%20-%20Reverse%20Linked%20List.md)
|  | [84 - Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/84%20-%20Add%20Two%20Numbers.md)
|  | [85 - Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/85%20-%20Copy%20List%20with%20Random%20Pointer.md)
|  | [86 - Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/86%20-%20Add%20Two%20Numbers%20II.md)
|  | [87 - Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/87%20-%20Reverse%20Linked%20List%20II.md)
|  | [88 - Reorder List](https://leetcode.com/problems/reorder-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/88%20-%20Reorder%20List.md)
|  | [89 - Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/89%20-%20Remove%20Nth%20Node%20From%20End%20of%20List.md)
|  | [90 - Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/84%20-%20Add%20Two%20Numbers.md)
|  | [91 - Partition List](https://leetcode.com/problems/partition-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/91%20-%20Partition%20List.md)
|  | [92 - Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/92%20-%20Remove%20Duplicates%20from%20Sorted%20List%20II.md)
|  | [93 - Rearrange a Linked List in Zig-Zag fashion](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%207/Linked%20List/93%20-%20Rearrange%20a%20Linked%20List%20in%20Zig-Zag%20fashion.md)
| **Day 8** | [94 - Rearrange a Linked List in Zig-Zag fashion](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/94%20-%20Rearrange%20a%20Linked%20List%20in%20Zig-Zag%20fashion.md) | 
|  | [95 - Sort List](https://leetcode.com/problems/sort-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/95%20-%20Sort%20List.md)
|  | [96 - Segregate even and odd nodes in a Linked List](https://leetcode.com/problems/linked-list-cycle/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/96%20-%20Segregate%20even%20and%20odd%20nodes%20in%20a%20Linked%20List.md)
|  | [97 - Rearrange a given linked list in-place](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/97%20-%20Rearrange%20a%20given%20linked%20list%20in-place.md)
|  | [98 - Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/98%20-%20Merge%20k%20Sorted%20Lists.md)
|  | [99 - Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/99%20-%20Reverse%20Nodes%20in%20k-Group.md)
|  | [100 - Subtraction in Linked List](https://www.geeksforgeeks.org/problems/subtraction-in-linked-list/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/100%20-%20Subtraction%20in%20Linked%20List.md)
|  | [101 - Flattening a Linked List](https://www.geeksforgeeks.org/problems/flattening-a-linked-list/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/101%20-%20Flattening%20a%20Linked%20List.md)


![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solutions/5524617/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀
`
