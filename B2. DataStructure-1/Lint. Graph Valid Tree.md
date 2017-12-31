##Graph Valid Tree

http://www.lintcode.com/en/problem/graph-valid-tree/

Given `n` nodes labeled from `0` to `n - 1` and a list of `undirected` edges (each edge is a pair of nodes), write a function to check whether these edges **make up a valid tree.**

**Notice**

You can assume that no duplicate edges will appear in edges. Since all edges are `undirected`, <u>`[0, 1]` is the same as `[1, 0]`</u> and thus will not appear together in edges.

**Example**

Given `n = 5` and `edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return true.

Given `n = 5` and `edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return false.



* **Undirected Graph**
  * BFS/DFS
  * Union-Find



```java
// version 1: BFS
public class Solution {
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        if (n == 0) {
            return false;
        }
        
        if (edges.length != n - 1) {
            return false;
        }
        
        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);
        
        // bfs
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> hash = new HashSet<>();
        
        queue.offer(0);
        hash.add(0);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (Integer neighbor : graph.get(node)) {
                if (hash.contains(neighbor)) {
                    continue;
                }
                hash.add(neighbor);
                queue.offer(neighbor);
            }
        }
        
        return (hash.size() == n);
    }
    
    private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }
        
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        return graph;
    }
}
```



```java
// version 2: Union Find
public class Solution {
      class UnionFind{ // nested class (no modifier or private)
        HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
        
        UnionFind(int n){ // (no modifier)
            for(int i = 0 ; i < n; i++) {
                father.put(i, i); 
            }
        }
        int compressed_find(int x){
            // get root node the set of x
            int parent =  father.get(x);
            while(parent!=father.get(parent)) {
                parent = father.get(parent);
            }
            
            // compress route
            int temp = -1;
            int fa = father.get(x);
          
            while(fa!=father.get(fa)) {
                temp = father.get(fa); // next node
                father.put(fa, parent); // compress route
                fa = temp; // continue on next node
            }
            return parent; // return parent!
                
        }
        
        void union(int x, int y){
            int fa_x = compressed_find(x);
            int fa_y = compressed_find(y);
            if(fa_x != fa_y)
                father.put(fa_x, fa_y);
        }
    }
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // @param n: the count of nodes
        // @param edges: a list of undirected edges
        // an edge: (edges[i][0], edges[i][1])
        // edges[i][0]: parent node 
        // edges[i][1]: child node
        // nodes are represented by numbers.
        
        // fiter out - edge cases
        // tree should have n nodes with n-1 edges -- "basic property"
        if (n - 1 != edges.length) {
            return false;
        }
        
        UnionFind uf = new UnionFind(n); // uf variable name
        
        for (int i = 0; i < edges.length; i++) {
            // determine if nodes x & y belong to the same tree
            if (uf.compressed_find(edges[i][0]) == uf.compressed_find(edges[i][1])) {
                // if there is a common root node of edges[i][0] and edge[i][1],
                // nodes edges[i][0] and edges[i][1] (already) belong to the same tree,
                // so the connection between these two nodes breaks the tree structure!
                // it is a GRAPH not a TREE, so we should return FALSE.
                // since there is a cycle/loop!! 
                return false; 
            }
            uf.union(edges[i][0], edges[i][1]); // within union implementation, find is called
        }
        return true;
    }
}
```



