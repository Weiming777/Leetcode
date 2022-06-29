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

