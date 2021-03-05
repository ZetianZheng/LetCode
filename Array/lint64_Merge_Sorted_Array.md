# Problem
[64. Merge Sorted Array
](https://www.lintcode.com/problem/64/my-submissions)

## Problem Description
```
Given two sorted integer arrays A and B, merge B into A as one sorted array.

You may assume that A has enough space (size that is greater or equal to m + n) to hold additional elements from B. The number of elements initialized in A and B are m and n respectively.
```
## Tags
@Array @Combine

# Solution
- combine B to A, think about backward(from A[m+n]) compare and fill—in, then we don't need to move m each time when fill-in(In total need to move n * m times).
# Code
```java
public class Solution {
    /*
     * @param A: sorted integer array A which has m elements, but size of A is m+n
     * @param m: An integer
     * @param B: sorted integer array B which has n elements
     * @param n: An integer
     * @return: nothing
     */
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        // write your code here
        if (B == null || B.length == 0) {
            return;
        }

        int i = m - 1, j = n - 1, index = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (B[j] > A[i]) {
                A[index--] = B[j--];
            }
            else {
                A[index--] = A[i--];
            }
        }

        while (i >= 0) {
            A[index--] = A[i--];
        }
        while (j >= 0) {
            A[index--] = B[j--];
        }

        return;
    }
}
```
## Complexity Analysis
- Time Complexity: O()
- Space Complexity: O()

## follow up  
[merge two sorted arrays](./lint6_Merge_Two_Sorted_Arrays.md)
