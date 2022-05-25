**只要看到面试题里给出的数组是有序数组，都可以想一想是否可以使用二分法。**

同时题目还强调数组中无重复元素，因为一旦有重复元素，使用二分查找法返回的元素下标可能不是唯一的。

# 704.Binary Search

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**

```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```



## Solution

Time complexity: O(log n).

```java
class Solution {
  public int search(int[] nums, int target){
    int pivot;
    int right = nums.length - 1;
    int left = 0;
    while (right >= left){
      pivot = (right - left) / 2 + left;
      if (nums[pivot] > target){
        right = pivot - 1;
      } else if (nums[pivot] < target){
        left = pivot + 1;
      } else {
        return pivot;
      }
    }
    return -1;
  }
}
```



# 35.Search Insert Position

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2:**

```
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3:**

```java
Input: nums = [1,3,5,6], target = 7
Output: 4
```



## Solution: Binary search

Because this is a **ascending** array, so I can just search this array and if this array do not have this number, I can put this number in the "left".

Time complexity: O(log n).

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int pivot;
        int right = nums.length - 1;
        int left = 0;
        while (left <= right){
            pivot = (right - left) / 2 + left;
            if (nums[pivot] > target){
                right = pivot - 1;
            } else if (nums[pivot] < target){
                left = pivot + 1;
            } else {
                return pivot;
            }
        }
        return left;
    }
}
```



## Solution: Brute Force

Time complexity: O(n).

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++){
            if (nums[i] >= target){
                return i;
            }
        }
        return nums.length;
    }
}
```

