# 59.Spiral Matrix II

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2:**

```java
Input: n = 1
Output: [[1]]
```



## Solution 1: 

假设为3*3方块，则先填充【0】【1】和【0】【2】，之后【0】【3】，【1】【3】，最后【2】【3】，【2】【2】。

以此类推。

最中心的方块需要单独拿出来赋值。

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int loop = 0; // record loop times
        int count = 1;  // record numbers
        int start = 0;  
        int i = 0;
        int j = 0;
    
        while (loop++ < n / 2) {
            for (i = start; i < n - loop; i++) {
                res[start][i] = count++;
            }
            for (j = start; j < n - loop; j++) {
                res[j][i] = count++;
            }
            for (; i >= loop; i--) {
                res[j][i] = count++;
            }
            for (; j >= loop; j--) {
                res[j][i] = count ++;
            }
            start++;
        }
        
        if (n % 2 == 1) {
            res[start][start] = count;
        }
        
        return res;
    }
}
```

