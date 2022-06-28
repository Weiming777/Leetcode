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





