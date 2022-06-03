# 209.Minimum Size Subarray Sum

Given an array of positive integers `nums` and a positive integer `target`, return the minimal length of a **contiguous subarray** `[numsl, numsl+1, ..., numsr-1, numsr]` of which the sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

 

**Example 1:**

```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

**Example 2:**

```
Input: target = 4, nums = [1,4,4]
Output: 1
```

**Example 3:**

```java
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```



## Solution 1: Sliding window

```java
class Solution {
    public int minSubArrayLen(int s, int[] a) {
        if (a == null || a.length == 0)
            return 0;
  
        int i = 0, j = 0, sum = 0, min = Integer.MAX_VALUE;
  
        while (j < a.length) {
            sum += a[j++];
    
            while (sum >= s) {
                min = Math.min(min, j - i);
                sum -= a[i++];
            }
        }
  
        return min == Integer.MAX_VALUE ? 0 : min;
    }
}
```



# 904.Fruit Into Baskets

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array `fruits` where `fruits[i]` is the **type** of fruit the `ith` tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

- You only have **two** baskets, and each basket can only hold a **single type** of fruit. There is no limit on the amount of fruit each basket can hold.
- Starting from any tree of your choice, you must pick **exactly one fruit** from **every** tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
- Once you reach a tree with fruit that cannot fit in your baskets, you must stop.

Given the integer array `fruits`, return *the **maximum** number of fruits you can pick*.

 

**Example 1:**

```
Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.
```

**Example 2:**

```
Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].
```

**Example 3:**

```java
Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].
```





## Solution 1: Sliding window

```java
class Solution {
    public int totalFruit(int[] fruits) {
      int n = fruits.length;
      if (n <= 2) return n;
      
      int left = 0;
      int right = 0;
      
      int ans = 2;
      int count = 0;
      
     	int[] freq = new int[n];
      
      while (right < n) {
        freq[fruits[right]]++;
        if (freq[fruits[right]] == 1) count++;  //这类水果首次入篮
        right++;
        
        while (count > 2) {
          freq[fruits[left]]--;
          if (freq[fruits[left]] == 0) count--;  //确保左指针移动到了，left到right之间只有2个水果的位置
          left++;
        }
        ans = Math.max(ans, right - left);
      }
      return ans;
    }
}
```

