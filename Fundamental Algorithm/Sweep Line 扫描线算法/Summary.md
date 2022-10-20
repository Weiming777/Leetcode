# Interval question template  数飞机



一般两种解法，一种是PriorityQueue(heap)，或者将start/end分开进行扫描线。

考点：sort常用comparator写法，判断interval merge的边界条件。



```java
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);  // 正序

PriorityQueue<int[]> pq = new ArrayList<>((a, b) -> (a[0] - b[0])); // pq可对heap中的数据进行排序
```

