# Problem
[34. N-Queens II
](https://www.lintcode.com/problem/n-queens-ii/)

## Problem Description
```
Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.
```
## Tags
@DFS

# Solution
add an public variable: sum, record number of solutions, change recursion exit, sum++.
# Code
```java
public class Solution {
    /**
     * @param n: The number of queens.
     * @return: The total number of distinct solutions.
     */
    public static int sum;
    public int totalNQueens(int n) {
        // write your code here
        sum = 0;
        if (n <= 0) {
            return sum;
        }
        
        search(new ArrayList<Integer>(), n);
        
        return sum;
    }
    
    // recursion
    private void search(List<Integer> cols, int n) {
        if (cols.size() == n) {
            sum++;
            return; 
        }
        
        // enumerate current row
        for (int colIndex = 0; colIndex < n; colIndex++) {
            if (!isValid(cols, colIndex)) {
                continue;
            }
            
            cols.add(colIndex);
            search(cols, n);
            cols.remove(cols.size() - 1); // back tracking
        }
    }
    
    private boolean isValid(List<Integer> cols, int colCandidate) {
        int row = cols.size();
        
        for (int rowIndex = 0; rowIndex < row; rowIndex++) {
            if (cols.get(rowIndex) == colCandidate) {
                return false;
            }
            
            if (row + colCandidate == rowIndex + cols.get(rowIndex)) {
                return false;
            }
            
            if (row - colCandidate == rowIndex - cols.get(rowIndex)) {
                return false;
            }
        }
        
        return true;
    }
}
```
## Complexity Analysis
- Time Complexity: O(S * n ^ 2)
- Space Complexity: O()

