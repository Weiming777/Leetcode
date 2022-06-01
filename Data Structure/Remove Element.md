# 27.Remove Element

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` *after placing the final result in the first* `k` *slots of* `nums`.

Do **not** allocate extra space for another array. You must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

**Custom Judge:**

The judge will test your solution with the following code:

```
int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be **accepted**.

 

**Example 1:**

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

**Example 2:**

```java
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```





## Solution: Two pointers

思路：如果fastIndex的值和val不一样，则立刻将其与最前面的数字交换（slowIndex所在位置）。

交换结束后将slowIndex向前移动一位，等待与后面遍历的，符合条件的，fastIndex交换。

```java
class Solution{
  public int removeElement(int[] nums, int val){
    int slowIndex = 0;
    int fastIndex = 0;
    for(; fastIndex < nums.length; fastIndex++){
      if (nums[fastIndex] != val){
        nums[slowIndex] = nums[fastIndex];
        slowIndex++;
      }
    }
    return slowIndex;
  }
}
```



# 26.Remove Duplicates from Sorted Array

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only **once**. The **relative order** of the elements should be kept the **same**.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` *after placing the final result in the first* `k` *slots of* `nums`.

Do **not** allocate extra space for another array. You must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

**Custom Judge:**

The judge will test your solution with the following code:

```java
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be **accepted**.

 

**Example 1:**

```java
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

**Example 2:**

```java
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```



## Solution: Two Pointers

```java
class Solution{
  public int removeDuplicates(int[] nums) {
    int fastPointer = 1;
    int slowPointer = 0;
    for (; fastPointer < nums.length; fastPointer++){
      if (nums[fastPointer] != nums[slowPointer]){
        slowPointer++;
        nums[slowPointer] == nums[fastPointer];
      }
    }
    return ++slowPointer;
  }
}
```



# 283.Move Zeroes

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

 

**Example 1:**

```java
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Example 2:**

```java
Input: nums = [0]
Output: [0]
```



## Solution: Two Pointers

```java
class Solution {
  public void moveZeroes(int[] nums) {
    int fastPointer = 1;
    int slowPointer = 0;
    for (; fastPointer < nums.length && slowPointer < nums.length; ){
      if (nums[slowPointer] == 0){
        nums[slowPointer] = nums[fastPointer];
        nums[fastPointer] = 0;
      }
      if (nums[slowPointer] == 0){
        fastPointer++;
      } else {
        fastPointer++;
        slowPointer++;
      }
    }
  }
}
```





# 844.Backspace String Compare

Given two strings `s` and `t`, return `true` *if they are equal when both are typed into empty text editors*. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

 

**Example 1:**

```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```

**Example 2:**

```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```

**Example 3:**

```java
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```





## Solution 1: Two pointer 

```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int sLength = s.length();
        int tLength = t.length();
        int sSkip = 0;
        int tSkip = 0;
        
        while (sLength > 0 || tLength > 0){
            while (sLength > 0){
                if (s.charAt(sLength - 1) == '#'){
                    sSkip ++;
                    sLength --;
                } else if (sSkip > 0) {
                    sSkip --;
                    sLength --;
                } else {
                    break;
                }
            }
            
            while (tLength > 0) {
                if (t.charAt(tLength -1) == '#'){
                    tSkip ++;
                    tLength --;
                } else if (tSkip > 0){
                    tSkip --;
                    tLength --;
                } else {
                    break;
                }
            }
            
            if (sLength > 0 && tLength > 0 && s.charAt(sLength - 1) != t.charAt(tLength - 1)){
                return false;
            }
            if ((sLength > 0) != (tLength > 0)){
                return false;
            }
            
            sLength--;
            tLength--;
        }
        return true;
    }
}
```



## Solution 2: Build String

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        return build(S).equals(build(T));
    }
    
    String build(String s) {
        Stack<Character> s2 = new Stack();
        for (char c: s.toCharArray()){
            if (c != '#') {
                s2.push(c);
            } else if (!s2.empty()) {
                s2.pop();
            }
        }
        return String.valueOf(s2);
    }
}
```



# 977.Squares of a Sorted Array

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

 

**Example 1:**

```java
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

**Example 2:**

```java
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```



## Solution 1: Square first and sort it.

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] temp = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++){
            temp[i] = nums[i] * nums[i];
        }
        
        int temp1;
        
        for (int j = 0; j < nums.length- 1; j++){
            for (int k = 0; k < nums.length - j - 1; k++){
                if (temp[k] > temp[k + 1]){
                    temp1 = temp[k];
                    temp[k] = temp[k + 1];
                    temp[k + 1] = temp1;
                }
            }
        }
        return temp;
    }
}
```



## Solution 2: Two Pointer

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
      	int[] result = new int[nums.length];
      	int left = 0;
      	int right = nums.length - 1;
      	int temp = 0;
      	int i = nums.length - 1;
      
        while (left <= right) {
          if (Math.abs(nums[left]) < Math.abs(nums[right])) {
            temp = nums[right];
            right --;
          } else if (Math.abs(nums[left]) >= Math.abs(nums[right])) {
            temp = nums[left];
            left ++;
          }
          result[i] = temp * temp;
          i--;
        }
      
      	return result;
    }
}
```





## Solution 3: using Arrays.sort() function

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] temp = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++){
            temp[i] = nums[i] * nums[i];
        }
        
        Arrays.sort(temp);
        
        return temp;
    }
}
```

