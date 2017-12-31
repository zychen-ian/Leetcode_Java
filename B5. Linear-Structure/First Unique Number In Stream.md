###First Unique Number In Stream

http://www.lintcode.com/en/problem/first-unique-number-in-stream/#

Given a continuous stream of numbers, write a function that returns the first unique number whenever terminating number is reached(include terminating number). If there no unique number before terminating number or you can't find this terminating number, return `-1`.

**Example**

Given a stream `[1, 2, 2, 1, 3, 4, 4, 5, 6]` and a number `5`
return `3`

Given a stream `[1, 2, 2, 1, 3, 4, 4, 5, 6]` and a number `7`
return `-1`



```java
public class Solution {
    /*
     * @param : a continuous stream of numbers
     * @param : a number
     * @return: returns the first unique number
     */
    public int firstUniqueNumber(int[] nums, int number) {
        // Write your code here
        
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        Deque<Integer> queue = new LinkedList<Integer>();
        Set<Integer> hash = new HashSet<Integer>();
        
        for (int n : nums) {
            
            if (hash.contains(n)) { // not unique
                
                queue.removeFirstOccurrence(n);
            } else { // unique
                hash.add(n);
                queue.offer(n); // 
            }
            
            if (n == number) {
                if (!queue.isEmpty()) {
                    return queue.peek();    
                } else { // no unique number before terminating number
                    return -1;
                }
            }
        }
        
        // can't find this terminating number
        return -1;
    }
};
```

