# 344.Reverse String

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

 

**Example 1:**

```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```





## Solution :

```java
class Solution {
    public void reverseString(char[] s) {
        int l = 0;
        int r = s.length - 1;
        while (l < r) {
            char temp = s[l];
            s[l] = s[r];
            s[r] = temp;
            l++;
            r--;
        }
    }
}
```





# 541.Reverse String II

Given a string `s` and an integer `k`, reverse the first `k` characters for every `2k` characters counting from the start of the string.

If there are fewer than `k` characters left, reverse all of them. If there are less than `2k` but greater than or equal to `k` characters, then reverse the first `k` characters and leave the other as original.

 

**Example 1:**

```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

**Example 2:**

```
Input: s = "abcd", k = 2
Output: "bacd"
```





## Solution :

```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] res = s.toCharArray();
        
        int start = 0;
        int end = s.length() - 1;
        
        while( start < end ) {
            if ((end - start + 1) >= k) {
                reverse(res, start, start + k - 1);
                start += 2 * k;
            }
            else {
                reverse(res, start, end);
                break;
            }
        }
        return new String(res);
    }
    
    public char[] reverse(char[] res, int start, int end) {
        int n = end - start;
        for (; n >= 0 ;) {
            char temp = res[start];
            res[start] = res[end];
            res[end] = temp;
            start++;
            end--;
            n -= 2;
        }
        return res;
    }
}
```

![image-20220628154730113](/Users/weimingqi/Library/Application Support/typora-user-images/image-20220628154730113.png)

## Solution 2: same with solution 1, but more concise.

```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] a = s.toCharArray();
        for (int start = 0; start < a.length; start += 2 * k) {
            int i = start, j = Math.min(start + k - 1, a.length - 1);
            while (i < j) {
                char tmp = a[i];
                a[i++] = a[j];
                a[j--] = tmp;
            }
        }
        return new String(a);
    }
}
```





# 151.Reverse Words in a String

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space.*

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

**Example 1:**

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```





## Solution :

```java
class Solution {
  public String reverseWords(String s) {
    // remove leading spaces
    s = s.trim();
    // split by multiple spaces
    List<String> wordList = Arrays.asList(s.split("\\s+"));
    Collections.reverse(wordList);
    return String.join(" ", wordList);
  }
}
```

