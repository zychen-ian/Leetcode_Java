###Continuous Subarray Sum I

http://www.lintcode.com/en/problem/continuous-subarray-sum/#

Given an integer array, find a continuous subarray where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number. (If their are duplicate answer, return anyone)



**Example**

Give `[-3, 1, 3, -3, 4]`, return `[1,4]`.



```java
public class Solution {
    /*
     * @param A: An integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> continuousSubarraySum(int[] A) {
        // write your code here

        List<Integer> results = new ArrayList<Integer>();
        
        results.add(0);        
        results.add(0);

        if (A ==  null || A.length == 0) {
            return results;
        }
        
        // Greedy
        int max = Integer.MIN_VALUE;
        int sum = 0;
        
        int s = 0, start = 0, end = 0;
        
        for (int i = 0; i < A.length; i++) {
            // different from max/min subarray
            // check sum first
            if (sum < 0) {
                sum = A[i];
                start = end = i;
            } else {
                sum += A[i];
                end = i;
            }
            // check max later
            if (max < sum) {
                max = sum;
                results.set(0, start); // !! exists
                results.set(1, end); // !! exists
            }
        }

        return results;
    }
}
```





###Continuous Subarray Sum II

https://algorithm.yuanbin.me/zh-hans/problem_misc/continuous_subarray_sum_ii.html

https://lefttree.gitbooks.io/leetcode/highFreq/continuousSubarraySum2.html

Given an integer array, find a continuous rotate subarray where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number. (If their are duplicate answer, return anyone. The answer can be rorate array or non- rorate array)

**Example**

Give `[3, 1, -100, -3, 4]`, return `[4,1]`.







```java


```

