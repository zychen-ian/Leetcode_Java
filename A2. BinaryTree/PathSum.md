### Path Sum



###Path Sum I

https://leetcode.com/problems/path-sum/description/

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:

Given the below binary tree and 

```
sum = 22
```



```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.





**Solution**:

* Traversal - Pre-order 

* Recursion

* if root is null -> false

* if root is left -> see if sum == root.val

* otherwise

  * start recursion on left child, and notice the sum is changed
  * start recursion on right child, and notice the sum is changed

  ​

```java
class Solution {
    
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }
        
        return hasPathSum(root.left, sum - root.val)
            || hasPathSum(root.right, sum - root.val);
    }

}
```







###Path Sum II

https://leetcode.com/problems/path-sum-ii/description/

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

 

```
sum = 22
```

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

```

return

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```



**Solution**:

* **Backtracking/Traversal**
  * Similar to Permutatioin/Subsets
  * Similar to Path Sum I
* ​

```java
public class Solution {
    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        ArrayList<ArrayList<Integer>> rst = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> solution = new ArrayList<Integer>();

        findSum(rst, solution, root, sum);
        return rst;
    }

    private void findSum(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> solution, TreeNode root, int sum){
        if (root == null) {
            return;
        }

        sum -= root.val;

        if (root.left == null && root.right == null) {
            if (sum == 0){
                solution.add(root.val);
                result.add(new ArrayList<Integer>(solution)); // easy to make mistake
                solution.remove(solution.size()-1); // easy to make mistake
            }
            return; // easy to make mistake
        }

        solution.add(root.val);
        findSum(result, solution, root.left, sum);
        findSum(result, solution, root.right, sum);
        solution.remove(solution.size()-1); // easy to make mistake
    }
}

```





###Path Sum III - count

https://leetcode.com/problems/path-sum-iii/description/

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must **go downwards** (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```





**Solution**:

* **Backtracing & Traversal**
  * similar to Path Sum II & Path Sum I

```java
class Solution {
    public int pathSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
            
        return pathSumFrom(root, sum) 
            + pathSum(root.left, sum)
            + pathSum(root.right, sum);
    }
    
    private int pathSumFrom(TreeNode node, int sum) {
        
        if (node == null) {
            return 0;
        }
        
        return (node.val == sum ? 1 : 0) 
            + pathSumFrom(node.left, sum - node.val) 
            + pathSumFrom(node.right, sum - node.val);
    }
}


```





###Path Sum III - all paths

https://yeqiuquan.blogspot.com/2017/04/lintcode-472-binary-tree-path-sum-iii.html

Give a binary tree, and a target number, find all path that the sum of nodes equal to target, the **path could be start and end at any node** in the tree.



**Example**
Given binary tree:

    1
   / \
  2   3
 /
4
and target = 6. Return :

[
  [2, 4],
  [2, 1, 3],
  [3, 1, 2],
  [4, 2]
]



**思路**
现在的题意是可以从任何一点出发，而且有parent节点。
那么我们其实是traverse一遍这棵树，在每一点，我们出发找有没有符合条件的路径。
在每一点我们可以有三个方向：左边，右边，和上面。但是我们**需要避免回头，所以需要一个from节点的参数**。

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public int val;
 *     public ParentTreeNode parent, left, right;
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @param target an integer
     * @return all valid paths
     */
    public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
        // Write your code here
        
        List<List<Integer>> result = new ArrayList<>();
        helper(root, result, target);
        return result;
    }
    
    public void helper(ParentTreeNode root, List<List<Integer>> result, int target) {
        
        if (root == null) {
            return;
        }
        
        List<Integer> path = new ArrayList<>();
        findSum(root, null, result, path, target);
        
        helper(root.left, result, target);
        helper(root.right, result, target);
    }
    
    public void findSum(ParentTreeNode root, 
                        ParentTreeNode from, // intermediate "from" 
                        List<List<Integer>> result, 
                        List<Integer> path, 
                        int target) {
        
        if (root == null) {
            return;
        }
        
        path.add(root.val);
        target -= root.val;
        
        if (target == 0) {
            result.add(new ArrayList<>(path));
        }
        
        // for example, function call -  findSum(root, null, result, path, target);
        // root is a real root of this tree
        // the parent direction is not allowed to go 
        if (root.parent != null && root.parent != from) {
            findSum(root.parent, root, result, path, target);
        }
        
        if (root.left != null && root.left != from) {
            findSum(root.left, root, result, path, target);
        }
        
        if (root.right != null && root.right != from) {
            findSum(root.right, root, result, path, target);
        }
        
        path.remove(path.size() - 1);
    }
}
```





