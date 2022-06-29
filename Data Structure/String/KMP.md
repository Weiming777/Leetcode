# KMP

String : aabaabaaf

Model string : aabaaf



KMP will after first loop to notice "f" in model string is not match with original string, it will find minium match prefix of model string, and continue loop with String[minium match prefix] with first letter in model string.



In this process, we need a "next" array to help us record prefix of model string.

```java
int[] getNext(int[] next,String modelString) {
  	// Initialization
		j = 0;
		next[0] = 0;
		
  	for (int i = 0; i < modelString.length(); i++) {
      // Prefix different
      while (j > 0 && modelString.charAt(i) != modelString.charAt(j)) {
        j = next[j - 1];
      }
      // Same prefix
      if (modelString.charAt(i) == modelString.charAt(j)) {
        j++;
      }
      // Update next
      next[i] = j;
    }
  
  return next;
}
```



"NEXT" array has three types:

1. As I code in the above, when we find different letter in the orginal string, we will know which letter in the model letter is different, and using this letter's index and min it one, to get the letter's "next" array number before it, and this number is which letter we should continue loop to match with original array. In this case, the loop number i of original string is not change, just the loop number j of model string is changed.
2. After we got the "next" array, we can right shift each number of "next" array and set the next[0] equal zero. In this case, when the letter of model array is not match with original array, we can get this number's index as "next" array's index to find which letter in the model array we should back off and loop again.
3. I do not make sense of this method. This method min each number of "next" array.



Video: https://www.bilibili.com/video/BV1M5411j7Xx/?spm_id_from=333.788&vd_source=4de6d1b67eb3cce826c252d2eb75d494



# 28.Implement strStr()

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

 

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```





## Solution 1: sliding window

```java
class Solution {
    public int strStr(String haystack, String needle) { 
        int firstn = haystack.length();
        
        int slideWindow = needle.length();
        
        if (slideWindow > firstn) {
            return -1;
        }
        
        char[] h = haystack.toCharArray();
        char[] n = needle.toCharArray();
        
        int first = 0;
        int second = 0;
        
        for (; first < firstn;) {
            int j = 0;
            second = first;
            
            while (second < firstn && h[second] == n[j]) {
                second++;
                j++;
                
                if (j == slideWindow) {
                    return first;
                }
            }
            
            first++;
        }
        
        return -1;
    }
}
```





## Solution 2: KPM

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int[] next = new int[needle.length()];
        getnext(next, needle);
        
        int hl = haystack.length();
        int nl = needle.length();
        
        int j = 0;
        
        for (int i = 0; i < hl; i++) {
            
            while (j > 0 && haystack.charAt(i) != needle.charAt(j)) {
                j = next[j - 1];
            }
            if (j < nl && haystack.charAt(i) == needle.charAt(j)) {
                j++;
            }
            
            if (j == nl) {
                return i - nl + 1;
            }
        }
        return -1;
    }
    
    public int[] getnext(int[] next, String n) {
        int j = 0;
        next[0] = 0;
        int nl = n.length();
        
        for (int i = 1; i < nl; i++) {
            while ( j > 0 && n.charAt(i) != n.charAt(j)) {
                j = next[j - 1];
            }
            
            if (n.charAt(i) == n.charAt(j)) {
                j++;
            }
            
            next[i] = j;
        }
        
        return next;
    }
}
```







# 459.Repeated Substring Pattern

Given a string `s`, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

 

**Example 1:**

```
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.
```

**Example 2:**

```
Input: s = "aba"
Output: false
```

**Example 3:**

```
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.
```





## Solution : KMP

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        if (s.equals("")) return false;

        int len = s.length();
        // 原串加个空格(哨兵)，使下标从1开始，这样j从0开始，也不用初始化了
        s = " " + s;
        char[] chars = s.toCharArray();
        int[] next = new int[len + 1];

        // 构造 next 数组过程，j从0开始(空格)，i从2开始
        for (int i = 2, j = 0; i <= len; i++) {
            // 匹配不成功，j回到前一位置 next 数组所对应的值
            while (j > 0 && chars[i] != chars[j + 1]) j = next[j];
            // 匹配成功，j往后移
            if (chars[i] == chars[j + 1]) j++;
            // 更新 next 数组的值
            next[i] = j;
        }

        // 最后判断是否是重复的子字符串，这里 next[len] 即代表next数组末尾的值
        if (next[len] > 0 && len % (len - next[len]) == 0) {
            return true;
        }
        return false;
    }
}
```



next 数组记录的就是最长相同前后缀( [字符串：KMP算法精讲 (opens new window)](https://programmercarl.com/0028.实现strStr.html)这里介绍了什么是前缀，什么是后缀，什么又是最长相同前后缀)， 如果 next[len - 1] != -1，则说明字符串有最长相同的前后缀（就是字符串里的前缀子串和后缀子串相同的最长长度）。

最长相等前后缀的长度为：next[len - 1] + 1。(这里的next数组是以统一减一的方式计算的，因此需要+1)

数组长度为：len。

如果len % (len - (next[len - 1] + 1)) == 0 ，则说明 (数组长度-最长相等前后缀的长度) 正好可以被 数组的长度整除，说明有该字符串有重复的子字符串。

**数组长度减去最长相同前后缀的长度相当于是第一个周期的长度，也就是一个周期的长度，如果这个周期可以被整除，就说明整个数组就是这个周期的循环。**

**强烈建议大家把next数组打印出来，看看next数组里的规律，有助于理解KMP算法**

如图：

![459.重复的子字符串_1](https://code-thinking.cdn.bcebos.com/pics/459.%E9%87%8D%E5%A4%8D%E7%9A%84%E5%AD%90%E5%AD%97%E7%AC%A6%E4%B8%B2_1.png)

next[len - 1] = 7，next[len - 1] + 1 = 8，8就是此时字符串asdfasdfasdf的最长相同前后缀的长度。

(len - (next[len - 1] + 1)) 也就是： 12(字符串的长度) - 8(最长公共前后缀的长度) = 4， 4正好可以被 12(字符串的长度) 整除，所以说明有重复的子字符串（asdf）。