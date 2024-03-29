# 1272.Remove Interval

A set of real numbers can be represented as the union of several disjoint intervals, where each interval is in the form `[a, b)`. A real number `x` is in the set if one of its intervals `[a, b)` contains `x` (i.e. `a <= x < b`).

You are given a **sorted** list of disjoint intervals `intervals` representing a set of real numbers as described above, where `intervals[i] = [ai, bi]` represents the interval `[ai, bi)`. You are also given another interval `toBeRemoved`.

Return *the set of real numbers with the interval* `toBeRemoved` ***removed** from* `intervals`*. In other words, return the set of real numbers such that every* `x` *in the set is in* `intervals` *but **not** in* `toBeRemoved`*. Your answer should be a **sorted** list of disjoint intervals as described above.*

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/24/removeintervalex1.png)

```
Input: intervals = [[0,2],[3,4],[5,7]], toBeRemoved = [1,6]
Output: [[0,1],[6,7]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/12/24/removeintervalex2.png)

```
Input: intervals = [[0,5]], toBeRemoved = [2,3]
Output: [[0,2],[3,5]]
```

**Example 3:**

```
Input: intervals = [[-5,-4],[-3,-2],[1,2],[3,5],[8,9]], toBeRemoved = [-1,4]
Output: [[-5,-4],[-3,-2],[4,5],[8,9]]
```





## Solution : Sweep Line

![image-20221018174014218](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018174014218.png)

```java
class Solution {
    public List<List<Integer>> removeInterval(int[][] intervals, int[] toBeRemoved) {
        List<List<Integer>> res = new ArrayList<>();
        
        for (int[] cur : intervals) {
            if (cur[1] <= toBeRemoved[0] || cur[0] >= toBeRemoved[1]) {
                res.add(Arrays.asList(cur[0], cur[1]));
            } 
            else {
                if (cur[0] < toBeRemoved[0]) {
                    res.add(Arrays.asList(cur[0], toBeRemoved[0]));
                } 
                if (cur[1] > toBeRemoved[1]) {
                    res.add(Arrays.asList(toBeRemoved[1], cur[1]));
                }
            }
        }
        return res;
    }
}
```

改进了一下，提前判断是否被toBeRemoved全覆盖，如果全覆盖，直接跳过cur。

```java
class Solution {
    public List<List<Integer>> removeInterval(int[][] intervals, int[] toBeRemoved) {
        List<List<Integer>> res = new ArrayList<>();
        
        for (int[] cur : intervals) {
            if (cur[1] <= toBeRemoved[0] || cur[0] >= toBeRemoved[1]) {
                res.add(Arrays.asList(cur[0], cur[1]));
            } else if(cur[0] > toBeRemoved[0] && cur[1] < toBeRemoved[1]) {
                continue;
            } else {
                if (cur[0] < toBeRemoved[0]) {
                    res.add(Arrays.asList(cur[0], toBeRemoved[0]));
                } 
                if (cur[1] > toBeRemoved[1]) {
                    res.add(Arrays.asList(toBeRemoved[1], cur[1]));
                }
            }
        }
        return res;
    }
}
```

