###House Robber I

https://leetcode.com/problems/house-robber/description/

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.



**Method I**

1. 状态 state - f[i]  表示前i个房子中，偷到的最大价值
2. 方程 function - f[i] = max(f[i-1], f[i-2] + A[i])
3. 初始化 initialization - f[0] = 0, f[1] = A[0]
4. 答案 answer - f[n]

**空间优化** O(n) - > O(1)

* only need the previous two states - f[i%2] depends on f[(i-1)%2] and f[(i-2)%2]

```java
class Solution {
    public int rob(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] dp = new int[nums.length + 1];
        dp[0] = 0; // dummy
        dp[1] = nums[0];
        
        for (int i = 2; i < nums.length + 1; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i - 1]); //!! nums[i - 1]
        }
        
        return dp[nums.length];
    }
}
```

```java
class Solution {
    public int rob(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] res = new int[2];
        
        res[0] = 0; // even
        res[1] = nums[0]; // odd
        
        // 奇偶得奇，偶奇得偶，往前滚动
        for (int i = 2; i < nums.length + 1; i++) {
            res[i % 2] = Math.max(res[(i - 2) % 2] + nums[i - 1], //!! nums[i - 1]
                                  res[(i - 1) % 2]);
        }
        
        return res[nums.length % 2];
    }
}
```



**Method II**

1. 状态 state - f[i]  表示前i个房子中，**偷了第i个房子的**，偷到的最大价值
2. 方程 function - f[i] = max(f[i-2], f[i-3]) + A[i]
   1. f[i] depends on f[i-2] and f[i-3], since f[i-2] & f[i-3] are 两种互斥的情况，而前面的f都包含在这两种内
3. 初始化 initialization - f[0] = **A[0]**, f[1] = **A[1]**, f[2] = A[0] + **A[2]**
4. 答案 answer - max{f[i]} (or compare the last 2 f?)

**空间优化** O(n) - > O(1)

- only need the previous three states - f[i%3] depends on f[(i-2)%3] and f[(i-3)%3]
- 12 得 1, 23 得 2, 31 得 3

```java
class Solution {
    public int rob(int[] nums) {
        
        if (nums == null) {
            return 0;
        }
        
        int n = nums.length;
        
        int[] res = new int[3];
        int ans = 0;
        
        if (n == 0) {
            return 0;
        }
        
        if (n >= 1) {
            res[0] = nums[0];
            ans = Math.max(ans, res[0]);
        }
        
        if (n >= 2) {
            res[1] = nums[1];
            ans = Math.max(ans, res[1]);
        }
        
        if (n >= 3) {
            res[2] = nums[0] + nums[2];
            ans = Math.max(ans, res[2]);
            
            for (int i = 3; i < n; i++) {
                res[i % 3] = Math.max(res[(i - 2) % 3], res[(i - 3) % 3])
                            + nums[i];
                
                ans = Math.max(ans, res[i % 3]);
            }
        }
        
        return ans;
    }
}
```





###House Robber II

https://leetcode.com/problems/house-robber-ii/description/

**Note:** This is an extension of [House Robber](https://leetcode.com/problems/house-robber/).

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.



* **Method I**

```java
class Solution {
    public int rob(int[] nums) {
        
        // 1st & last elements cannot be picked all
        
        if (nums == null) { // null
            return 0;
        }
        
        int n = nums.length;
        
        if (n == 0) { // len 0
            return 0;
        }
        
        if (n == 1) { // len 1
            return nums[0];
        }
        
        return Math.max(robber1(nums, 0, nums.length - 2), //
                        robber1(nums, 1, nums.length - 1));
    }
    
    private int robber1(int[] nums, int start, int end) {
        int[] res = new int[2];
        
        // dont forget edge cases
        if (start == end) { // len = 1
            return nums[end];
        }
        
        //if (start + 1 == end) { // len = 2
            //return Math.max(nums[start], nums[end]);
        //}
        
        // unncessarily start with index 0
        // should depend on the actual index !!
        res[start % 2] = nums[start];
        res[(start + 1) % 2] = Math.max(nums[start], nums[start + 1]);
        
        for (int i = start + 2; i <= end; i++) {
            
            res[i % 2] = Math.max(res[(i - 2) % 2] + nums[i], //
                                  res[(i - 1) % 2]);
            
        }
        // actual index end
        return res[end % 2];
    }
}
```





###House Robber III

https://leetcode.com/problems/house-robber-iii/description/

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```
     3
    / \
   2   3
    \   \ 
     3   1

```

Maximum amount of money the thief can rob = 

3 + 3 + 1 = 7.

**Example 2:**

```
     3
    / \
   4   5
  / \   \ 
 1   3   1

```

Maximum amount of money the thief can rob = 

4 + 5 = 9.



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    // DP + DFS (divide & conquer)
    public int rob(TreeNode root) {
        int[] ans = dp(root);  // length is 2
        // Two states
        // ans[0] max when NOT pick root val
        // ans[1] max when pick root val
        return Math.max(ans[0], ans[1]); // compare at last
    }
    
    private int[] dp(TreeNode root) {
        if (root == null) {
            int[] now = new int[]{0, 0};
            return now;
        }
        
        // Divide
        int[] left = dp(root.left);
        int[] right = dp(root.right);
        
        
        // Conquer
        int[] now = new int[2]; // 2
        // !!! different from array
        // f[i] = Math.max(f[i - 2] + A[i], f[i - 1])
        // f[i - 1] itself is max as well (may not include A[i-1])
        // BUT HERE ---------------
        // left[1] & right[1] is just without val but not larger than left[0] always
        
        now[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]); // !!!!
        now[1] = left[0] + right[0] + root.val;
        
        return now;
    }
}
```

