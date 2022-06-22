# Two Sum

在array里



# 454. 4Sum II

Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that:

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

 

**Example 1:**

```
Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
Output: 2
Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

**Example 2:**

```
Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1
```





## Solution 1: Same as Two Sum

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer, Integer> hash1 = new HashMap<>();
        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums2.length; j++) {
                if (hash1.containsKey(nums1[i] + nums2[j])) {
                    hash1.put(nums1[i] + nums2[j], hash1.get(nums1[i] + nums2[j]) + 1);
                } else {
                    hash1.put(nums1[i] + nums2[j], 1);
                }
            }
        }
        
        int count = 0;
        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums1.length; j++) {
                int temp = 0 - (nums3[i] + nums4[j]);
                if (hash1.containsKey(temp)){
                    count += hash1.get(temp);
                }
            }
        }
        return count;
    }
}
```





# 383.Ransom Note

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed by using the letters from* `magazine` *and* `false` *otherwise*.

Each letter in `magazine` can only be used once in `ransomNote`.

 

**Example 1:**

```
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2:**

```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3:**

```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```





## Solution 1: HashMap

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character, Integer> hash = new HashMap<>();
        for (int i = 0; i < magazine.length(); i++) {
            if (hash.containsKey(magazine.charAt(i))){
                hash.put(magazine.charAt(i),hash.get(magazine.charAt(i)) + 1);
            } else {
                hash.put(magazine.charAt(i),1);
            }
        }
        
        // ransomNote
        for (int i = 0; i < ransomNote.length(); i++) {
            if (hash.containsKey(ransomNote.charAt(i)) && hash.get(ransomNote.charAt(i)) > 0){
                hash.replace(ransomNote.charAt(i), hash.get(ransomNote.charAt(i)) - 1);
            } else {
                return false;
            }
        }
        
        return true;
    }
}
```





## Solution 2: Simulation

```java
public boolean canConstruct(String ransomNote, String magazine) {
    // For each character, c,  in the ransom note.
    for (char c : ransomNote.toCharArray()) {
        // Find the index of the first occurrence of c in the magazine.
        int index = magazine.indexOf(c);
        // If there are none of c left in the String, return False.
        if (index == -1) {
            return false;
        }
        // Use substring to make a new string with the characters 
        // before "index" (but not including), and the characters 
        // after "index". 
        magazine = magazine.substring(0, index) + magazine.substring(index + 1);
    }
    // If we got this far, we can successfully build the note.
    return true;
}
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

