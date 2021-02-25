# Problem
[197. Permutation Index
](https://www.lintcode.com/problem/permutation-index/)

## Problem Description
```
Given a permutation which contains no repeated number, find its index in all the permutations of these numbers, which are ordered in lexicographical order. The index begins at 1.

Input:[1,2,4]
Output:1

Input:[3,2,1]
Output:6
```
## Tags
@permutation

# Solution
```
To get index of the permutation, we only need to know about how many numbers of possible permutations exists before that in lexicographical order.  

The method to count that is to find the number of possible numbers at position:i which smaller than A[i] 
(at right side of A[i]), multiply with number of permutations after i.

For example,  
[3,7,4,9,1]  
[3,7,4,1,X] first, 1 is smaller than 9, so we can put 1 at A[4] to get an permutation smaller than original one in lexicographical order.
[3,7,1,X,X] 1 is smaller than 4, count 1 times 2!.
[3,1or4,X,X,X] 1 and 4 are smaller than 7，count 2 times 3!
[1,X,X,X,X]  1 is smaller than 3, count 1 times 4!.

last, add all it together
1×1!+1×2!+2×3!+1×4!=39
```
# Code
```java
public class Solution {
    /**
     * @param A: An array of integers
     * @return: A long integer
     */
    public long permutationIndex(int[] A) {
        // write your code here
        if (A == null) {
            return 0;
        }
        
        long permutation = 1;
        long ret = 0;
        int s =0;
        
				// backward count number of how many permutations exist before A
        for (int i = A.length - 2; i >= 0; i--) { 
            // last bit can only have 1 permutation which is original one, since i begin from A.length - 2
            s = smallerCounts(A, i);
            ret += s * permutation;
            permutation *= A.length - i; // factorial 
        }
        
        return ret + 1; // Permutation Index
    }
    
    private int smallerCounts(int[] A, int start) {
        int ret = 0;
        for (int i = start + 1; i < A.length; i++) {
            if (A[i] < A[start]) {
                ret++;
            }
        }
        
        return ret;
    }
}
```
## Complexity Analysis
- Time Complexity: O(n^2)
- Space Complexity: O()

