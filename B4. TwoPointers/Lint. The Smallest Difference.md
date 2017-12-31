## The Smallest Difference

http://www.lintcode.com/en/problem/the-smallest-difference/

Given two array of integers(the first array is array `A`, the second array is array `B`), now we are going to find a element in array A which is A[i], and another element in array B which is B[j], so that the difference between A[i] and B[j] (|A[i] - B[j]|) is as small as possible, return their smallest difference.

Have you met this question in a real interview?

 

Yes

Example

For example, given array A = `[3,6,7,4]`, B = `[2,8,9,3]`, return `0`

**Challenge**

O(*n* log *n*) time



```
求 |A[i] - B [j]|
```

 

```java
public class Solution {
    /**
     * @param A, B: Two integer arrays.
     * @return: Their smallest difference.
     */
    public int smallestDifference(int[] A, int[] B) {
        if (A == null || A.length == 0 || B == null || B.length == 0) {
            return 0;
        }
        
        Arrays.sort(A);
        Arrays.sort(B);
        
        int ai = 0, bi = 0;
        int min = Integer.MAX_VALUE;
        while (ai < A.length && bi < B.length) {
            // Math.abs(int) ONLY 1 parameter
            // Math.abs(A[ai] - B[bi])
            min = Math.min(min, Math.abs(A[ai] - B[bi]));
            if (A[ai] < B[bi]) {
                ai++;
            } else {
                bi++;
            }
        }
        return min;
    }
}
```

