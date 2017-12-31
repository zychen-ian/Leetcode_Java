## Content - Binary Tree

* Manipulations/Creation of Binary Tree
  * add/delete a node
* Divde & Conquer
* DFS/BFS Traversal


[144. Binary Tree Preorder Traversal](./144. Binary Tree Preorder Traversal.md)

[94. Binary Tree Inorder Traversal](94. Binary Tree Inorder Traversal.md)

[145. Binary Tree Postorder Traversal](145. Binary Tree Postorder Traversal.md)



[Lint. Partition Array I & II](./Lint. Partition Array.md) - Similar to **Parition List**

[104. Maximum Depth of Binary Tree](104. Maximum Depth of Binary Tree.md)

[111. Minimum Depth of Binary Tree](111. Minimum Depth of Binary Tree.md)

[124. Binary Tree Maximum Path Sum](124. Binary Tree Maximum Path Sum.md)

[543. Diameter of Binary Tree](543. Diameter of Binary Tree.md)

[PathSum](PathSum.md)

[257. Binary Tree Paths](257. Binary Tree Paths.md)

[236. Lowest Common Ancestor of a Binary Tree](236. Lowest Common Ancestor of a Binary Tree.md)

[662. Maximum Width of Binary Tree](662. Maximum Width of Binary Tree.md)

[623. Add One Row to Tree](623. Add One Row to Tree.md)

* Binary Tree DFS Traversal
  * preorder(根左右) / inorder(左根右) / postorder(左右根)
    * Non-recursive/Iterative - Stack
    * Recursive - Traversal 
    * Recursive - Divde & Conquer
    * **Note**: Normally, recursive approach. If you unfamiliar iwth iterative approach, dont ask interviewer whether I should write code in iterative approach or not.
  * **Divide & Conquer as template**  
    * Merge Sort
      * 先局部有序，再整体有序
      * space complexity: ${O(n + m)}$ - out-of-place
      * best/average/worst running time: ${O(nlog_2 n)}$
        * merge n/2 elem and n/2 elem: ${O(n)}$
        * height ${log_2 n}$: 1, 2, 4, 8, …. n count: ${log_2 n}$
        * T(n) = 2 * T(n/2) + O(n) ==> ${O(nlog_2 n)}$
      * 稳定性：稳定 when merging two sorted list/array, the elem in the 1st sorted list/array is on the 1st priority to pick up when two elements are equal, so that we maintain the relative order
        * For example, 2(id: 1), 1, 2(id: 2) —> 1, 2(id: 1), 2(id: 2)
    * **Quick** Sort
      * 先整体有序，再局部有序
      * space complexity: ${O(1)}$ - in-place
      * best/average running time: ${O(nlog_2 n)}$
      * worst running time: ${O(n^2)}$
      * 稳定性：不稳定 due to swap operations; It might not maintain the **relative order**
        * For example, 2(id: 1), 1, 2(id: 2) —> 1, 2(id: 2), 2(id: 1)
    * Most of the Binary Tree Problems !
  * Introduce DFS Template [link](http://www.jiuzhang.com/solutions/dfs-template)


```java
Template 1: Traverse

public class Solution {
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        // do something with root
        traverse(root.left);
        // do something with root
        traverse(root.right);
        // do something with root
    }
}


Tempate 2: Divide & Conquer

public class Solution {
    public ResultType traversal(TreeNode root) {
        // null or leaf
        if (root == null) {
            // do something and return;
        }
        
        // Divide
        ResultType left = traversal(root.left);
        ResultType right = traversal(root.right);
        
        // Conquer
        ResultType result = Merge from left and right.
        return result;
    }
}
```



* Binary Tree BFS Traversal

  [Binary Tree Level Order Traversal I & II](Lint. Binary Tree Level Order Traversal.md)

  [Binary Tree Zigzag Level Order Traversal](103. Binary Tree Zigzag Level Order Traversal.md)

  [515. Find Largest Value in Each Tree Row](515. Find Largest Value in Each Tree Row.md)

  [199. Binary Tree Right Side View](199. Binary Tree Right Side View.md)

  [Boundary of Binary Tree](Boundary of Binary Tree.md) - Left/Right Boundary is not defined as same as Left/Right Side View

  [116. Populating Next Right Pointers in Each Node](116. Populating Next Right Pointers in Each Node.md)

  [637. Average of Levels in Binary Tree](637. Average of Levels in Binary Tree.md)

  * Introduce BFS template
    * 2 Queues
      * QueueA: level 1, 3, 5...
      * QueueB: level 2, 4, 6...
      * Once a level is traversed, delete!
    * 1 Queue + dummy node 
      * dummy node is used as a middleware between two levels
        * A # BC # DE
    * 1 Queue (best)

* Binary Search Tree

  [Validate Binary Search Tree](98. Validate Binary Search Tree.md)


  [110. Balanced Binary Tree](110. Balanced Binary Tree.md)

  [100. Same Tree](100. Same Tree.md)

  [101. Symmetric Tree](101. Symmetric Tree.md)

  [226. Invert Binary Tree](226. Invert Binary Tree.md)

  [404. Sum of Left Leaves](404. Sum of Left Leaves.md)

  [563. Binary Tree Tilt](563. Binary Tree Tilt.md)

  [572. Subtree of Another Tree](572. Subtree of Another Tree.md)

  [508. Most Frequent Subtree Sum](508. Most Frequent Subtree Sum.md)

  [617. Merge Two Binary Trees](617. Merge Two Binary Trees.md)

  [129. Sum Root to Leaf Numbers](129. Sum Root to Leaf Numbers.md)

**Manipulation**

[Remove Node in Binary Search Tree](Lint. Remove Node in Binary Search Tree.md)












