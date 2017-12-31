###Maximum Subtree

**Description**
Given a binary tree, find the subtree with maximum sum. Return the root of the subtree.

**Notice**
LintCode will print the subtree which root is your return node.
It's guaranteed that there is only one subtree with maximum sum and the given binary tree is not an empty tree.


**Example**
Given a binary tree:

​       1
​     /   \
  -5      2
  / \    /  \
0   3 -4  -5
return the node with value 3.



```java
class TreeNode {
	public int val;
    public TreeNode left, right;
    public TreeNode(int val) {
        this.val = val;
    }
}

public class Solution {
    public int max_weight = Integer.MIN_VALUE; // NOT Always feasible !!!!!! See Below
    public TreeNode result = null;
  
    public TreeNode findSubtree(TreeNode root) {
     	helper(root);
        return target;
    }
  
    public int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }
      
     	//if (root.left == null && root.right == null) {
        //    return root.val;
        //}
      
        // Divide
		int left = helper(root.left);
        int right = helper(root.right);
        // Conquer
        int sum = left + right + root.val;
        
        // update global var
        if (result == null || max_weight < sum) { // result == null -> one root with val Integer.MIN_VALUE !!!!!!!!!!!!
            max_weight = sum;
            result = root;
        }
        
        return sum;
    }
}
```

