# [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

To convert a sorted array into a height-balanced binary search tree (BST), we can utilize the property that the middle element of the sorted array becomes the root of the BST. This approach ensures that the tree is balanced, as it divides the array into two halves, each forming a subtree.

Here's how you can implement this:

1. **Select the middle element** of the current subarray as the root.
2. Recursively do the same for the left half and the right half of the current subarray to construct the left and right subtrees.
3. Base case: If the subarray is empty, return `None`.

## Code

```python
# Definition for a binary tree node.
from typing import List, Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        def buildBST(left: int, right: int) -> Optional[TreeNode]:
            if left > right:
                return None

            # Middle element to make the tree balanced
            mid = (left + right) // 2
            node = TreeNode(nums[mid])

            # Recursively build the left and right subtrees
            node.left = buildBST(left, mid - 1)
            node.right = buildBST(mid + 1, right)

            return node

        return buildBST(0, len(nums) - 1)
```

### Explanation:

- **Recursive Function `buildBST`**:
  - The function `buildBST(left, right)` constructs a BST using the elements from index `left` to `right`.
  - The base case checks if `left > right`, which means the subarray is empty, and returns `None`.
  - We calculate `mid` as the middle index of the current subarray and create a `TreeNode` with this middle element.
  - We recursively build the left and right subtrees using the left and right halves of the current subarray, excluding the middle element.

- **Main Function `sortedArrayToBST`**:
  - It initializes the recursion with the entire range of the array, i.e., `0` to `len(nums) - 1`.

### Complexity Analysis:

- **Time Complexity**: \(O(n)\), where \(n\) is the number of elements in the array. Each element is processed once.
- **Space Complexity**: \(O(\log n)\) for the recursive stack, as the tree is balanced and the depth of recursion is \(\log n\).

This method effectively constructs a height-balanced BST from a sorted array, ensuring optimal depth and balanced subtrees.
