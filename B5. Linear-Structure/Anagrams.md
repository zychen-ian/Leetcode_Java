###Anagrams

http://www.lintcode.com/en/problem/anagrams/#

Given an array of strings, return all groups of strings that are anagrams.

##### Notice

All inputs will be in **lower-case**

**Example**

Given `["lint", "intl", "inlt", "code"]`, return `["lint", "inlt", "intl"]`.

Given `["ab", "ba", "cd", "dc", "e"]`, return `["ab", "ba", "cd", "dc"]`.



* Map
  * key: unique key
  * value; anagram groups
  * APIs

```java
public class Solution {
    /*
     * @param strs: A list of strings
     * @return: A list of strings
     */
    public List<String> anagrams(String[] strs) {
        // write your code here
        
        List<String> res = new ArrayList<String>();
        
        if (strs == null || strs.length == 0) {
            return res;
        }
        
        Map<String, ArrayList<String>> map = new HashMap<String, ArrayList<String>>();
        for (int i = 0; i < strs.length; i++) {
            
            char[] arr = strs[i].toCharArray();
            Arrays.sort(arr);
            String s = String.valueOf(arr); // char[] -> String used as key
            
            if (!map.containsKey(s)) {
                ArrayList<String> list = new ArrayList<String>();
                map.put(s, list);
            }
            map.get(s).add(strs[i]);
        }
        
        for (Map.Entry<String, ArrayList<String>> entry : map.entrySet()) {
            if (entry.getValue().size() >= 2) { // anagram groups
                result.addAll(entry.getValue());
            }
        }
        
        return result;
    }
}
```





###Group Anagrams

https://leetcode.com/problems/group-anagrams/description/

Given an array of strings, group anagrams together.

For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"]`, 
Return:

```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:** All inputs will be in lower-case.



```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<List<String>>();
        if (strs == null || strs.length == 0) {
            return res;
        }
        
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        
        for (int i = 0; i < strs.length; i++) {
            
            char[] sc = strs[i].toCharArray();
            Arrays.sort(sc);
            String s = String.valueOf(sc);
            
            if (!map.containsKey(s)) {
                List<String> list = new ArrayList<String>();
                map.put(s, list);
            }
            
            map.get(s).add(strs[i]);
        }
        
        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            // !!!!!
            // if (entry.getValue().size() >= 2) {
            res.add(entry.getValue());
            // }
        }
        
        return res;
    }
}

```

