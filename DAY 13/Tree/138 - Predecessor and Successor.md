# [Predecessor and Successor](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)




### Intuition
- **Predecessor**: The predecessor of a node in a BST is the largest node in its left subtree or the nearest ancestor for which the node lies in the right subtree.
- **Successor**: The successor of a node in a BST is the smallest node in its right subtree or the nearest ancestor for which the node lies in the left subtree.
- By maintaining the current node as a possible predecessor or successor while traversing the tree, we ensure that the values are updated to their closest ancestors or subtree nodes.

### Approach
1. **Base Case**: If the root is `NULL`, simply return as there are no nodes to process.
2. **Recursive Search**:
   - If the key is smaller than the root's key, update the successor to the current root and search in the left subtree.
   - If the key is greater than the root's key, update the predecessor to the current root and search in the right subtree.
   - If the key matches the root's key, check:
     - **Left Subtree**: For the predecessor, find the rightmost node.
     - **Right Subtree**: For the successor, find the leftmost node.

## Code
```cpp
/* BST Node
struct Node
{
	int key;
	struct Node *left;
	struct Node *right;
	
	Node(int x){
	    key = x;
	    left = NULL;
	    right = NULL;
	}
};
*/

// This function finds predecessor and successor of key in BST.
// It sets pre and suc as predecessor and successor respectively
class Solution
{
    public:
    void findPreSuc(Node* root, Node*& pre, Node*& suc, int key)
    {
        // Your code goes here
        if (root == NULL) return;
        
        // If the key is less than the root's key, search in the left subtree
        if (key < root->key) {
            suc = root; // Update successor
            findPreSuc(root->left, pre, suc, key);
        }
        // If the key is greater than the root's key, search in the right subtree
        else if (root->key < key) {
            pre = root; // Update predecessor
            findPreSuc(root->right, pre, suc, key);
        }
        // If the key is equal to the root's key
        else {
            // Check the left subtree for predecessor
            if (root->left != NULL) {
                Node* tmp = root->left;
                while (tmp->right) {
                    tmp = tmp->right;
                }
                pre = tmp;
            }
            // Check the right subtree for successor
            if (root->right != NULL) {
                Node* tmp = root->right;
                while (tmp->left) {
                    tmp = tmp->left;
                }
                suc = tmp;
            }
        }
    }
};
```

### Complexity
- **Time Complexity**: \(O(h)\), where \(h\) is the height of the BST. In the worst case, this is \(O(n)\) for an unbalanced tree, but \(O(\log n)\) for a balanced tree.
- **Space Complexity**: \(O(h)\) due to the recursive call stack, similar to the time complexity analysis.

This solution efficiently finds the predecessor and successor by leveraging the BST properties and ensuring minimal checks and updates during the traversal.
