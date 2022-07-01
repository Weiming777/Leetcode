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

```java
class Solution {
    public String removeDuplicates(String s) {
        int n = s.length();
        
        Stack<Character> stack = new Stack<Character>();
        
        stack.push(s.charAt(0));
        
        for (int i = 1; i < n; i++) {
            if (!stack.isEmpty() && s.charAt(i) == stack.peek()) {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (char c : stack) {
            sb.append(c);
        }
        
        return sb.toString();
    }
}
```

```java
// The best
class Solution {
  public String removeDuplicates(String S) {
    StringBuilder sb = new StringBuilder();
    int sbLength = 0;
    for(char character : S.toCharArray()) {
      if (sbLength != 0 && character == sb.charAt(sbLength - 1))
        sb.deleteCharAt(sbLength-- - 1);
      else {
        sb.append(character);
        sbLength++;
      }
    }
    return sb.toString();
  }
}
```





# 150.Evaluate Reverse Polish Notation

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

 

**Example 1:**

```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```



## Solution : Stack

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        
        int n = tokens.length;
        
        for (int i = 0; i < n; i++) {
            if ("*".equals(tokens[i])) {                // leetcode 内置jdk的问题，不能使用==判断字符串是否相等
                stack.push(stack.pop() * stack.pop());
            } else if ("/".equals(tokens[i])) {         // 注意 - 和/ 需要特殊处理
                int temp1 = stack.pop();
                int temp2 = stack.pop();
                stack.push(temp2 / temp1);
            } else if ("-".equals(tokens[i])) {
                stack.push(-stack.pop() + stack.pop());
            } else if ("+".equals(tokens[i])) {
                stack.push(stack.pop() + stack.pop());
            } else {
                stack.push(Integer.valueOf(tokens[i]));
            }
        }
        
        return stack.pop();
    }
}
```

