###Maximum Subarray Difference

http://www.lintcode.com/en/problem/maximum-subarray-difference/#

Given an array with integers.

Find two *non-overlapping*subarrays *A* and *B*, which `|SUM(A) - SUM(B)|`is the largest.

Return the largest difference.



```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two substrings
     */
    public int maxDiffSubArrays(int[] nums) {
        // write your code here
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        
        int[] leftMax = new int[nums.length];
        int[] leftMin = new int[nums.length];

        int[] rightMax = new int[nums.length];
        int[] rightMin = new int[nums.length];
        
        
        int sum = 0;
        int minSum = 0;
        int maxSum = 0;
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            
            max = Math.max(max, sum - minSum);
            min = Math.min(min, sum - maxSum);
            
            minSum = Math.min(minSum, sum);
            maxSum = Math.max(maxSum, sum);
            
            leftMax[i] = max;
            leftMin[i] = min;
            System.out.println("left max " + max);
            System.out.println("left min " + min);
        }
        
        sum = 0;
        minSum = 0;
        maxSum = 0;
        max = Integer.MIN_VALUE;
        min = Integer.MAX_VALUE;
        
        for (int i = nums.length - 1; i >= 0; i--) {
            sum += nums[i];
            
            max = Math.max(max, sum - minSum);
            min = Math.min(min, sum - maxSum);
            
            minSum = Math.min(minSum, sum);
            maxSum = Math.max(maxSum, sum);
            
            rightMax[i] = max;
            rightMin[i] = min;
            
            System.out.println("right max " + max);
            System.out.println("right min " + min);
        }
        
        int diff = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            diff = Math.max(diff, Math.abs(leftMax[i] - rightMin[i + 1]));
            diff = Math.max(diff, Math.abs(leftMin[i] - rightMax[i + 1]));

        }
        
        return diff;
        
    }
}
```

