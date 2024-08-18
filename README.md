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
| | | |
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
| | | |
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
| | | |
| **Day 8** | [94 - Rearrange a Linked List in Zig-Zag fashion](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/94%20-%20Rearrange%20a%20Linked%20List%20in%20Zig-Zag%20fashion.md) | 
|  | [95 - Sort List](https://leetcode.com/problems/sort-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/95%20-%20Sort%20List.md)
|  | [96 - Segregate even and odd nodes in a Linked List](https://leetcode.com/problems/linked-list-cycle/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/96%20-%20Segregate%20even%20and%20odd%20nodes%20in%20a%20Linked%20List.md)
|  | [97 - Rearrange a given linked list in-place](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/97%20-%20Rearrange%20a%20given%20linked%20list%20in-place.md)
|  | [98 - Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/98%20-%20Merge%20k%20Sorted%20Lists.md)
|  | [99 - Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/99%20-%20Reverse%20Nodes%20in%20k-Group.md)
|  | [100 - Subtraction in Linked List](https://www.geeksforgeeks.org/problems/subtraction-in-linked-list/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/100%20-%20Subtraction%20in%20Linked%20List.md)
|  | [101 - Flattening a Linked List](https://www.geeksforgeeks.org/problems/flattening-a-linked-list/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%208/Linked%20List/101%20-%20Flattening%20a%20Linked%20List.md)
| | | |
| **Day 9** | [102 - Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/102%20-%20Implement%20Queue%20using%20Stacks.md) | 
|  | [103 - Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/103%20-%20Backspace%20String%20Compare.md)
|  | [104 - Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/104%20-%20Implement%20Stack%20using%20Queues.md)
|  | [105 - Implement Stack and Queue using Deque](https://www.geeksforgeeks.org/implement-stack-queue-using-deque/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/105%20-%20Implement%20Stack%20and%20Queue%20using%20Deque.md)
|  | [106 - Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/106%20-%20Next%20Greater%20Element%20I.md)
|  | [107 - Evaluation of Postfix Expression](https://www.geeksforgeeks.org/problems/evaluation-of-postfix-expression1735/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/107%20-%20Evaluation%20of%20Postfix%20Expression.md)
|  | [108 - Implement two stacks in an array](https://www.geeksforgeeks.org/problems/implement-two-stacks-in-an-array/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/108%20-%20Implement%20two%20stacks%20in%20an%20array.md)
|  | [109 - Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/109%20-%20Daily%20Temperatures.md)
|  | [110 - Minimum Cost Tree From Leaf Values](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/110%20-%20Minimum%20Cost%20Tree%20From%20Leaf%20Values.md)
|  | [111 - Online Stock Span](https://leetcode.com/problems/online-stock-span/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/105%20-%20Implement%20Stack%20and%20Queue%20using%20Deque.md)
|  | [112 - Rotten Oranges](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/112%20-%20Rotten%20Oranges.md) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/112%20-%20Rotten%20Oranges.md)
|  | [113 - Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/113%20-%20Sum%20of%20Subarray%20Minimums.md)
|  | [114 - Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%209/Stacks%20and%20Queues/114%20-%20Evaluate%20Reverse%20Polish%20Notation.md)
| | | |
| **Day 10** | [115 - Circular tour](https://www.geeksforgeeks.org/problems/circular-tour-1587115620/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/115%20-%20Circular%20tour.md) | 
|  | [116 - Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/116%20-%20Remove%20All%20Adjacent%20Duplicates%20in%20String%20II.md)
|  | [117 - Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/117%20-%20Flatten%20Nested%20List%20Iterator.md)
|  | [118 - Maximum of minimum for every window size](https://www.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size3453/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/116%20-%20Remove%20All%20Adjacent%20Duplicates%20in%20String%20II.md)
|  | [119 - LRU Cache](https://leetcode.com/problems/lru-cache/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/119%20-%20LRU%20Cache.md)
|  | [120 - The Celebrity Problem](https://www.geeksforgeeks.org/problems/the-celebrity-problem/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/116%20-%20Remove%20All%20Adjacent%20Duplicates%20in%20String%20II.md)
|  | [121 - Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/119%20-%20LRU%20Cache.md)
|  | [122 - Maximum Number of Visible Points](https://leetcode.com/problems/maximum-number-of-visible-points/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Two%20Pointers%20and%20Sliding%20Window/122%20-%20Maximum%20Number%20of%20Visible%20Points.md)
| | | |
| **Day 11** | [123 - Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/123%20-%20Diameter%20of%20Binary%20Tree.md) | 
|  | [124 - Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/124%20-%20Invert%20Binary%20Tree.md)
|  | [125 - Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/125%20-%20Subtree%20of%20Another%20Tree.md)
|  | [126 - Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2010/Stacks%20and%20Queues/116%20-%20Remove%20All%20Adjacent%20Duplicates%20in%20String%20II.md)
|  | [127 - Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/127%20-%20Symmetric%20Tree.md)
|  | [128 - Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/128%20-%20Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree.md)
|  | [129 - Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/129%20-%20Merge%20Two%20Binary%20Trees.md)
| | | |
| **Day 12** | [130 - Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/130%20-%20Maximum%20Depth%20of%20Binary%20Tree.md) | 
|  | [131 - Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/131%20-%20Binary%20Tree%20Paths.md)
|  | [132 - Same Tree](https://leetcode.com/problems/same-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/132%20-%20Same%20Tree.md)
|  | [133 -  Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/133%20-%20%20Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.md)
|  | [134 - Path Sum](https://leetcode.com/problems/path-sum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/134%20-%20Path%20Sum.md)
|  | [135 - Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/%23%20135%20-%20Minimum%20Absolute%20Difference%20in%20BST.md)
|  | [136 - Sum of Left Leaves](https://leetcode.com/problems/merge-two-binary-trees/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2011/Tree/129%20-%20Merge%20Two%20Binary%20Trees.md)
| | | |
| **Day 13** | [137 - Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2013/Tree/137%20-%20Balanced%20Binary%20Tree.md) | 
|  | [138 - Predecessor and Successor](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2012/Tree/131%20-%20Binary%20Tree%20Paths.md)
|  | [139 - Binary Tree Inorder Traversal](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2013/Tree/139%20-%20Binary%20Tree%20Inorder%20Traversal.md)
| | | |
| **Day 14** | [140 - Check whether BST contains Dead End](https://www.geeksforgeeks.org/problems/check-whether-bst-contains-dead-end/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/140%20-%20Check%20whether%20BST%20contains%20Dead%20End.md) | 
|  | [141 - Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/141%20-%20Binary%20Search%20Tree%20Iterator.md)
|  | [142 - Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/142%20-%20Unique%20Binary%20Search%20Trees%20II.md)
|  | [143 - All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/143%20-%20All%20Nodes%20Distance%20K%20in%20Binary%20Tree.md)
|  | [144 - Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/144%20-%20Validate%20Binary%20Search%20Tree.md)
|  | [145 - Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/145%20-%20Binary%20Tree%20Right%20Side%20View.md)
|  | [146 - Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/146%20-%20Binary%20Tree%20Level%20Order%20Traversal.md)
|  | [147 - Path Sum III](https://leetcode.com/problems/path-sum-iii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/147%20-%20Path%20Sum%20III.md)
|  | [148 - Construct Binary Tree from Preorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/148%20-%20Construct%20Binary%20Tree%20from%20Preorder%20and%20Postorder%20Traversal.md)
|  | [149 - Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/149%20-%20Unique%20Binary%20Search%20Trees.md)
|  | [150 - Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2014/Tree/150%20-%20Recover%20Binary%20Search%20Tree.md)
| | | |
| **Day 15** | [151 - Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/151%20-%20Populating%20Next%20Right%20Pointers%20in%20Each%20Node.md) | 
|  | [152 - Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/152%20-%20Flatten%20Binary%20Tree%20to%20Linked%20List.md)
|  | [153 - Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/153%20-%20Maximum%20Width%20of%20Binary%20Tree.md)
|  | [154 - Min distance between two given nodes of a Binary Tree](https://www.geeksforgeeks.org/problems/min-distance-between-two-given-nodes-of-a-binary-tree/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/154%20-%20Min%20distance%20between%20two%20given%20nodes%20of%20a%20Binary%20Tree.md)
|  | [155 - Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/155%20-%20Kth%20Smallest%20Element%20in%20a%20BST.md)
|  | [156 - Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/156%20-%20Binary%20Tree%20Zigzag%20Level%20Order%20Traversal.md)
|  | [157 - Count BST nodes that lie in a given range](https://www.geeksforgeeks.org/problems/count-bst-nodes-that-lie-in-a-given-range/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/157%20-%20Count%20BST%20nodes%20that%20lie%20in%20a%20given%20range.md)
|  | [158 - Preorder to BST](https://www.geeksforgeeks.org/problems/preorder-to-postorder4423/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/158%20-%20Preorder%20to%20BST.md)
|  | [159 - Binary Tree to DLL](https://www.geeksforgeeks.org/problems/binary-tree-to-dll/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/159%20-%20Binary%20Tree%20to%20DLL.md)
|  | [160 - Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2015/160%20-%20Binary%20Tree%20Maximum%20Path%20Sum.md)
| | | |
| **Day 16** | [161 - Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/161%20-%20Sum%20of%20Distances%20in%20Tree.md) | 
|  | [162 - Binary Tree Cameras](https://leetcode.com/problems/binary-tree-cameras/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/162%20-%20Binary%20Tree%20Cameras.md)
|  | [163 - Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/163%20-%20Vertical%20Order%20Traversal%20of%20a%20Binary%20Tree.md)
|  | [164 - Print all k-sum paths in a binary tree](https://www.geeksforgeeks.org/print-k-sum-paths-binary-tree/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/164%20-%20Print%20all%20k-sum%20paths%20in%20a%20binary%20tree.md)
|  | [165 - Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/165%20-%20Serialize%20and%20Deserialize%20Binary%20Tree.md)
|  | [166 - Median of BST](https://www.geeksforgeeks.org/problems/median-of-bst/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/166%20-%20Median%20of%20BST.md)
|  | [167 - Largest BST](https://www.geeksforgeeks.org/problems/largest-bst/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/167%20-%20Largest%20BST.md)
|  | [168 - Construct Tree from Preorder Traversal](https://www.geeksforgeeks.org/problems/construct-tree-from-preorder-traversal/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2016/Tree/168%20-%20Construct%20Tree%20from%20Preorder%20Traversal.md)
| | | |
| **Day 17** | [169 - BFS of graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/169%20-%20BFS%20of%20graph.md) | 
|  | [170 - DFS of Graph](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/170%20-%20DFS%20of%20Graph.md)
|  | [171 - Number of Islands](https://leetcode.com/problems/number-of-islands/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/171%20-%20Number%20of%20Islands.md)
|  | [172 - Flood Fill](https://leetcode.com/problems/flood-fill/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/172%20-%20Flood%20Fill.md)
|  | [173 - Rat in a Maze Problem - I](https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/173%20-%20Rat%20in%20a%20Maze%20Problem%20-%20I.md)
|  | [174 - Undirected Graph Cycle](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/174%20-%20Undirected%20Graph%20Cycle.md)
|  | [175 - Directed Graph Cycle](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/175%20-%20Directed%20Graph%20Cycle.md)
|  | [176 - Steps by Knight](https://www.geeksforgeeks.org/problems/steps-by-knight5927/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/176%20-%20Steps%20by%20Knight.md)
|  | [177 - Decode String](https://leetcode.com/problems/decode-string/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/177%20-%20Decode%20String.md)
|  | [178 - Shortest Bridge](https://leetcode.com/problems/shortest-bridge/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/178%20-%20Shortest%20Bridge.md)
|  | [179 - Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/179%20-%20Number%20of%20Operations%20to%20Make%20Network%20Connected.md)
|  | [180 - Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/180%20-%20Find%20Eventual%20Safe%20States.md)
|  | [181 - Strongly Connected Components (Kosaraju's Algo)](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/181%20-%20Strongly%20Connected%20Components%20(Kosaraju's%20Algo).md)
|  | [182 - Time Needed to Inform All Employees](https://leetcode.com/problems/time-needed-to-inform-all-employees/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/182%20-%20Time%20Needed%20to%20Inform%20All%20Employees.md)
|  | [183 - Introduction to Graph Coloring](https://www.geeksforgeeks.org/graph-coloring-applications/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/183%20-%20Introduction%20to%20Graph%20Coloring.md)
|  | [184 - Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/184%20-%20Most%20Stones%20Removed%20with%20Same%20Row%20or%20Column.md)
|  | [185 - As Far from Land as Possible](https://leetcode.com/problems/as-far-from-land-as-possible/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/185%20-%20As%20Far%20from%20Land%20as%20Possible.md)
|  | [187 - Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/187%20-%20Find%20the%20City%20With%20the%20Smallest%20Number%20of%20Neighbors%20at%20a%20Threshold%20Distance.md)
|  | [186 - Prerequisite Tasks](https://www.geeksforgeeks.org/problems/prerequisite-tasks/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/186%20-%20Prerequisite%20Tasks.md)
|  | [188 - Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/188%20-%20Minimum%20Spanning%20Tree.md)
|  | [189 - Floyd Warshall](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/189%20-%20Floyd%20Warshall.md)
|  | [190 - Evaluate Division](https://leetcode.com/problems/evaluate-division/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/190%20-%20Evaluate%20Division.md)
| | | |
| **Day 18** | [191 - Snakes and Ladders](https://leetcode.com/problems/snakes-and-ladders/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/191%20-%20Snakes%20and%20Ladders.md) | 
|  | [192 - Topological sort](https://www.geeksforgeeks.org/problems/topological-sort/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/192%20-%20Topological%20sort.md)
|  | [193 - Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2017/Graph/171%20-%20Number%20of%20Islands.md)
|  | [194 - Detect a negative cycle in a Graph - Bellman Ford](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/194%20-%20Detect%20a%20negative%20cycle%20in%20a%20Graph%20%7C%20(Bellman%20Ford).md)
|  | [195 - Bipartite Graph](https://www.geeksforgeeks.org/problems/bipartite-graph/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/195%20-%20Bipartite%20Graph.md)
|  | [196 - Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/196%20-%20Longest%20Increasing%20Path%20in%20a%20Matrix.md)
|  | [197. Making A Large Island](https://leetcode.com/problems/making-a-large-island/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/197%20-%20Making%20A%20Large%20Island.md)
|  | [198 - Remove Boxes](https://leetcode.com/problems/remove-boxes/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/198%20-%20Remove%20Boxes.md)
|  | [199 - Alien Dictionary](https://www.geeksforgeeks.org/problems/alien-dictionary/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/199%20-%20Alien%20Dictionary.md)
|  | [200 - Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/200%20-%20Critical%20Connections%20in%20a%20Network.md)
|  | [201 - Water Jug problem using BFS](https://www.geeksforgeeks.org/water-jug-problem-using-bfs/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/201%20-%20Water%20Jug%20problem%20using%20BFS.md)
|  | [202 - Travelling Salesman Problem using Dynamic Programming](https://www.geeksforgeeks.org/travelling-salesman-problem-using-dynamic-programming/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/202%20-%20Travelling%20Salesman%20Problem%20using%20Dynamic%20Programming.md)
|  | [203 - Total number of Spanning Trees in a Graph](https://www.geeksforgeeks.org/total-number-spanning-trees-graph/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/203%20-%20Total%20number%20of%20Spanning%20Trees%20in%20a%20Graph.md)
|  | [204 - Word Ladder](https://leetcode.com/problems/word-ladder/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/204%20-%20Word%20Ladder.md)
|  | [205 - Minimize Cash Flow among a given set of friends who have borrowed money from each other](https://www.geeksforgeeks.org/minimize-cash-flow-among-given-set-friends-borrowed-money/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/205%20-%20Minimize%20Cash%20Flow%20among%20a%20given%20set%20of%20friends%20who%20have%20borrowed%20money%20from%20each%20other.md)
|  | [206 - Redundant Connection](https://leetcode.com/problems/redundant-connection/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/206%20-%20Redundant%20Connection.md)
|  | [207 - Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/Trie/207%20-%20Design%20Add%20and%20Search%20Words%20Data%20Structure.md)
|  | [208 - Word Break (Trie)](https://www.geeksforgeeks.org/problems/word-break-trie--141631/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/Trie/208%20-%20Word%20Break%20(Trie).md)
|  | [209 - Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/Trie/209%20-%20Implement%20Trie%20(Prefix%20Tree).md)
|  | [210 - Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/Trie/210%20-%20Palindrome%20Pairs.md)
|  | [211 - Phone directory](https://www.geeksforgeeks.org/problems/phone-directory4628/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2018/Trie/211%20-%20Phone%20directory.md)
| **Day 19** | [212 - Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/212%20-%20Top%20K%20Frequent%20Elements.md) | 
|  | [213 - Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/213%20-%20Kth%20Largest%20Element%20in%20an%20Array.md)
|  | [214 - Ugly Number II](https://leetcode.com/problems/ugly-number-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/214%20-%20Ugly%20Number%20II.md)
|  | [215 - Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/215%20-%20Furthest%20Building%20You%20Can%20Reach.md)
|  | [216 - Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/216%20-%20Kth%20Smallest%20Element%20in%20a%20Sorted%20Matrix.md)
|  | [217 - Reorganize String](https://leetcode.com/problems/reorganize-string/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/217%20-%20Reorganize%20String.md)
|  | [218 - Find the Most Competitive Subsequence](https://leetcode.com/problems/find-the-most-competitive-subsequence/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/218%20-%20Find%20the%20Most%20Competitive%20Subsequence.md)
|  | [219 - Largest subarray with 0 sum](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/219%20-%20Largest%20subarray%20with%200%20sum.md)
|  | [220 - K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/220%20-%20K%20Closest%20Points%20to%20Origin.md)
|  | [221 - Minimum Number of Refueling Stops](https://leetcode.com/problems/minimum-number-of-refueling-stops/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/221%20-%20Minimum%20Number%20of%20Refueling%20Stops.md)
|  | [222 - Minimum Cost to Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/222%20-%20Minimum%20Cost%20to%20Hire%20K%20Workers.md)
|  | [223 - Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/223%20-%20Swim%20in%20Rising%20Water.md)
|  | [224 - Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2019/Heap(Priority%20Queue)/224%20-%20Sliding%20Window%20Maximum.md)
| | | |
| **Day 20** | [225 - Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/225%20-%20Climbing%20Stairs.md) | 
|  | [226 - Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/226%20-%20Maximum%20Product%20Subarray.md)
|  | [227 - Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/227%20-%20Ones%20and%20Zeroes.md)
|  | [228 - Counting Bits](https://leetcode.com/problems/counting-bits/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/228%20-%20Counting%20Bits.md)
|  | [229 - Knight Dialer](https://leetcode.com/problems/knight-dialer/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/229%20-%20Knight%20Dialer.md)
|  | [230 - Maximize The Cut Segments](https://www.geeksforgeeks.org/problems/cutted-segments1642/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/230%20-%20Maximize%20The%20Cut%20Segments.md)
|  | [231 - Unique Paths](https://leetcode.com/problems/unique-paths/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/231%20-%20Unique%20Paths.md)
|  | [232 - Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2020/Dynamic%20Programming/232%20-%20Minimum%20Path%20Sum.md)
| | | | 
| **Day 23** | [246 - Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/246%20-%20Best%20Time%20to%20Buy%20and%20Sell%20Stock%20IV.md) | 
|  | [247 - Minimum Insertion Steps to Make a String Palindrome](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/247%20-%20Minimum%20Insertion%20Steps%20to%20Make%20a%20String%20Palindrome.md)
|  | [248 - Largest area rectangular sub-matrix with equal number of 1’s and 0’s](https://www.geeksforgeeks.org/largest-area-rectangular-sub-matrix-equal-number-1s-0s/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/248%20-%20Largest%20area%20rectangular%20sub-matrix%20with%20equal%20number%20of%201%E2%80%99s%20and%200%E2%80%99s.md)
|  | [249 - Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/249%20-%20Trapping%20Rain%20Water.md)
|  | [250 - Minimum Cost to Merge Stones](https://leetcode.com/problems/minimum-cost-to-merge-stones/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/250%20-%20Minimum%20Cost%20to%20Merge%20Stones.md) 
|  | [251 - Count Different Palindromic Subsequences](https://leetcode.com/problems/count-different-palindromic-subsequences/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/251%20-%20Count%20Different%20Palindromic%20Subsequences.md)
|  | [252 - Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2023/DP/252%20-%20Maximal%20Rectangle.md)
| | | | 
| **Day 24** | [253 - Burst Balloons](https://leetcode.com/problems/burst-balloons/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/DP/253%20-%20Burst%20Balloons.md) | 
|  | [254 - Super Egg Drop](https://leetcode.com/problems/super-egg-drop/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/DP/254%20-%20Super%20Egg%20Drop.md)
|  | [255 - Partition Equal Subset Sum](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/DP/255%20-%20Partition%20Equal%20Subset%20Sum.md)
|  | [256 - Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/Segment%20Tree/256%20-%20Range%20Sum%20Query%20-%20Immutable.md)
|  | [257 - Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/DP/255%20-%20Partition%20Equal%20Subset%20Sum.md)
|  | [258 - Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2024/Segment%20Tree/258%20-%20Count%20of%20Range%20Sum.md)
| | | | 
| **Day 25** | [259 - CHOCOLA - Chocolate](https://www.spoj.com/problems/CHOCOLA/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2025/Greedy/259%20-%20CHOCOLA%20-%20Chocolate.md) | 
|  | [260 - Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2025/Greedy/260%20-%20Non-overlapping%20Intervals.md)
|  | [261 - Minimum Time to Make Rope Colorful](https://leetcode.com/problems/minimum-time-to-make-rope-colorful/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2025/Greedy/261%20-%20Minimum%20Time%20to%20Make%20Rope%20Colorful.md)
|  | [262 - Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2025/Backtracking/262%20-%20Combination%20Sum%20II.md)
|  | [263 - Combinations](https://leetcode.com/problems/combinations/description/) | [Link](https://github.com/nandini-gangrade/DSA-Sheet/blob/main/DAY%2025/Backtracking/263%20-%20Combinations.md)

![image.png](https://assets.leetcode.com/users/images/dd42a649-e1d9-4b22-9eb8-add015c24468_1721761764.4795635.png)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet), [Leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solutions/5524617/best-solution-challenge-day-1-revisewitharsh) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀
`
