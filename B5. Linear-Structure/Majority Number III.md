###Majority Number III

Given an array of integers and a number k, the majority number is the number that occurs `more than 1/k` of the size of the array.

Find it.

##### Notice

There is only one majority number in the array.

**Example**

Given `[3,1,2,3,2,3,3,4,4,4]`and `k=3`, return `3`.



```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @param k: An integer
     * @return: The majority number
     */
    public int majorityNumber(List<Integer> nums, int k) {
        // write your code here
        
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        
        for (int num : nums) {
            
            if (!map.containsKey(num)) {
                map.put(num, 0);
            }
            
            map.put(num, map.get(num) + 1);
        }
        
        int maxKey = 0;
        int maxFreq = Integer.MIN_VALUE;
        
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            
            int freq = entry.getValue();
            
            if (freq >= nums.size() / k && maxFreq < freq) {
                maxFreq = freq;
                maxKey = entry.getKey();
            }
        }
        
        return maxKey;
    }
}
```





* nine chapter

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: As described
     * @return: The majority number
     */
    public int majorityNumber(ArrayList<Integer> nums, int k) {
        // count at most k keys.
        HashMap<Integer, Integer> counters = new HashMap<Integer, Integer>();
        for (Integer i : nums) {
            if (!counters.containsKey(i)) {
                counters.put(i, 1);
            } else {
                counters.put(i, counters.get(i) + 1);
            }
            
            if (counters.size() >= k) {
                removeKey(counters);
            }
        }
        
        // corner case
        if (counters.size() == 0) {
            return Integer.MIN_VALUE;
        }
        
        // recalculate counters
        for (Integer i : counters.keySet()) {
            counters.put(i, 0);
        }
        for (Integer i : nums) {
            if (counters.containsKey(i)) {
                counters.put(i, counters.get(i) + 1);
            }
        }
        
        // find the max key
        int maxCounter = 0, maxKey = 0;
        for (Integer i : counters.keySet()) {
            if (counters.get(i) > maxCounter) {
                maxCounter = counters.get(i);
                maxKey = i;
            }
        }
        
        return maxKey;
    }
    
    private void removeKey(HashMap<Integer, Integer> counters) {
        Set<Integer> keySet = counters.keySet();
        List<Integer> removeList = new ArrayList<>();
        for (Integer key : keySet) {
            counters.put(key, counters.get(key) - 1);
            if (counters.get(key) == 0) {
                removeList.add(key);
            }
        }
        for (Integer key : removeList) {
            counters.remove(key);
        }
    }
}
```

