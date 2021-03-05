# Problem
[6. Merge Two Sorted Arrays
](https://www.lintcode.com/problem/6/my-submissions)

## Problem Description
```
Merge two given sorted ascending integer array A and B into a new sorted integer array.
```
## Tags
@Array @Combine

# Solution
pointers to two arrays, compare them.   
after one array iterated to the end, add other array to the answer in order.
# Code
```java
public class Solution {
    /**
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        // write your code here
        if (A == null || A.length == 0) {
            return B;
        }
        if (B == null || B.length == 0) {
            return A;
        }

        int[] C = new int[A.length + B.length];
        int i = 0, j = 0, n = 0;

        // compare A[i] and B[j]
        while (i < A.length && j < B.length) {
            if (A[i] < B[j]) {
                C[n++] = A[i++];
            }
            else {
                C[n++] = B[j++];
            }
        }

        // one array has been iterated to the end.
        while (i < A.length) {
            C[n++] = A[i++];
        }

        while (j < B.length) {
            C[n++] = B[j++];
        }

        return C;
    }
}
```
## notice
- C[n++]: do operation, get C[n], then n + 1,
## Complexity Analysis
- Time Complexity: O(n)
- Space Complexity: O(n)

