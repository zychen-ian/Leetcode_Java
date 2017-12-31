###Subarray Sum

http://www.lintcode.com/en/problem/subarray-sum/#

Given an integer array, find a subarray where the sum of numbers is **zero**. Your code should return the index of the first number and the index of the last number.

##### Notice

There is at least one subarray that it's sum equals to zero.

**Example**

Given `[-3, 1, 2, -3, 4]`, return `[0, 2]` or `[1, 3]`.



```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> subarraySum(int[] nums) {
        // write your code here
        
        List<Integer> res = new ArrayList<Integer>();
        
        if (nums == null || nums.length == 0) {
            return res;
        }
        
        int sum = 0;
        
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, -1); // -1 useful - in case sum == k !!! 
                         // (-1 + 1) ... i
        
        
        for (int i = 0; i < nums.length; i++) {
            
            sum += nums[i];
            
            if (map.containsKey(sum - 0)) {
                int index = map.get(sum - 0);
                
                // System.out.println(index + 1);
                // System.out.println(i);
                res.add(index + 1);
                res.add(i);
                return res;
            }
            
            if (!map.containsKey(sum)) {
                map.put(sum, i);
            }
            
        }
        
        return res;
    }
}
```

