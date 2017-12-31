###Valid Parentheses

http://www.lintcode.com/en/problem/valid-parentheses/

Given a string containing just the characters `'(', ')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

**Example**

The brackets must close in the correct order, `"()"`and `"()[]{}"` are all valid but `"(]"` and `"([)]"`are not.



**Method**

* Parenthesis: "([{<"


* "([{" - push into stack
* "}])" - peek from stack to see if it is a pair

```java
public class Solution {
    /*
     * @param s: A string
     * @return: whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        // write your code here
        Stack<Character> sk = new Stack<Character>();
        
        for (char c : s.toCharArray()) {
            
            if ("([{".contains(String.valueOf(c))) {
                sk.push(c);
                
            } else {
                if (!sk.isEmpty() && is_valid(sk.peek(), c)) {
                    sk.pop();                    
                } else {
                    return false;
                }
            }
        }
        
        return sk.isEmpty();
    }
    
    private boolean is_valid(char a, char b) {
        return (a == '(' && b == ')') ||
               (a == '[' && b == ']') ||
               (a == '{' && b == '}');
    }
}
```

