##Triangle Count

https://aaronice.gitbooks.io/lintcode/content/two_pointers/triangle_count.html

Given an array of integers, **how many three numbers** can be found in the array, so that we can build an triangle whose three edges length is the three numbers that we find?

Example

Given array S = [3,4,6,7], return 3. They are:

```
[3,4,6]
[3,6,7]
[4,6,7]

```

Given array S = [4,4,4,4], return 4. They are:

```
[4(1),4(2),4(3)]
[4(1),4(2),4(4)]
[4(1),4(3),4(4)]
[4(2),4(3),4(4)]
```



**Method**

* **Brute Force** - 3 nested loops

```java
// ensure that every tuple (i, j, k) is distinct and NOT duplicated
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
    	for (int k = 0; k < j; k++) {
            // 3 requirements
            // A[i] + A[j] > A[k]
            // A[j] + A[k] > A[i]
            // A[k] + A[i] > A[j]
        } 
    }
}
```



* Sort -> A[k]<A[j]<A[i] based on the above 3 nested loops
  * A[i] + A[j] > A[k] **satisfied**
  * A[i] + A[k] > A[j] **satisfied**
  * A[k] + A[j] > A[i] **?**
* Sort
* Loop: ${O(n)}$
  * Two Pointers: ${O(n)}$
* Time: ${O(nlog_2n + n^2)}$

```java
for (int i = 0; i < n; i++) {
    int target = A[i];
    // A[k] + A[j] > A[i] similar to 2SUM2 (Lint.)
    // 2Sum2 performed on array A[0..i-1]
}

```



* Nine Chapter

```java
public class Solution{
  public int triangleCount(int[] nums) {
      Arrays.sort(nums);
      int ans = 0, left, right;
      for (int i = 0; i < nums.length; i++) {
		  left = 0;
          right = i - 1;
          while (left < right) {
              if (nums[left] + nums[right] > nums[i]) {
                  ans += right - left;
                  right--;
              } else {
                  left++;
              }
          }
      }
      return ans;
  }
}
```





##Valid Triangle Number

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

**Example 1:**

```
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3

```

**Note:**

1. The length of the given array won't exceed 1000.
2. The integers in the given array are in the range of [0, 1000].













