## Recover Rotated Sorted Array

http://www.lintcode.com/en/problem/recover-rotated-sorted-array/

Given a rotated sorted array, recover it to sorted array in-place.

Example [4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]



Follow-up:

* in-place
* Time Complexity: ${O(n)}$ 
* Space Complexity: ${O(1)}$ 



The original array is [1,2,3,4]

The rotated array of it can be [1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]



**Method**:

* **三步翻转法**
  * e.g., 4 5 1 2 3
    1. [4 5], [1 2 3] - Just use iterative loop to find peak to split into 2 sub arrays
    2. [5 4], [3 2 1]
    3. [1 2 3 4 5]
  * **Time Complexity**: ${O(n)}$
  * **Space Complexity**: ${O(1)}$

```java
public class Solution {
    /**
     * @param nums: The rotated sorted array
     * @return: The recovered sorted array
     */
    public void recoverRotatedSortedArray(ArrayList<Integer> nums) {
        for (int index = 0; index < nums.size() - 1; index++) {
            if (nums.get(index) > nums.get(index + 1)) {
                reverse(nums, 0, index);
                reverse(nums, index + 1, nums.size() - 1);
                reverse(nums, 0, nums.size() - 1);
                return;
            }
        }
    }
  
    private void reverse(ArrayList<Integer> nums, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            int temp = nums.get(i);
            nums.set(i, nums.get(j));
            nums.set(j, temp);
        }
    }
}
```



