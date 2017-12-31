###Longest Palindrome

http://www.lintcode.com/en/problem/longest-palindrome/#

https://yeqiuquan.blogspot.com/2017/03/lintcode-627-longest-palindrome.html

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example `"Aa"` is not considered a palindrome here.

**Example**

Given s = `"abccccdd"` return `7`

One longest palindrome that can be built is `"dccaccd"`, whose length is `7`.



* **Set** NOT Map

```java
public class Solution {
    /*
     * @param s: a string which consists of lowercase or uppercase letters
     * @return: the length of the longest palindromes that can be built
     */
    public int longestPalindrome(String s) {
        // write your code here
        
        if (s == null || s.length() == 0) { // easy to forget
            return 0;
        }
        
        
        int count = 0;
        Set<Character> set = new HashSet<Character>();
        
        for (int i = 0; i < s.length(); i++) {
            
            if (set.contains(s.charAt(i))) {
                set.remove(s.charAt(i));
                count += 2;
            } else {
                set.add(s.charAt(i));
            }
                
        }
        
        if (set.isEmpty()) {
            return count;
        } else {
            return count + 1;
        }
    }
}

```

