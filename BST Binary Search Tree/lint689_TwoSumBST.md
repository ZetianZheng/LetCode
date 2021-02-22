# Problem
[689. Two Sum IV - Input is a BST
](https://www.lintcode.com/problem/two-sum-iv-input-is-a-bst/)
## Problem Description
```
Given a binary search tree and a number n, find two numbers in the tree that sums up to n.

notice: Without any extra space

{4,2,5,1,3}
3
Output: [1,2] (or [2,1])
Explanation:
binary search tree:
    4
   / \
  2   5
 / \
1   3
```
## Tags
@BST

# Solution


# Code
## method 1 (with extra space: hashset, time saving)
```java
public class Solution {
    /*
     * @param : the root of tree
     * @param : the target sum
     * @return: two numbers from tree which sum is n
     */
    public int[] twoSum(TreeNode root, int n) {
        // write your code here
        if (root == null) {
            return null;
        }
        Set<Integer> set = new LinkedHashSet<Integer>();
        int[] ret = new int[2];
        
        helper(root, n, set, ret);
        
        return ret;
    }
    
    public void helper(TreeNode root, int n, Set<Integer> set, int[] ret) {
        if (root == null || !Arrays.equals(ret, new int[2])) { // return the first found pairs
            return;
        }
        
        int num = n - root.val;
        if (set.contains(num)) {
            ret[0] = root.val;
            ret[1] = num;
            return ;
        }
        set.add(root.val);
        
        helper(root.left, n, set, ret);
        helper(root.right, n, set, ret);
    }
}
```
## Complexity Analysis
- Time Complexity: O(N), In the worst case, all nodes are on one side.
- Space Complexity: O(N)

## method 2 
> Do a little change to method 1 for handling quest: no extra space.  
> Inorder traversal all nodes in the tree,  
> If find value of a node equal to (n - root.val), return answer.  
```java
public class Solution {
    /*
     * @param : the root of tree
     * @param : the target sum
     * @return: two numbers from tree which sum is n
     */
    TreeNode root; // point to initial root.
    
    public int[] twoSum(TreeNode root, int n) {
        // write your code here
        if (root == null) {
            return null;
        }
        this.root = root;
        
        int[] ret = new int[2];
        inorder(root, n, ret);
        return ret;
    }
    
    public void inorder(TreeNode root, int n, int[] ret) {
        if (root == null || !Arrays.equals(ret, new int[2])) {
            return ;
        }
        
        inorder(root.left, n, ret);
        
        if (findNode(this.root, n - root.val, root)){
            // int ret = new int[2] // this is a big mistake! I create a new int[] named ret, but not the param ret!
            ret[0] = root.val;
            ret[1] = n - root.val;
            return;
        }
        
        inorder(root.right, n, ret);
    }
    
    public boolean findNode(TreeNode root, int target, TreeNode curroot) {
        if (root == null) return false;
        
        if (root.val == target && root != curroot) { // avoid return self. (self add self equal to target.)
            return true;
        }
        
        if (root.val < target) { // pay attention on right or left, focus on target!
           return findNode(root.right, target, curroot);
        } else {
           return findNode(root.left, target, curroot);
        }
        
    }
}
```