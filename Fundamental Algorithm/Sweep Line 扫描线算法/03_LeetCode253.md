# 253.Meeting Rooms II

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of conference rooms required*.

 

**Example 1:**

```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

**Example 2:**

```
Input: intervals = [[7,10],[2,4]]
Output: 1
```





## Solution :

```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        List<int[]> list = new ArrayList<>();  // used as two dimensional array
        
      	// separate start time and end time, and record them
        // start time and end time completely independent
        for (int[] interval : intervals) {
            list.add(new int[]{interval[0], 1});  // {index, value}
            list.add(new int[]{interval[1], -1});
        }
        
      	// if has same start time, sorting by end time
      	// if not, sorting by start time
        Collections.sort(list, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        
        int cnt = 0;
        int res = 0;
        for (int[] point : list) {
            cnt += point[1];
            res = Math.max(cnt, res);
        }
        return res;
    }
}
```

