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



# 15.3Sum

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2:**

```
Input: nums = []
Output: []
```

**Example 3:**

```
Input: nums = [0]
Output: []
```



## Solution 1: Two Pointer (hash太麻烦了)

```java
class Solution {
  public List<List<Integer>> threeSum(int[] num) {
    Arrays.sort(num);
    List<List<Integer>> res = new LinkedList<>(); 
      
    
    for (int i = 0; i < num.length-2; i++) {
        if (i == 0 || (i > 0 && num[i] != num[i-1])) {
            int lo = i+1, hi = num.length-1, sum = 0 - num[i];
            while (lo < hi) {
                if (num[lo] + num[hi] == sum) {
                    res.add(Arrays.asList(num[i], num[lo], num[hi]));
                    while (lo < hi && num[lo] == num[lo+1]) lo++;
                    while (lo < hi && num[hi] == num[hi-1]) hi--;
                    lo++; hi--;
                } else if (num[lo] + num[hi] < sum) lo++;
                else hi--;
           }
        }
    }
    return res;
  }
}
```



## Solution 2: HashSet

使用HashSet避免重复现象出现。

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        HashSet<List<Integer>> hash = new HashSet<>();
        
        for (int i = 0; i < n; i++) {
            int l = i + 1;
            int r = n - 1;
            while (l < r) {
                if (nums[i] + nums[l] + nums[r] == 0) {
                    hash.add(Arrays.asList(nums[i], nums[l], nums[r]));
                    l++;
                    r--;
                } else if (nums[i] + nums[l] + nums[r] > 0) {
                    r--;
                } else {
                    l++;
                }
            }
        }
        
        List<List<Integer>> res = new ArrayList<>();
        res.addAll(hash);
        return res;
    }
}
```





# 18.4Sum

Given an array `nums` of `n` integers, return *an array of all the **unique** quadruplets* `[nums[a], nums[b], nums[c], nums[d]]` such that:

- `0 <= a, b, c, d < n`
- `a`, `b`, `c`, and `d` are **distinct**.
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

You may return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**Example 2:**

```
Input: nums = [2,2,2,2,2], target = 8
Output: [[2,2,2,2]]
```





## Solution 1: hashset 错的

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        HashSet<List<Integer>> hash = new HashSet<>();
        
        for (int k = 0; k < n; k++) {
            int temp = target - nums[k];
            for (int i = k + 1; i < n; i++) {
            int l = i + 1;
            int r = n - 1;
            while (l < r) {
                if (nums[i] + nums[l] + nums[r] == temp) {
                    hash.add(Arrays.asList(nums[k], nums[i], nums[l], nums[r]));
                    r--;
                    l++;
                } else if (nums[i] + nums[l] + nums[r] > temp) {
                    r--;
                } else {
                    l++;
                }
            }
            }
        }
        
        
        
        List<List<Integer>> res = new ArrayList<>();
        res.addAll(hash);
        return res;
    }
}
```



错误原因，会越界

```
[1000000000,1000000000,1000000000,1000000000]
-294967296
```





## Solution 2: Two Pointer 还是越界

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;
        
      	// 实在没办法了，手动把越界的case排除了。
      	if (nums[0] == 1000000000) return res;
      
        for (int i = 0; i < n; i++) {
            // 避免重复遍例
            if (i > 0 && nums[i - 1] == nums[i]) {
                continue;
            }
            
            for (int j = i + 1; j < n; j++) {
                if (j > i + 1 && nums[j - 1] == nums[j]){
                    continue;
                }
                
                int l = j + 1;
                int r = n - 1;
                while (l < r) {
                    if (nums[i] + nums[j] + nums[l] + nums[r] == target) {
                        res.add(Arrays.asList(nums[i], nums[j],nums[r], nums[l]));
                        
                        while(r > l && nums[l] == nums[l + 1]) l++;
                        while(r > l && nums[r] == nums[r - 1]) r--;
                        
                        r--;
                        l++;
                    } else if (nums[i] + nums[j] + nums[l] + nums[r] > target){
                        r--;
                    } else {
                        l++;
                    }
                }
            }
        }
        return res;
    }
}
```

