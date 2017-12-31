###Boundary of Binary Tree

http://www.cnblogs.com/grandyang/p/6833459.html

Given a binary tree, return the values of its boundary inanti-clockwise directionstarting from root. Boundary includes left boundary, leaves, and right boundary inorder without duplicate nodes.

**Left boundary** is defined as the path from root to the left-most node. **Right boundary** is defined as the path from root to theright-most node. **If the root doesn't have left subtree or right subtree, then the root itself is left boundary or rightboundary.** Note this definition only applies to the input binary tree, and not appliesto any subtrees.

The left-most node is defined as a leaf node you could reach when you always firstly travel to the left subtree if exists. If not, travel to the right subtree. Repeatuntil you reach a leaf node.

The right-most node is also defined by the same way with left and right exchanged.

Example 1

```
Input:
  1
   \
    2
   / \
  3   4

Ouput:
[1, 3, 4, 2]

Explanation:
The root doesn't have left subtree, so the root itself is left boundary.
The leaves are node 3 and 4.
The right boundary are node 1,2,4. Note the anti-clockwise direction means you should output reversed right boundary.
So order them in anti-clockwise without duplicates and we have [1,3,4,2].
```

 

Example 2

```
Input:
    ____1_____
   /          \
  2            3
 / \          / 
4   5        6   
   / \      / \
  7   8    9  10  
       
Ouput:
[1,2,4,7,8,9,10,6,3]

Explanation:
The left boundary are node 1,2,4. (4 is the left-most node according to definition)
The leaves are node 4,7,8,9,10.
The right boundary are node 1,3,6,10. (10 is the right-most node).
So order them in anti-clockwise without duplicate nodes we have [1,2,4,7,8,9,10,6,3].
```



```java
  List<Integer> nodes = new ArrayList<Integer>();

  public List<Integer> boundaryOfBinaryTree(TreeNode root) {
      if (root == null) return nodes;

      node.add(root.val);

      leftBoundary(root.left);

      leaves(root.left);
      leaves(root.right);

      rightBoundary(root.right);

      return nodes;
  }
  
  public void leftBoundary(TreeNode root) {
      // null or leaf
      if (root == null || 
           (root.left == null && root.right == null)) {
          return;
      }
    
      nodes.add(root.val);
    
      if (root.left == null) {
          leftBoundary(root.right);
      } else {
          leftBoundary(root.left);
      }
  }

  public void rightBoundary(TreeNode root) {
      // null or leaf
      if (root == null || 
           (root.left == null && root.right == null)) {
          return;
      }
    
      if (root.right == null) {
          leftBoundary(root.left);
      } else {
          leftBoundary(root.right);
      }
    
      nodes.add(root.val);
  }

  public void leaves(TreeNode root) {
      if (root == null) {
          return;
      }
    
      if (root.left == null && root.right == null) {
          nodes.add(root.val);
          return;
      }
    
      leaves(root.left);
      leaves(root.right);
  }
```



























