**Overview**

* **Union Find**

  * implementation: **array** (similar to stack, queue)

  * APIs:

    * **Find 查找**: 查找两个结点是否在同一个集合
      * recursion < **iteration**
        * save memory
        * simple implementation

    ```java
    HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
    // O(n)
    int find(int x) {
        int parent = father.get(x);   
        while (parent != father.get(parent)) {
            parent = father.get(parent);
        }
        return parent;
    }
    ```

    * **Union 合并**: BIG FATHER 合并！！！！

    ```java
    HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
    // O(n)
    int union(int x, int y) {
        int fa_x = find(x);   
        int fa_y = find(y);
        if (fa_x != fa_y) {
    		father.put(fa_x, fa_y); // new connection pairs of two root nodes!!
            // father.put(fa_y, fa_x); ? should consider problem
        }
        return parent;
    }
    ```

  * 适合的题目

    * 集合合并 
    * 判断在不在同一个集合中
    * **判断是否有一个环**
    * 最大/小集合，集合个数，集合
    * [Find the Connected Component in the Undirected Graph](Find the Connected Component in the Undirected Graph.md)
    * [Find the Weak Connected Component in the Directed Graph (Follow up)](Find the Weak Connected Component in the Directed Graph.md)

  * **Optimization**

    * 查询 compressed_find
      * average running time: ${O(1)}$

    ```java
    int compressed_find(int x) {
        // find root node
    	int parent = father.get(x);
        while (parent != father.get(parent)) {
            parent = father.get(parent);
        }
        
        // 路径压缩
        int temp = -1;
        int fa = x;
        while (fa != father.get(fa)) {
        	temp = father.get(fa);
            father.put(fa, parent);
            fa = temp;
        }
        return parent;
    }
    ```

    * 合并 (roots合并)
      * use compressed_find
      * average running time: ${O(1)}$

  * 更多题目

    * [Number of Islands I, II](200. Number of Islands.md)
    * [Surrounded Regions](130. Surrounded Regions.md)
    * [Graph Valid Tree](Lint. Graph Valid Tree.md)：Check if a graph is a tree
    * [朋友圈](朋友圈.md)

* **Trie (前置树／查找树／字典树) - retrieve**

  * Properties
    * 虚根
    * 26叉树 (children nodes are initially null)
  * 类似题目
    * [Implement Trie](208. Implement Trie (Prefix Tree).md)
    * [Word Search II](212. Word Search II.md)
    * [Add and Search Word](211. Add and Search Word - Data structure design.md)
    * [设计算法获得IP到城市的MAP](设计算法获得IP到城市的MAP.md)
  * HashMap vs Trie
    * **Search** - n is length of a word
    * HashMap
      * Time: $O(1) - 1: string$,  $O(n) - n : characters (used to compute hash value)$
      * Space: 
    * Trie
      * Time: $O(1) - 1: string$,  $O(n) - n : characters$
      * Space: save memory
      * **WHEN TO USE TRIE**
        * 需要一个一个字符串遍历
        * 快速找到一个元素
        * 前缀(prefix)可以被压缩(重复)
        * 节约空间

* **Scan/Sweep Line - 区间拆分**  

  * 类似题目
    * [Number of Airplanes in the Sky (马甲1)](Number of Airplanes in the Sky.md)
    * A company holds several meetings. Given a list of start/end time of each meeting, ask for the # of meeting rooms. (马甲2)
    * Given a list of start/end time of each train xx, ask for the # of railways. (马甲3)
    * [Merge Intervals](Merge Intervals.md)
    * **other problems** which mix ScanLine & other data structure
  * **Define Point**: (xx, xx, ...)
  * **Priority**: Pick up the Point with some max/min


























































