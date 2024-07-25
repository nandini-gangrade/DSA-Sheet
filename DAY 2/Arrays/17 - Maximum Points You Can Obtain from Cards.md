# [1423. Maximum Points You Can Obtain from Cards](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/description/)
[LeetCode Solution](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/solutions/5535805/step-by-step-explanation-challenge-day-2-revisewitharsh)

Given an integer array `cardPoints` where each element represents the points of a card in a row, and an integer `k`, return the maximum score you can obtain by taking exactly `k` cards. You can take cards from either the beginning or the end of the row.

### Examples

**Example 1:**

- **Input:** `cardPoints = [1,2,3,4,5,6,1]`, `k = 3`
- **Output:** `12`
- **Explanation:** Take the three cards on the right: `5 + 6 + 1 = 12`.

**Example 2:**

- **Input:** `cardPoints = [2,2,2]`, `k = 2`
- **Output:** `4`
- **Explanation:** Regardless of which two cards you take, your score will always be `4`.

**Example 3:**

- **Input:** `cardPoints = [9,7,7,9,7,7,9]`, `k = 7`
- **Output:** `55`
- **Explanation:** Take all the cards since `k` equals the length of `cardPoints`.

## Intuition

To maximize the score from taking `k` cards, you can take cards from either the left or the right end of the array. The naive approach would be to try every combination of taking cards from the start and the end, but this would be inefficient. Instead, we can use a sliding window approach to solve the problem in linear time.

## Approach

1. **Calculate Total Points:** First, calculate the total sum of the first `k` cards from the start of the array. This will be the initial maximum score.

2. **Sliding Window:** Iterate backwards, moving one card from the start to the end for each step:
   - Subtract the card being removed from the start of the window.
   - Add the card being added to the end of the window.
   - Update the maximum score accordingly.

3. **Maintain Maximum Score:** Keep track of the highest score achieved during this sliding window operation.

## Code

Here's the Python implementation:

```python
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        
        # Initial score using the first k cards
        current_score = sum(cardPoints[:k])
        max_score = current_score
        
        # Use a sliding window to calculate the score by taking cards from the end
        for i in range(1, k + 1):
            current_score += cardPoints[-i] - cardPoints[k - i]
            max_score = max(max_score, current_score)
        
        return max_score
```

## Complexity Analysis

- **Time Complexity:** \(O(k)\), where \(k\) is the number of cards to take. We use a sliding window over the `k` cards.
- **Space Complexity:** \(O(1)\), as we only use a few variables to store sums and scores.

This approach efficiently calculates the maximum possible score by leveraging the fact that we only need to consider `k` elements at a time, either from the start or the end of the `cardPoints` array.

---

![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀
`
