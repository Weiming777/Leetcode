# 242.Valid Anagram

Given two strings `s` and `t`, return `true` *if* `t` *is an anagram of* `s`*, and* `false` *otherwise*.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```





## Solution 1: Sorting

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()){
            return false;
        }
        
        char[]  s1 = s.toCharArray();
        char[]  t1 = t.toCharArray();
        Arrays.sort(s1);
        Arrays.sort(t1);
        return Arrays.equals(s1, t1);
    }
}
```



## Solution 2: Hash table (counter)

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()){
            return false;
        }
        
      	// 26个字母各有一个位置
        int[] counter = new int[26];
      	
      	//通过使用.charAt(i) - 'a'改为数字，装入对应字母的数组中
        for (int i = 0; i < s.length(); i++) {
            counter[s.charAt(i) - 'a'] ++;
            counter[t.charAt(i) - 'a'] --;
        }
      
        //超级遍历：将counter中的值依次赋值给count去进行操作
        for (int count : counter) {
            if (count != 0) {
                return false;
            }
        }
        return true;
    }
}
```

