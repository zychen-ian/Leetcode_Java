## Content - LinkedList

[Add Two Number I & II](./2. Add Two Numbers.md)



**Outline**

* Dummy Node in Linked List
* Basic skills in Linked List 
  * Insert a Node in Sorted List
  * Remove a Node from Linked List
  * Reverse  a Linked List
  * Merge Two Sorted List
  * Find the Middle of a Linked List
* Two Pointers

**Note**

* When accessing to X.next, ensure X is not null (NullPointerException)
* Delete a node
  * prev->curt->next: prev.next = prev.next.next;
  * curt->next: curt.val = next.val; curt.next = next.next;
* Use dummy node **when head node is not determinated** or **undetermined** 
  * make code concise & clean 
  * Problems:
    * Remove Duplicates from Sorted List II
    * Reverse Linked List II
    * Partition List
    * Merge Two Sorted Lists
* Avoid infinite loop on recursion
  * recursion(a, b, c): ensure that the problem represented by a, b, c, is **smaller**
    * Binary Tree: node.left, node.right
    * Linked List: 保证list size越来越小
    * Array: 保证数组越来越小
    * Permutation / Subsets: n个数的排列 -> n-1个数的排列
  * Recursion - algorithm:  让问题的规模经过同样的处理后，越来越小
  * Recursion - program: 函数的自我调用

 

[Remove Duplicates from Sorted List I & II](83. Remove Duplicates from Sorted List.md)

[Reverse Linked List I & II](206. Reverse Linked List.md)

[Partition List](86. Partition List.md)

* [Partition Array](Lint. Partition Array.md)

[Merge Two Sorted Lists](21. Merge Two Sorted Lists.md)



**Sort List**

* ${O(log_2 n)}$
  * MergeSort
    * FindMiddle
    * MergeSortedList
  * QuickSort
    * FindMiddel (value of mid used to partition list)
    * PartitionList



**Fast Slow Pointers (Two Pointers)**

1. Find the Middle of Linked List
2. [Remove Nth Node From End of List](19. Remove Nth Node From End of List.md)
3. [Linked List Cycle I, II](141. Linked List Cycle.md)



**Merge K Sorted List / Array**

* heap: **PriorityQueue** in Java

[Merge k Sorted Lists](23. Merge k Sorted Lists.md)

[Merge k Sorted Arrays](Lint. Merge k Sorted Arrays.md)



**Copy List with Random Pointer** / **Copy Graph**

* Deap Copy/Clone:   

[Copy List with Random Pointer](138. Copy List with Random Pointer.md)

[Clone Graph](133. Clone Graph.md)



**Convert Sorted List to Binary Search Tree**

* ​

[Convert Sorted List to Binary Search Tree](109. Convert Sorted List to Binary Search Tree.md)