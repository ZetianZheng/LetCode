# Problem
[344. Reverse String](https://leetcode.com/problems/reverse-string/)

## Problem Description
```
Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```
## Tags
@twoPointer
# Code
```java
class Solution {
    public void reverseString(char[] s) {
        int start = 0;
        int end = s.length - 1;
        while(start < end) {
            swap(s, start, end);
            start++;
            end--;
        }
    }
    
    private void swap(char[] s, int start, int end) {
        char temp = s[start];
        s[start] = s[end];
        s[end] = temp;
    }
}
```
## Complexity Analysis
- Time Complexity: O(n)
- Space Complexity: O(1)