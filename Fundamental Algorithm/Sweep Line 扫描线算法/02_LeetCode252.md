# 252.Meeting Rooms

Given an array of meeting time `intervals` where `intervals[i] = [starti, endi]`, determine if a person could attend all meetings.

 

**Example 1:**

```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: false
```

**Example 2:**

```
Input: intervals = [[7,10],[2,4]]
Output: true
```





## Solution : Sweep Line

```java
class Solution {
    public boolean canAttendMeetings(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
      	for (int i = 0; i < intervals - 1; i++) {
          if (intervals[i][1] > intervals[i + 1][0]) 
            return false;
        }
      return true;
    }
}
```





### Arrays.sort:

1 Java内置的静态方法Arrays.sort()默认是将数组调整为升序，它的代码中实现了Compareable接口的compare(a,b)方法，该方法用于比较两个元素的大小。

2 而它实现的compare(a,b)方法默认是这样的：若a>b，输出正数；若a<b，输出负数；若a=b，输出0。它的方法体实际代码为：return a-b;

3.1 若我们将compare(a,b)方法重写，相比原先默认的，将它的输出值的正负符号取反；

3.2 对于内置Arrays.sort()的除compare(a,b)方法外的其他代码保留不变。这样改写后调用sort，出来的结果将相反，即实现数组降序。

4 即将compare(a,b)方法重写为这样：若a>b，输出负数；若a<b，输出正数；若a=b，输出0。故，方法体要改写成这样的代码：return -(a-b);（即return b-a;）

5.如果是二维数组，则a[0] 表示第0列，a[1]表示第1列。

原文链接：https://blog.csdn.net/GsxxInCsdn/article/details/122147184