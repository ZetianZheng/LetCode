# Problem
[192. Wildcard Matching
](https://www.lintcode.com/problem/wildcard-matching/)

## Problem Description
```
Implement wildcard pattern matching with support for '?' and '*'.

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).

Input:
"aa"
"*"
Output: true
```
## Tags
@DP @DP-matching

# Solution
1. DP(state, initialization, function, answer)
2. Use rolling array to optimize space complexity, because dp[i][x] depend on dp[i-1][x] plus other conditions


# Code

the most confused part of code is need to distinct difference from index of p or s and index of dp[][], need to consider about which index means the last char.

1. Standard dynamic programming
```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    public boolean isMatch(String s, String p) {
        // write your code here
        if (s == null || p == null) {
            return false;
        }

        int n = s.length(); 
        int m = p.length();

        // State
        // dp[i][j]: Is first i chars in source s can match first j chars in pattern p? true/false
        boolean[][] dp = new boolean[n + 1][m + 1];
        
        // Initialization, handle if someone is ""
        // 1. s = "", p = ""
        dp[0][0] = true; 
        // 2. s > 0, p = "" -> false. 
        // Do not need to set it manually, the array will set as false by default.
        // for (int i = 1; i <= n; i++) { 
        //     dp[i][0] = false;
        // }
        // 3. s = "", p is the string all of "*" -> true
        for (int j = 1; j <= m; j++) { 
            dp[0][j] = dp[0][j - 1] && p.charAt(j - 1) == '*';
        }

        // Function:
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
								// if the last char at p is '*':
								// 1. * matches '': dp[i][j] = dp[i][j - 1]
								// 2. * not matches '': dp[i][j] = dp[i - 1][j] 
								//    Do in next loop: ...= dp[i - 2][j]....
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else {
                    dp[i][j] = dp[i - 1][j - 1] && isMatchChar(s, p, i - 1, j - 1);
                }    
            }
        }

        // Answer: dp[n][m] is the last one 
        return dp[n][m];
    }

    private boolean isMatchChar(String s, String p, int i, int j) {
        if (s.charAt(i) == p.charAt(j) || p.charAt(j) == '?') {
            return true;
        }
        return false;
    }
}
```

2. Rolling array
```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    public boolean isMatch(String s, String p) {
        // write your code here
       if(s == null || p == null) {
           return false;
       }

        // state
        int n = s.length();
        int m = p.length();
        boolean[][] dp = new boolean[2][m+1]; // rolling array, keep 2 spaces (i mod 2, (i - 1) mod 2) 

        // initialization
        dp[0][0] = true;
        // if s = '' and all of p are '*'
        for (int i = 1; i <=m; i++) {
            // dp[0][i] depends on dp[0][i - 1] and p[i] = *;
            dp[0][i] = dp[0][i - 1] && p.charAt(i - 1) == '*';
        }

        // function
        for (int i = 1; i <= n; i++) {
            dp[i % 2][0] = false; // clean the table.
            for (int j = 1; j <= m; j++) {
                if (p.charAt(j - 1) == '*'){ // the last char at current p is *
                    dp[i % 2][j] = dp[i % 2][j - 1] || dp[(i - 1) % 2][j];
                } else {
                    dp[i % 2][j] = dp[(i - 1) % 2][j - 1] && isMatchChar(s, p, i - 1, j - 1);
                }
            }
        }

        return dp[n % 2][m];
    }

    private boolean isMatchChar(String s, String p, int i, int j) {
        if (s.charAt(i) == p.charAt(j) || p.charAt(j) == '?'){
            return true;
        }

        return false;
    }
}
```

## Complexity Analysis
for the standard DP:
- Time Complexity: O(n^2)
- Space Complexity: O(n^2)

for the rolling array, we reduce the space complexity to:
- Space Complexity: O(n)

