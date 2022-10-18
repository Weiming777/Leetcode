# 1288.Remove Covered Intervals

Given an array `intervals` where `intervals[i] = [li, ri]` represent the interval `[li, ri)`, remove all intervals that are covered by another interval in the list.

The interval `[a, b)` is covered by the interval `[c, d)` if and only if `c <= a` and `b <= d`.

Return *the number of remaining intervals*.

 

**Example 1:**

```
Input: intervals = [[1,4],[3,6],[2,8]]
Output: 2
Explanation: Interval [3,6] is covered by [2,8], therefore it is removed.
```

**Example 2:**

```
Input: intervals = [[1,4],[2,3]]
Output: 1
```





## Solution : Sweep Line

```java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
      
      	// b[1] - a[1] 是为了如果出现某一数据涵盖范围很大，则可以尽快找出他来，其余的作为子集只需++即可
      	// 直接就排好了顺序太强了
      	// 只需对比end就可以了
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);
        
        int res = 0;
        int cur = 0;
        for (int[] i : intervals) {
            if (cur < i[1]) {
                cur = i[1];
                res++;
            }
        }
        return res;
    }
}
```





### Wrong solution:

没法进行跳过处理（不过应该也行？哈哈）

```java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        
        int res = 0;
        int[] cur = intervals[0];
        for (int i = 1; i < intervals.length; i++) {
            if (cur[1] >= intervals[i][1]) {
                if (cur[0] <= intervals[i][0]) {
                    res++;
                    if (i > intervals.length - 2) {
                        cur = intervals[i + 1];
                    } else break;
                }
            }
            cur = intervals[i];
        }
        
        return res;
    }
}
```

