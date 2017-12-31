###Convert Sorted List to Binary Search Tree

https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/description/

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.



* Sorted List to BST
* BST is height balanced.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    private ListNode current;
    
    public TreeNode sortedListToBST(ListNode head) {
        int size;
        
        current = head;
        size = getListLength(head);
        
        return sortedListToBSTHelper(size);
    }
    
    private int getListLength(ListNode head) {
        int size = 0;
        
        while (head != null) {
            head = head.next;
            size++;
        }
        
        return size;
    }
    
    private TreeNode sortedListToBSTHelper(int size) {
        /*
         * Must use inorder traversal, since inorder traversal
         * performed on BST produces a sorted list
         */ 
        
        if (size <= 0) {
            return null;
        }
        
        TreeNode left = sortedListToBSTHelper(size / 2);
        TreeNode root = new TreeNode(current.val);
        current = current.next;
        TreeNode right = sortedListToBSTHelper(size - 1 - size / 2);
        
        root.left = left;
        root.right = right;
        
        return root;
    }
}
```





###Convert Sorted Array to Binary Search Tree

https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.



* Sorted Array to BST
* BST is height balanced

```java


```





###Covert Array/List to Binary Search Tree



* Array/List to BST
* NOT considering if it's height balanced

```java
public class BST {
    class TreeNode {
      int val;
       TreeNode left;
       TreeNode right;
       TreeNode(int x) { val = x; }
    }
  
	public TreeNode root;

	public BST(int[] values) {
		createBST(values);
	}
	
	public void createBST(int[] values) {
		for (int i = 0; i < values.length; i++) {
			addFromRoot(values[i]);
		}
	}

	public void addFromRoot(int value) {
		root = (root == null) ? new TreeNode(value) : addNode(root, value);
	}

    // Divide & Conquer
	public TreeNode addNode(TreeNode root, int value) {
		if (root == null) {
			return new TreeNode(value);
		}

		if (value < root.val) {
			TreeNode left = addNode(root.left, value);
			root.left = left;
		} else {
			TreeNode right = addNode(root.right, value);
			root.right = right;
		}

		return root;
	}
	
	public void display(TreeNode root) {
		if (root == null) {
			System.out.println(" null ");
			return;
		}

		// preorder - traversal
		System.out.println(" " + root.val + " ");
		
		display(root.left);
		display(root.right);
	} 

	public static void main(String args[]) {
		int values[] = { 5, 6, 3, 1, 2, 4 };
		BST s = new BST(values);
		s.display(s.root);
	}
}
```

