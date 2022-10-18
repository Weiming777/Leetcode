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





## Solution : Sweep Line

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





## Solution: Priority Queue

```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
      
      	// 这个queue要按end time去进行排序
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[1] - b[1]);
      
      	// 这里offer进去的只是个地址     ？？？？？？？？？？
        if (intervals.length != 0) heap.offer(intervals[0]);
      
        for (int i = 1; i < intervals.length; i++) {
            int[] cur = heap.poll();
          	// 如果结束时间比下一场开始时间早，则更换cur为下一场会议
          	// 也就是下一场会议依旧使用上一场会议的地址
            if (cur[1] <= intervals[i][0]) 
                cur[1] = intervals[i][1];
          	// 如果结束时间比下一场开始时间晚，赋予新地址
            else heap.offer(intervals[i]);
          	// 把上一场的地址重新加回去
            heap.offer(cur);
        }
        return heap.size();
    }
}
```





## Solution :

![image-20221018155848285](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018155848285.png)

![image-20221018155921699](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018155921699.png)