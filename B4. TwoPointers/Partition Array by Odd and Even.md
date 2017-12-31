###Partition Array by Odd and Even

Partition an integers array into odd number first and even number second.



Example

Given `[1, 2, 3, 4]`, return `[1, 3, 2, 4]`

**Challenge**

Do it in-place.



* Partition (对撞型指针)

```java
public class Solution {
    /*
     * @param nums: an array of integers
     * @return: nothing
     */
    public void partitionArray(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return;
        }
        
        int start = 0, end = nums.length - 1;
        
        // two pointer
        while (start < end) {
            
            while (start < end && nums[start] % 2 == 1) {
                start++;
            }
            
            while (start < end && nums[end] % 2 == 0) {
                end--;
            }
            
            if (start < end) {
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                
                start++;
                end--;
            }
        }
        
    }
}
```

