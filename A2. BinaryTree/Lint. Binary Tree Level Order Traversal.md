##Binary Tree Level Order Traversal I

http://www.jiuzhang.com/solutions/binary-tree-level-order-traversal

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example: Given binary tree {3,9,20,#,#,15,7}, 3 / 
9 20 / 
15 7 return its level order traversal as: [ [3], [9,20], [15,7] ]



```java
// [!!!] version 1: BFS - 1 Queue (best) + for-loop
public class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List result = new ArrayList();

        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            // prep for for-stmt
            ArrayList<Integer> level = new ArrayList<Integer>();
            int size = queue.size(); // should do it first 
                                     // instead of in the loop 
                                     // avoid the issue of concurrency
            for (int i = 0; i < size; i++) {
                // handle this node from queue
                TreeNode head = queue.poll();
                level.add(head.val);
              
                // handle children of this node
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            result.add(level);
        }

        return result;
    }
}


// version 2:  DFS
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        
        if (root == null) {
            return results;
        }
        
        int maxLevel = 0;
        while (true) {
            List<Integer> level = new ArrayList<Integer>();
            dfs(root, level, 0, maxLevel);
            if (level.size() == 0) {
                break;
            }
            
            results.add(level);
            maxLevel++;
        }
        
        return results;
    }
    
    private void dfs(TreeNode root,
                     List<Integer> level,
                     int curtLevel,
                     int maxLevel) {
        if (root == null || curtLevel > maxLevel) {
            return;
        }
        
        if (curtLevel == maxLevel) {
            level.add(root.val);
            return;
        }
        
        dfs(root.left, level, curtLevel + 1, maxLevel);
        dfs(root.right, level, curtLevel + 1, maxLevel);
    }
}


// [!!!] version 3: BFS. two queues
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null) {
            return result;
        }
        
        List<TreeNode> Q1 = new ArrayList<TreeNode>();
        List<TreeNode> Q2 = new ArrayList<TreeNode>();

        Q1.add(root);
        while (Q1.size() != 0) {
            List<Integer> level = new ArrayList<Integer>();
            Q2.clear();
            for (int i = 0; i < Q1.size(); i++) {
                TreeNode node = Q1.get(i);
                level.add(node.val);
                if (node.left != null) {
                    Q2.add(node.left);
                }
                if (node.right != null) {
                    Q2.add(node.right);
                }
            }
            
            // swap q1 and q2
            List<TreeNode> temp = Q1;
            Q1 = Q2;
            Q2 = temp;
            
            // add to result
            result.add(level);
        }
        
        return result;
    }
}

// [!!!] version 4: BFS, queue with dummy node
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null) {
            return result;
        }
        
        Queue<TreeNode> Q = new LinkedList<TreeNode>();
        Q.offer(root);
        Q.offer(null); // dummy node
        
        List<Integer> level = new ArrayList<Integer>();
        while (!Q.isEmpty()) {
            TreeNode node = Q.poll();
            if (node == null) {
                if (level.size() == 0) {
                    break;
                }
                result.add(level);
                level = new ArrayList<Integer>();
                Q.offer(null); // add a new dummy node
                continue;
            }
            
            level.add(node.val);
            if (node.left != null) {
                Q.offer(node.left);
            }
            if (node.right != null) {
                Q.offer(node.right);
            }
        }
        
        return result;
    }
}
```



##Binary Tree Level Order Traversal II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example: Given binary tree {3,9,20,#,#,15,7}, 3 / 
9 20 / 
15 7 return its bottom-up level order traversal as: [ [15,7][9,20], [3], ]

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: buttom-up level order a list of lists of integer
     */
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            List<Integer> level = new ArrayList<>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                level.add(head.val);
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            result.add(level);
        }
        // top to bottom -> bottom to top
        Collections.reverse(result); // Collections.reverse(...) Please remember !!!
        /*
        for (int i = 0; i < results.size() / 2; i++) {
            List<Integer> temp = results.get(i);
            results.set(i, results.get(results.size() - 1 - i));
            results.set(results.size() - 1 - i, temp);
        }
        */
      
        return result;
    }
}
```

