# Problem
[17. Subsets
](https://www.lintcode.com/problem/subsets/description)

## Problem Description
```
Given a set of distinct integers, return all possible subsets.

Input: [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
## Tags
@DFS @Combination

# Solution
Using DFS to search all possible subsets.
## method 1
> For this question, A tree can be created.   
> For each level in this tree, we decide the nums[index] should be keep or not.   
> All leaf nodes are results which are possible subsets.

<div style="text-align: center;">
    <img src = 'https://raw.githubusercontent.com/ZetianZheng/PicGo_imgs/master/Algorithm/subset_1.png' width = "400" height = "200" alt="subset_1"/>
</div>

## method 2
> For this question, A tree can be created.   
> For each level in this tree, find all subsets which are head of their parent nodes.   
> All nodes are results which are possible subsets.

<div style="text-align: center;">
    <img src = 'https://raw.githubusercontent.com/ZetianZheng/PicGo_imgs/master/Algorithm/subset_2.png' width = "300" height = "200" alt="subset_2"/>
</div>

***
## Not Recursion Method:
## method 3: binary transform
```
[1, 2, 3]:
0 -> 000 -> {}
1 -> 001 -> {3}
2 -> 010 -> {2}
3 -> 011 -> {2,3}
4 -> 100 -> {1}
5 -> 101 -> {1,3}
6 -> 110 -> {1,2}
7 -> 111 -> {1,2,3}
```
# Code
## method 1: leaf nodes are results
```java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    public List<List<Integer>> subsets(int[] nums) {
        // write your code here
        List<List<Integer>> ret = new ArrayList<>();
        
        if (nums == null) {
            return ret;
        }
        
        Arrays.sort(nums);
        
        dfs(nums, 0, new ArrayList<Integer>(), ret);
        
        return ret;
    }
    
    public void dfs(int[] nums, 
                    int index, 
                    List<Integer> subset, 
                    List<List<Integer>> results) {
        if (nums.length == 0 || index == nums.length) { // to the leaf, return results which add deep copy of current subset
            results.add(new ArrayList<Integer>(subset));
            return ;
        }
        
        // recusion: left subtree, take the nums[index]
        subset.add(nums[index]); // list.add() return boolean, so cannot be used directly as the param.
        dfs(nums, index + 1, subset, results);
        
        // recusion: right subtree, don't take the nums[index]
        subset.remove(subset.size() - 1); 
        dfs(nums, index + 1, subset, results);
    }
}
```
### notice
- deep copy of subset.
## Complexity Analysis
- Time Complexity: O()
- Space Complexity: O()

## method 2: all nodes are in results, backtracking.
``` java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    public List<List<Integer>> subsets(int[] nums) {
        // write your code here
        List<List<Integer>> ret = new ArrayList<>();
        
        if (nums == null) {
            return ret;
        }
    
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<>(), ret);
        
        return ret;
    }
    
    public void dfs(int[] nums, int index, List<Integer> subset, List<List<Integer>> results) {
       results.add(new ArrayList<Integer>(subset));
       
       for (int i = index; i < nums.length; i++) {
           subset.add(nums[i]); // current subset
           dfs(nums, i + 1, subset, results); // recursion to find subsets which has head of current subset.
           subset.remove(subset.size() - 1); // backtracking
       }
       
       return;
    }
    
}
```
## method 3: binary transform
``` java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ret = new ArrayList<>();
        if (nums == null) {
            return ret;
        }
        Arrays.sort(nums);
        int n = nums.length;
        for (int i = 0; i < (1<<n); i++) { // how many possible subsets have, and transfer to binary form. ex: length 3: 000 ~ 111
            List<Integer> subset = new ArrayList<>();
            // transfer binary form to answer form
            for (int j = 0; j < n; j++) { // which bit is 1:
                // if (i & (1<<j) != 0) { error! java didn't take i & (1<<j) as a binary operation
                if ((i & (1<<j)) != 0) { // can not write like: i & (1<<j) == 1 (10 & 110 = 010)
                    subset.add(nums[j]);
                }
            }
            ret.add(subset);
        }
        
        return ret;
    }
}
```