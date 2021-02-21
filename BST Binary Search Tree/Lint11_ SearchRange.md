# Problem
[11. Search Range in Binary Search Tree](https://www.lintcode.com/problem/search-range-in-binary-search-tree/)
## Problem decription
```
Given a binary search tree and a range [k1, k2], return node values within a given range in ascending order.
Input：{5},6,10
Output：[]
        5
it will be serialized {5}
No number between 6 and 10
```
# Solution
## Binary Search Tree feature:  

Binary Search Tree is a node-based binary tree data structure which has the following properties:

> The left subtree of a node contains only nodes with keys lesser than the node’s key.  
> The right subtree of a node contains only nodes with keys greater than the node’s key.  
> The left and right subtree each must also be a binary search tree.


Using recursion: 
- root.val < k1: the answer will be in right subtree
- root.val > k2: the answer will be in left subtree
- k1 <= root.val <= k2: in the range, record root.val, continue search
- root == null: stop the recursion, exit.

# Code
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
```
``` java
// solution not use the recursion helper: 17.5%
public class Solution {
    /**
     * @param root: param root: The root of the binary search tree
     * @param k1: An integer
     * @param k2: An integer
     * @return: return: Return all keys that k1<=key<=k2 in ascending order
     */
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        if (root == null) {
            return ret;
        }
        
        if (root.val < k1) {
            ret.addAll(searchRange(root.right, k1, k2));
            return ret;
        } 
        else if (root.val > k2) {
            ret.addAll(searchRange(root.left, k1, k2));
            return ret;
        }
        else {
            ret.add(root.val);
            ret.addAll(searchRange(root.left, k1, k2));
            ret.addAll(searchRange(root.right, k1, k2));
            return ret;
        }
    }
}
```
```java
// solution use the recursion helper: 13.6%
public class Solution {
    /**
     * @param root: param root: The root of the binary search tree
     * @param k1: An integer
     * @param k2: An integer
     * @return: return: Return all keys that k1<=key<=k2 in ascending order
     */
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        Helper(root, k1, k2, ret);
        return ret;
    }
    
    public void Helper(TreeNode root, int k1, int k2, List<Integer> ret) {
        if (root == null) {
            return;
        }
        
        if (root.val < k1) {
            Helper(root.right, k1, k2, ret);
        }
        else if (root.val > k2) {
            Helper(root.left, k1, k2, ret);
        }
        else {
            ret.add(root.val);
            Helper(root.left, k1, k2, ret);
            Helper(root.right, k1, k2, ret);
        }
    }
}
```