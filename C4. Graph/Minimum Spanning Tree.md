###Minimum Spanning Tree

题目内容是这样的，给十几个城市供电，连接不同城市的花费不同，让花费最小同时连到所有的边。给出一系列connection类，里面是edge两端的城市名和它们之间的一个cost，找出要你挑一些边，把所有城市连接起来并且总花费最小。不能有环，最后所以城市要连成一个连通块。

不能的话输出空表，最后还要按城市名字排序输出，按照node1来排序,如果一样的话再排node2。

输入:

{"Acity","Bcity",1}

("Acity","Ccity",2}

("Bcity","Ccity",3}

输出：

("Acity","Bcity",1}

("Acity","Ccity",2}

补充一句，test case一共有6个。

思路会有很多，我的想法是Kruskal+Union Find，将输入的一群connection类（其实就是边）按照cost从小到大排序(Kruskal算法)，然后遍历。挑出一个connection之后，看一下edge两头的城市属于哪一个团伙(Union Find)。如果落单了就加入，不同团伙就合并，都是落单了就抱团。最后有两个要求，1.如果MST不存在，那么输出一个空表（应该不是null）。这个可以用union find思想，最后查有几个union，如果大家都是自己人，那么就正常输出，如果大家是1，有零星2了，那就空表了。2.输出要按照城市的名字排序，这个不难，就正常排序就行。







####Method

```java
1. input: List<Connection> 
   output: List<Connection> minimum spanning tree
   // min spanning tree: 
   //  * num of edges = num of nodes - 1
   //  * no loop
   //  * every node is connected
   //  * min sum of weight 
2. sort connections by cost increasingly
   if weight same, sort connections by city names (city1 first city2 second) in the alphabetical order
3. traverse every connections, if two cities are not connected, connect them, add this connection to result. 
4. check result. if num of picked connection != n - 1, return new ArrayList<>(), else return result

* Use father array as union-find data structure for connecting cities (union) or checking if two cities are connected (find)
```



```java
/**
 * Definition for a Connection.
 * public class Connection {
 *   public String city1, city2;
 *   public int cost;
 *   public Connection(String city1, String city2, int cost) {
 *       this.city1 = city1;
 *       this.city2 = city2;
 *       this.cost = cost;
 *   }
 * }
 */
public class Solution {
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
    public List<Connection> lowestCost(List<Connection> connections) {

        Collections.sort(connections, comp);
        Map<String, Integer> hash = new HashMap<String, Integer>();
        int n = 0;
        for (Connection connection : connections) {
            if (!hash.containsKey(connection.city1)) {
                hash.put(connection.city1, ++n);
            }
            if (!hash.containsKey(connection.city2)) {
                hash.put(connection.city2, ++n);
            }
        }
		// initialize father array
        int[] father = new int[n + 1]; // !!! n + 1

        List<Connection> results = new ArrayList<Connection>();
        for (Connection connection : connections) {
            int num1 = hash.get(connection.city1);
            int num2 = hash.get(connection.city2);

            int root1 = find(num1, father);
            int root2 = find(num2, father);
            if (root1 != root2) {
                // quick_union
                father[root1] = root2;
                results.add(connection);
            }
        }

        if (results.size() != n - 1)
            return new ArrayList<Connection>();
        return results;
    }

    static Comparator<Connection> comp = new Comparator<Connection>() {
        public int compare(Connection a, Connection b) {
            if (a.cost != b.cost)
                return a.cost - b.cost;
            if (a.city1.equals(b.city1)) {
                return a.city2.compareTo(b.city2);
            }
            return a.city1.compareTo(b.city1);
        }
    };
    // compressed_find (find + compress route)
    public int find(int num, int[] father) {
        if (father[num] == 0)
            return num;

        return father[num] = find(father[num], father);
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
    int n = 0;

    public List<Connection> lowestCost(List<Connection> connections) {
        // Write your code here
        List<Connection> ans = new ArrayList<>();
        UFS ufs = new UFS(connections.size() * 2);

        Collections.sort(connections, new Comparator<Connection>() {
            public int compare(Connection a, Connection b) {
                if (a.cost != b.cost) {
                    return a.cost - b.cost;
                }
                if (a.city1.equals(b.city1)) {
                    return a.city2.compareTo(b.city2);
                }
                return a.city1.compareTo(b.city1);
            }
        });

        for (Connection item : connections) {
            int c1 = getID(item.city1);
            int c2 = getID(item.city2);
            if (ufs.find(c1) != ufs.find(c2)) {
                ans.add(item);
                ufs.union(c1, c2);
            }
        }
        if (ans.size() == n - 1) {
            return ans;
        } else {
            return new ArrayList<>();
        }
    }


    Map<String, Integer> name2ID = new HashMap<>();

    public int getID(String name) {
        if (name2ID.containsKey(name)) {
            return name2ID.get(name);
        } else {
            name2ID.put(name, n++);
            return n - 1;
        }
    }

    public class UFS {
        int[] f;          // father

        public UFS(int n) {
            f = new int[n];
            for (int i = 0; i < n; i++) {
                f[i] = -1;
            }
        }

        public void union(int a, int b) {
            a = find(a);
            b = find(b);
            if (f[a] < f[b]) {
                f[a] += f[b];
                f[b] = a;
            } else {
                f[b] += f[a];
                f[a] = b;
            }
        }

        public int find(int x) {
            if (f[x] < 0) {
                return x;
            }
            f[x] = find(f[x]);
            return f[x];
        }
    }
}
```

