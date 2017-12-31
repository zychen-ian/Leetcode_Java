## Content - Binary Search & Sorted Array

[34. Search for a Range](./34. Search for a Range.md)

[35. Search Insert Position](./35. Search Insert Position.md)

[!! 33. Search Rotated Sorted Array I & II](./33. Search Rotated Sorted Array.md)

[!! 153. Find Minimum in Rotated Sorted Array I & II](./153. Find Minimum in Rotated Sorted Array.md)

[74. Search a 2D Matrix I & II](./74. Search a 2D Matrix.md)

[278. First Bad Version](./278. First Bad Version.md)

[162. Find Peak Element](./162. Find Peak Element.md)

[69. Sqrt(x)](69. Sqrt(x).md)

**When to use Binary Search**

* first / last position
* O(n)  -optimize->  O(logn)



**Classical Binary Search**

Given an sorted integer array - nums, and an integer - target. Find the **any/first/last** position of target in nums, return -1 if target doesn’t exist.



工程项目中一般避免写递归程序，因存在stack overflow的exception的可能性

Recursion: simple
While-loop: save memory resources

```java
class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int start = 0;
        int end = nums.length - 1;
        int mid;
  
        // loop stops when start and end are adjacent or equal.
        while (start + 1 < end) { // avoid infinite loop
            mid = start + (end - start) / 2; // avoid overflow when (end + start)
            if (target < nums[mid]) {
                end = mid;
            } else if (target > nums[mid]) {
                start = mid;
            } else {
                // find first position (leftmost), so that end should move leftside,
                // get close to start
                end = mid; 
                // if find last position (rightmost), start = mid;
            }
        }
        
        // MUST CHANGE IF REQUIREMENT CHANGE (LIKE, FIRST - > LAST)
        // find first position so look up start first!
        if (nums[start] == target) {
            return start;
        }
        // if find last position should look up end first!
        if (nums[end] == target) {
            return end;
        }

        return -1;
    }
}
```

1. e.g., start = 1, end = 2 => mid = 1 => start = mid = 1 => ….

```java
	while (start + 1 < end) { // avoid infinite loop
```

​			

**Sorted Array**

[26. Remove Duplicates from Sorted Array I & II](./26. Remove Duplicates from Sorted Array.md)

[88. Merge Sorted Array](./88. Merge Sorted Array.md)



##**三步翻转法**

实用题目：

* [Recover Rotated Sorted Array](Lint. Recover Rotated Sorted Array.md)
* [Rotate String](Lint. Rotate String.md)
* [Rotate Array](189. Rotate Array.md) 
  * [Rotate List](../LinkedList/61. Rotate List.md)
* [Reverse Words in a String I & II](151. Reverse Words in a String.md)

***

* Reverse in Array/String
  * Time: O(n)
  * Space: O(1)
* Reverse in LinkedList
  * Time: O(n)
  * Space: O(1)



[153. Find Minimum in Rotated Sorted Array.md]: 