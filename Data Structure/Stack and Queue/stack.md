# 20.Valid Parentheses

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

 

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```





## Solution :

```java
class Solution {
    public boolean isValid(String s) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
      	map.put(')', '(');
        map.put(']', '[');
        map.put('}', '{');
      
      	Stack<Character> stack = new Stack<Character>();
      	int n = s.length();	
      
      	for (int i = 0; i < n; i++) {
          char c = s.charAt(i);
          if (map.containKey(c)) {
            if (stack.empty() || stack.pop() != map.get(c)) return false;
          }
          else {
            stack.push(c);
          }
        }
      	return stack.empty();
    }
}
```





# 1047.Remove All Adjacent Duplicates In String

You are given a string `s` consisting of lowercase English letters. A **duplicate removal** consists of choosing two **adjacent** and **equal** letters and removing them.

We repeatedly make **duplicate removals** on `s` until we no longer can.

Return *the final string after all such duplicate removals have been made*. It can be proven that the answer is **unique**.

 

**Example 1:**

```
Input: s = "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```

**Example 2:**

```
Input: s = "azxxzy"
Output: "ay"
```





# Solution 1: Stack

```java
class Solution {
    public String removeDuplicates(String s) {
        int n = s.length();
        
        Stack<Character> stack = new Stack<Character>();
        
        stack.push(s.charAt(n - 1));
        
        for (int i = (n - 2); i >= 0; i--) {
            if (!stack.isEmpty() && s.charAt(i) == stack.peek()) {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }
        
        String res = new String("");
        int i = 0;
        
        while (!stack.isEmpty()) {
            res += stack.pop();
            i++;
        }
        
        return res;
    }
}
```

```java
class Solution {
    public String removeDuplicates(String s) {
        Stack<Character> characterStack= new Stack<>();
        for (char c: s.toCharArray()) {
            if(!characterStack.isEmpty() && c==characterStack.peek()){
                characterStack.pop();
            }
            else{
                characterStack.push(c);
            }
        }
        StringBuilder sb=new StringBuilder();
        for(char c:characterStack ){
            sb.append(c);
        }
        return sb.toString();
    }
}
```

