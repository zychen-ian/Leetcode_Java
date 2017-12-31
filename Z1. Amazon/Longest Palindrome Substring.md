###Longest Palindrome Substring

https://leetcode.com/problems/longest-palindromic-substring/description/

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example:**

```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.

```

**Example:**

```
Input: "cbbd"

Output: "bb"
```



**Method**

```java
1. LPS length value in terms of position
   LPS value d at position i: substring from position i - d to i + d is a palindrome of length d
2. position can be the acutal character position or the position between two character, extreme left and right positions
   position i : 0 to 2 * length (count: 2 * length + 1)
3. from the 1st actual character postion to the last actual character position, find LPS at position i with d, and if d > maxCount, update maxLPS
```





```java
class Solution {
    public String longestPalindrome(String s) {
        //     " a b a "
        //      0123456 
        // loop: 12345   
        if (s == null || s.length() == 0) {
            return ""; // null
        }
        
        int length = s.length();
        int max = 0;
        String res = "";
        
        for (int i = 1; i <= 2 * length - 1; i++) {
            int count = 1;
            while (i - count >= 0 && i + count <= 2 * length && //
                  ( get(s, i - count) == get(s, i + count) )) {
                count++;
            }
            
            count--; // there will be one extra count for the outbound #
            if (count > max) {
                res = s.substring((i - count) / 2, (i + count) / 2);
                max = count;
            }
        }
        
        return res;
    }
    
    private char get(String s, int i) {
        if (i % 2 == 0) { // even index: extra space
            return '#';
        } else {
            // i:   1, 3, 5, 7...
            // idx: 0, 1, 2, 3...
            return s.charAt(i / 2);
        }
    }
}
```



