# Problem
[46. Permutations](https://leetcode.com/problems/permutations/)

## Problem Description
```
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```
## Tags


# Solution


# Code
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        if (nums == null) {
            return null;
        }
        
        List<List<Integer>> ret = new ArrayList<>();
        
        Arrays.sort(nums);
       
        // Do next permutation if have next.
        boolean flag = true;
        while (flag) {
            // copy from int[] to list<>
            List<Integer> current = new ArrayList<>();
            for (int n: nums) {
                current.add(n);           
            }
            ret.add(current);
            flag = nextPermutation(nums);
        }
        
        return ret;
    }
    
     public boolean nextPermutation(int[] nums) {
        if (nums == null) {
            return false;
        }
        
        int n = nums.length;
        int pivot = n - 2;
        
        // get pivot where break monotonically decreasing, nums: pivot < pivot + 1
        while (pivot >= 0 && nums[pivot] >= nums[pivot + 1]) { 
            pivot--;
        }
        
        // special situation: the list is monotonically decreasing.
        if (pivot < 0) { 
            reverse(nums, 0, n - 1);
            return false;
        }
        
        // find an element larger than pivot. because nums in range [pivot+1，n) is monotonically decreasing
        int lg = pivot + 1;
        while (lg < n && nums[lg] > nums[pivot]) {
            lg++;
        }
        lg = lg - 1;
        
        // Do swap then reverse
        swap(nums, pivot, lg);
        reverse(nums, pivot + 1, n - 1);
        return true;
        
    }
     
    private void swap(int[] s, int start, int end) {
        int temp = s[start];
        s[start] = s[end];
        s[end] = temp;
    }
    
    private void reverse(int[] s, int start, int end) {
         while(start < end) {
            swap(s, start, end);
            start++;
            end--;
        }
    }
}
```
## Complexity Analysis
- Time Complexity: O()
- Space Complexity: O()

