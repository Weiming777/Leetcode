# 主要思想：

当为标准正方形时，可以按照59solution的解法来。

当为不规则时，则需要使用四个常量来记录matrix的上下左右四个边界。同时在每转半圈后，在检查从右下到左下时，需要检查是否在同一行遍历，如果时，则重复了，续跳过；从左下到左上同样需要检测。



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





# 54.Spiral Matrix

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```java
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```





## Solution 1: Spiral Form

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int rows = matrix.length;
        int columns = matrix[0].length;
            
        List<Integer> res = new ArrayList<>();
        
        int up = 0;
        int down = rows - 1;
        int left = 0;
        int right = columns - 1;
        
        while (res.size() < rows * columns) {
            for (int col = left; col <= right; col++) {
                res.add(matrix[up][col]);
            }
            for (int row = up + 1; row <= down; row++) {
                res.add(matrix[row][right]);
            }
            // 保证不在同一行
            if (up != down) {
                for (int col = right - 1; col >= left; col--) {
                    res.add(matrix[down][col]);
                }
            }
            // 保证不在同一列
            if (left != right) {
                for (int row = down - 1; row > up; row--) {
                    res.add(matrix[row][left]);
                }
            }
            
            left++;
            right--;
            up++;
            down--;
        }
        
        return res;
    }
}
```

