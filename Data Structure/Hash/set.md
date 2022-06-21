# 349.Intersection of Two Arrays

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must be **unique** and you may return the result in **any order**.

 

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```





## Solution : HashSet

HashSet和HashMap差不多，但HashSet不允许有重复的元素存在。

```java
class Solution {
  public int[] intersection(int[] nums1, int[] nums2) {
    HashSet<Integer> set1 = new HashSet<Integer>();
    for (Integer n : nums1) set1.add(n);
    HashSet<Integer> set2 = new HashSet<Integer>();
    for (Integer n : nums2) set2.add(n);

    set1.retainAll(set2);

    int [] output = new int[set1.size()];
    int idx = 0;
    for (int s : set1) output[idx++] = s;
    return output;
  }
}
```





# 202.Happy Number

Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
- Those numbers for which this process **ends in 1** are happy.

Return `true` *if* `n` *is a happy number, and* `false` *if not*.

 

**Example 1:**

```
Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**Example 2:**

```
Input: n = 2
Output: false
```





## Solution 1: HashSet

```java
class Solution {
    public boolean isHappy(int n) {
      HashSet<Integer> record = new HashSet<>();
      while (n != 1 && !record.contains(n)) {
        record.add(n);
        n = squareNum(n);
      }
      
      return n == 1;
    }
  
  	public int squareNum(int n) {
      int res = 0;
      while (n > 0) {
        int temp = n % 10;
        res += temp * temp;
        n /= 10;
      }
      
      return res;
    }
}
```



# 知识点：

## 1. 判断一个数字的位数

```java
int n; // 待判断的数字
int i; // 最终i将记录数字的个数
for (i = 0; n > 0; i++) {
  n /= 10;
}
```

## 2. % 和 /

```java
// % 取余
10 % 5 = 0
// 运用：一个数字用10取余，可以得到个位数字：798 % 10 = 8

// / 除
10 / 5 = 2
// 运用：一个数字除10，可以去除最低位数字：798 / 10 = 79
```

