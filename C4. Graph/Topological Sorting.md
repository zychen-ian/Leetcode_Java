###Topological Sorting

http://www.lintcode.com/en/problem/topological-sorting/#

Given an directed graph, a topological order of the graph nodes is defined as follow:

- For each directed edge `A -> B` in graph, A must before B in the order list.
- The first node in the order can be any node in the graph with no nodes direct to it.

Find any topological order for the given graph.



* Find nodes without any ancestors and add them to result list
* Remove those nodes without any ancestors (one by one) and their connections with other nodes
* Then get more nodes without any ancestors and append them to result list
* Repeat the above steps until there is no nodes in the graph

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
    /*
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        
        // 对于每条有向边A--> B，则A必须排在B之前　　
        // 拓扑排序的第一个节点可以是任何在图中没有其他节点指向它的节点
        
        ArrayList<DirectedGraphNode> res = new ArrayList<>();
        
        // Pair: node ~ count of parent nodes
        HashMap<DirectedGraphNode, Integer> map = new HashMap<>();
        
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (map.containsKey(neighbor)) {
                    map.put(neighbor, map.get(neighbor) + 1);     
                } else {
                    map.put(neighbor, 1);
                }
            }
        }
        
        // queue only storing starting node (no parent/ancestor nodes)
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        for (DirectedGraphNode node : graph) {
            if (!map.containsKey(node)) {
                q.offer(node); // starting nodes
                
                res.add(node); // nodes with no parent 
            }
        }
        
        // queue only storing starting node (no parent/ancestor nodes)
        while (!q.isEmpty()) {
            DirectedGraphNode node = q.poll(); // deleted node
          
            for (DirectedGraphNode n : node.neighbors) {
                
                map.put(n, map.get(n) - 1); // remove connection
                
                if (map.get(n) == 0) {
                    q.offer(n); // new starting nodes
                    res.add(n); // nodes with no parent
                }
            }
        }
        
        return res;
    }
}
```





