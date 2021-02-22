# Problem
[701. Trim a Binary Search Tree
](https://www.lintcode.com/problem/trim-a-binary-search-tree/)

## Problem Description
```
Given the root of a binary search tree and 2 numbers min and max, trim the tree such that all the numbers in the new tree are between min and max (inclusive). The resulting tree should still be a valid binary search tree. So, if we get this tree as input:

{8,3,10,1,6,#,14,#,#,4,7,13}
5
13
Output: {8, 6, 10, #, 7, #, 13}
Explanation:
The picture of tree is in the description.
```
## Tags
@BST @recursion
# Solution
- if root.val < minimum: left part subtree and root need be pruned, so return trimBST(right subtree).
- if root.val > maximum: right part subtree and root need be pruned, so return trimBST(left subtree).
- if minimum < root.val < maximum: keep root, do trim to its subtrees.

# Code
```java
public class Solution {
    /**
     * @param root: given BST
     * @param minimum: the lower limit
     * @param maximum: the upper limit
     * @return: the root of the new tree 
     */
    public TreeNode trimBST(TreeNode root, int minimum, int maximum) {
        // write your code here
        if (root == null) {
            return null;
        }
        
        if (root.val < minimum) {
            return trimBST(root.right, minimum, maximum);
        } else if (root.val > maximum) {
            return trimBST(root.left, minimum, maximum);
        } else {
            root.left = trimBST(root.left, minimum, maximum);
            root.right = trimBST(root.right, minimum, maximum);
        }
        
        return root;
    }
}
```
## Complexity Analysis
- Time Complexity: O(N)
- Space Complexity: O(N) (keep all nodes, and the tree is a one side tree)

