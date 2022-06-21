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

