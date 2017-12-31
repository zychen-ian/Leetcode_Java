### Strings Homomorphism

http://www.lintcode.com/en/problem/strings-homomorphism/

Given two strings **s**and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.





* For string problems, always ask what is the possible characters set of a given string, you may be able to optimize the space usage if there are only ASCII characters.
* a mapping from a char in s to a char in t

```java
public class Solution {
    /*
     * @param s: a string
     * @param t: a string
     * @return: true if the characters in s can be replaced to get t or false
     */
    public boolean isIsomorphic(String s, String t) {
        // write your code here
        
        if (s == null || s.length() == 0) {
            return false;
        }
        
        if (t == null || t.length() == 0) {
            return false;
        }
        
        if (t.length() != s.length()) {
            return false;
        }
        
        // paper 
        // title
        
        // int[] to store mapping bet. char and char (e.g., 'p' & 't')
        // ASCII: 0 ~ 255
        // MUST use 2 maps!! 
        // mapping of a char in A VS. a char in B
      
        int[] m1 = new int[256]; // space optimization 
                                 // not always use set/map
                                 // especially for string problem
        int[] m2 = new int[256];
        
        for (int i = 0; i < 256; i++) {
            m1[i] = Integer.MAX_VALUE; // initial
            m2[i] = Integer.MAX_VALUE; // initial
        }
        
        // note that 'p' in s mapping to 't' in t
        // is different from  (one-way binding)
        // 't' in s mapping to 'p' in t
        for (int i = 0; i < s.length(); i++) {
            int sc = (int) s.charAt(i); // 'p'
            int tc = (int) t.charAt(i); // 't'
            
            // 2 good cases: 
            // m1[sc] = tc
            // m2[tc] = Integer.MIN_VALUE
          
            // otherwise, return false
          
            if (m1[sc] == Integer.MAX_VALUE) {
                
                if (m2[tc] == Integer.MAX_VALUE) {
                    // available for mapping
                    
                    m1[sc] = tc;
                    m2[tc] = Integer.MIN_VALUE;
                    
                } else { // Integer.MIN_VALUE 
                         // tc is mapped by other char in s
                    return false;
                }
                
            } else if (m1[sc] != tc) {
                         // sc is mapped to other char (NOT tc)
                return false;
            }
        }
        
        return true;
    }
}
```

