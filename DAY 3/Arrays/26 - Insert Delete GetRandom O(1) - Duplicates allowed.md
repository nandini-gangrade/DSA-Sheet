# [381. Insert Delete GetRandom O(1) - Duplicates allowed](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/description/)
[LeetCode Solution](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/solutions/5540249/best-solution-challenge-day-3-revisewitharsh)

You need to implement a data structure, `RandomizedCollection`, which allows for:
1. Inserting an item into the collection.
2. Removing an item from the collection.
3. Getting a random element from the collection with each element's probability proportional to its frequency in the collection.

## Intuition

To achieve average \(O(1)\) time complexity for all operations, you need:
1. **Efficient Insertion and Removal:** Use a data structure that supports efficient updates and removals while maintaining the ability to retrieve elements by their indices.
2. **Random Access:** Use an array or list to store elements to support efficient random access.
3. **Tracking Indices:** Use a hash map to keep track of all indices where each value is stored to allow quick lookups and updates.

## Approach

1. **Data Structures:**
   - **List (`nums`):** To store the elements. This supports efficient retrieval and update operations.
   - **HashMap (`idxMap`):** Maps each value to a set of indices in `nums` where the value occurs. This allows efficient lookups and updates.
   - **Random Object:** To generate random indices for retrieving random elements.

2. **Insert Operation:**
   - Add the element to `nums`.
   - Update `idxMap` to include the new index for the element.
   - Return `true` if the element was not previously present, otherwise `false`.

3. **Remove Operation:**
   - Check if the element is present in `idxMap`.
   - Remove the element from `nums` and update `idxMap` accordingly.
   - Handle the case where the element to remove is at the end of the list separately.
   - If the element has more occurrences, update the index set.

4. **Get Random Operation:**
   - Use a `Random` object to select a random index from `nums`.

## Code

```python []
import random
from collections import defaultdict

class RandomizedCollection:

    def __init__(self):
        self.nums = []
        self.idx_map = defaultdict(set)
        self.random = random.Random()
    
    def insert(self, val: int) -> bool:
        is_new = len(self.idx_map[val]) == 0
        self.idx_map[val].add(len(self.nums))
        self.nums.append(val)
        return is_new
    
    def remove(self, val: int) -> bool:
        if not self.idx_map[val]:
            return False
        
        # Remove index to be deleted
        idx_to_remove = self.idx_map[val].pop()
        last_val = self.nums[-1]
        
        if idx_to_remove != len(self.nums) - 1:
            # Move the last element to the place of the element to be removed
            self.nums[idx_to_remove] = last_val
            self.idx_map[last_val].add(idx_to_remove)
            self.idx_map[last_val].remove(len(self.nums) - 1)
        
        self.nums.pop()
        
        # Clean up if necessary
        if not self.idx_map[val]:
            del self.idx_map[val]
        
        return True
    
    def getRandom(self) -> int:
        return self.nums[self.random.randint(0, len(self.nums) - 1)]
```

## Complexity

- **Insertion:** \(O(1)\) average time complexity. Adding an element to the list and updating the hash map takes constant time.
- **Removal:** \(O(1)\) average time complexity. Removing an element from the list and updating the hash map involves a constant number of operations.
- **Get Random:** \(O(1)\) average time complexity. Retrieving a random element from the list takes constant time.

This implementation uses a list for storage and a hash map for indexing, allowing each operation to be performed in average \(O(1)\) time.

---
![upvotee.jpg](https://assets.leetcode.com/users/images/e9ab2638-b67e-4627-b3b2-9a9a22f0846e_1674113681.4102023.jpeg)

***Follow my progress and join the challenge on my*** **[GitHub](https://github.com/nandini-gangrade/DSA-Sheet) *and* [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7221580562367414272/)** 

`Let's tackle these coding challenges together! 🚀`
