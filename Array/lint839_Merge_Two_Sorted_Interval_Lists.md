# Problem
[839. Merge Two Sorted Interval Lists
](https://www.lintcode.com/problem/839/)

## Problem Description
```
Merge two sorted (ascending) lists of interval and return it as a new sorted list. The new sorted list should be made by splicing together the intervals of the two lists and sorted in ascending order.

Input: list1 = [(1,2),(3,4)] and list2 = [(2,3),(5,6)]
Output: [(1,4),(5,6)]
Explanation:
(1,2),(2,3),(3,4) --> (1,4)
(5,6) --> (5,6)
```
## Tags
@Array @Combine

# Solution
same as merge two sorted array, the only difference is how to combine two Intervals:  
- if two intervals are separately, or results have no  interval yet, add new interval to the end  
- if two intervals are overlap, compare the end of two intervals, keep the largest one as the new end. (new.start must be included).

# Code
```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

public class Solution {
    /**
     * @param list1: one of the given list
     * @param list2: another list
     * @return: the new sorted list of interval
     */
    public List<Interval> mergeTwoInterval(List<Interval> list1, List<Interval> list2) {
        // write your code here
        if (list1 == null) {
            return list2;
        }
        if (list2 == null) {
            return list1;
        }

        List<Interval> ret = new ArrayList<>();

        int i = 0, j = 0;

        while (i < list1.size() && j < list2.size()) {
            if (list1.get(i).start < list2.get(j).start) {
                addInterval(ret, list1.get(i));
                i++;
            } else {
                addInterval(ret, list2.get(j));
                j++;
            }
        }

        while (i < list1.size()) {
            addInterval(ret, list1.get(i));
            i++;
        }
        while (j < list2.size()) {
            addInterval(ret, list2.get(j));
            j++;
        }

        return ret;
    }

    private void addInterval(List<Interval> results, Interval newIntvl) {
        if (results == null || results.size() == 0) {
            results.add(newIntvl);
            return;
        }
        Interval last = results.get(results.size() - 1);
        if (last.end < newIntvl.start){
            results.add(newIntvl);
            return;
        }

        last.end = Math.max(last.end, newIntvl.end);
        results.set(results.size() - 1, last);
        return;
    }
}
```
## Complexity Analysis
- Time Complexity: O()
- Space Complexity: O()

