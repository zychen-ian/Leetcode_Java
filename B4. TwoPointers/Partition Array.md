###Partition Array

http://www.lintcode.com/en/problem/partition-array/#

Given an array `nums` of integers and an int `k`, partition the array (i.e move the elements in "nums") such that:

- All elements < *k* are moved to the *left*
- All elements >= *k* are moved to the *right*

Return the partitioning index, i.e the first index *i* nums[*i*] >= *k*.



If nums = `[3,2,2,1]`and `k=2`, a valid answer is `1`.



```java
public class Solution {
    /*
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        // write your code here
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            
            while (left < nums.length && nums[left] < k) {
                left++;
            }
            
            while (right >= 0 && nums[right] >= k) {
                right--;
            }
            
            if (left < right) {
                // swap
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
            }
        }
        
        return left; // NOT right!!
                   // Return the partitioning index, i.e the first index i nums[i] >= k.
    }
}
```

