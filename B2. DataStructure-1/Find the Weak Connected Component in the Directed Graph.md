##Find the Weak Connected Component in the Directed Graph

Find the number Weak Connected Component in the directed graph. Each node in the graph contains a label and a list of its neighbors. (a connected set of a directed graph is a subgraph in which any two vertices are connected by direct edge path.)



**Notice**

**Sort the element in the set in increasing order**

**Example**

Given graph:

```
A----->B  C
 \     |  | 
  \    |  |
   \   |  |
    \  v  v
     ->D  E <- F

```

Return {A,B,D}, {C,E,F}. Since there are two connected component which are {A,B,D} and {C,E,F}



* **Weak Connected Component** (Different from **Strong Connected Component**)
  * Do not consider direction of arrows (just like connected componenet in undirected graph)
* Strong Connected Componenet
  * Another algorithm - Not Required in Coding Interview

**Data Structure**

* Union-Find



```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param nodes a array of Directed graph node
     * @return a connected set of a directed graph
     */
    class UnionFind{
        HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
        public UnionFind(ArrayList<Integer> array){
            for(int i : array){
                father.put(i, i);
            }
        }

        public int compressed_find(int x){
            int parent = father.get(x);
            while(parent != father.get(parent)){
                parent = father.get(parent);
            }

            int temp = 0;
            int fa = x;
            while(fa != father.get(fa)){
                temp = father.get(fa);
                father.put(fa, parent);
                fa = temp;
            }

            return parent;
        }

        public void union(int a, int b){
            int aFather = compressed_find(a);
            int bFather = compressed_find(b);
            if(aFather != bFather){
                father.put(aFather, bFather);
            }
        }
    }
    public List<List<Integer>> connectedSet2(ArrayList<DirectedGraphNode> nodes) {
        // Write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        ArrayList<Integer> array = new ArrayList<Integer>();
        for(DirectedGraphNode dgn : nodes){
            if(!array.contains(dgn.label)){
                array.add(dgn.label);
            }
            for(DirectedGraphNode neighbor : dgn.neighbors){
                if(!array.contains(neighbor.label)){
                    array.add(neighbor.label);
                }
            }
        }

        UnionFind uf = new UnionFind(array);

        for(DirectedGraphNode dgn : nodes){
            for(DirectedGraphNode neighbor : dgn.neighbors){
                uf.union(dgn.label, neighbor.label);
            }
        }

        HashSet<Integer> set = new HashSet<Integer>();
        for(int i = 0; i < nodes.size(); i++){
            if(set.contains(uf.compressed_find(nodes.get(i).label))){
                continue;
            }

            set.add(uf.compressed_find(nodes.get(i).label));

            List<Integer> list = new ArrayList<Integer>();
            list.add(nodes.get(i).label);
            for(int j = i + 1; j < nodes.size(); j++){
                if(uf.compressed_find(nodes.get(j).label) == uf.compressed_find(nodes.get(i).label)){
                    list.add(nodes.get(j).label);
                }
            }
            result.add(list);
        }

        return result;
    }
}
```

























