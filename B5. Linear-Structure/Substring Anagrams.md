###Substring Anagrams (Find All Anagrams in a String)

http://www.lintcode.com/en/problem/substring-anagrams/#

https://leetcode.com/problems/find-all-anagrams-in-a-string/description/

Given a string `s`and a **non-empty**string `p`, find all the start indices of `p`'s anagrams in `s`.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 40,000.

The order of output does not matter.

**Example**

Given s = `"cbaebabacd"` p = `"abc"`

return `[0, 6]`

```
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



```java
public class Solution {
    /*
     * @param s: a string
     * @param p: a string
     * @return: a list of index
     */
    public List<Integer> findAnagrams(String s, String p) {
        // write your code here
        
        List<Integer> res = new ArrayList<Integer>();
        if (s == null || s.length() == 0) {
            return res;
        }
        
        if (p == null || p.length() == 0) {
            return res;
        }
        
        if (s.length() < p.length()) {
            return res;
        }
        
        int[] freq_p = new int[128];
        int[] freq_s = new int[128];
        
        for (int i = 0; i < p.length(); i++) {
            int pc = (int) p.charAt(i);
            int sc = (int) s.charAt(i);
            
            freq_p[pc]++;
            freq_s[sc]++;
        }
        
        
        for (int i = p.length(); i < s.length(); i++) {
            if (same(freq_p, freq_s)) {
                res.add(i - p.length());
            }
            
            freq_s[(int) s.charAt(i)]++;
            freq_s[(int) s.charAt(i - p.length())]--;            
        }
        
        if (same(freq_p, freq_s)) {
            res.add(s.length() - p.length()); // s.length() - p.length()
          									 // NOT s.length() - 1 - p.length()
        }
            
        return res;
    }
    
    private boolean same(int[] a, int[] b) {
        for (int i = 0; i < a.length; i++) {
            if (a[i] != b[i]) {
                return false;
            }
        }
        return true;
    }
}
```

