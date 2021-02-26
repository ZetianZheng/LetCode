# Problem
[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

## Problem Description
```
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

Input: nums = [1,2,3]
Output: [1,3,2]
```
## Tags


# Solution


# Code
```java
class Solution {
    public void nextPermutation(int[] nums) {
        if (nums == null) {
            return;
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
            return ;
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
        return;
        
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

