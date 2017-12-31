##Longest Common Subsequence

http://www.lintcode.com/en/problem/longest-common-subsequence/



Given two strings, find the **longest** comment subsequence (LCS).

Your code should return the **length** of LCS.

Example For "ABCD" and "EDCA", t he LCS is "A" (or D or C), return 1

For "ABCD" and "EACB", the LCS is "AC", return 2



```java
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {
        if (A == null || B == null) {
            return -1; // tech commu
        }
      
        int n = A.length();
	    int m = B.length();
        int f[][] = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){ // NOT j<=i due to 2SequenceDP NOT SequenceDP
                if(A.charAt(i - 1) == B.charAt(j - 1)) { // easily get error: (i - 1) !!
                    f[i][j] = f[i - 1][j - 1] + 1;
                } else {
                    f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
                }
            }
        }
        return f[n][m];
    }
}
```

