##Longest Increasing Subsequence (LIS)

https://leetcode.com/problems/longest-increasing-subsequence/description/

http://wikioi.com/problem/1576/ 



Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,
Given `[10, 9, 2, 5, 3, 7, 101, 18]`,
The longest increasing subsequence is `[2, 3, 7, 101]`, therefore the length is `4`. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?



* **State Function**
  * f[i]：代表前i个数的LIS - **不能做** 因为无法知道最后一个被选择的数是哪个 
  * f[i]：(代表前i个数，并且第i个数是LIS中最后一个数的) 最长LIS的长度
* ​

```java
// O(n^2) DP
public class Solution {
    /**
     * @param nums: The integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0; // tech commu
        }
      
        int f[] = new int[nums.length];
        int max = 0;
        for (int i = 0; i < nums.length; i++) { // start from 0
            f[i] = 1; // initialize 
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    f[i] = f[i] > f[j] + 1 ? f[i] : f[j] + 1;
                    // f[i] = Math.max(f[i], f[j] + 1); 
                }
            }
            // find maximum
            if (f[i] > max) {
                max = f[i];
            }
        }
        return max;
    }
}


// O(nlogn) Binary Search
public class Solution {
    /**
     * @param nums: The integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        int[] minLast = new int[nums.length + 1];
        minLast[0] = Integer.MIN_VALUE;
        for (int i = 1; i <= nums.length; i++) {
            minLast[i] = Integer.MAX_VALUE;
        }
        
        for (int i = 0; i < nums.length; i++) {
            // find the first number in minLast >= nums[i]
            int index = binarySearch(minLast, nums[i]);
            minLast[index] = nums[i];
        }
        
        for (int i = nums.length; i >= 1; i--) {
            if (minLast[i] != Integer.MAX_VALUE) {
                return i;
            }
        }
        
        return 0;
    }
    
    // find the first number > num
    private int binarySearch(int[] minLast, int num) {
        int start = 0, end = minLast.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (minLast[mid] < num) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        return end;
    }
}
```







