###Course Scheduler

http://www.lintcode.com/en/problem/course-schedule/#

https://leetcode.com/problems/course-schedule/description/



There are a total of *n* courses you have to take, labeled from `0` to `n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

```
2, [[1,0],[0,1]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

[click to show more hints.](https://leetcode.com/problems/course-schedule/description/#)

Hints:

1. This problem is **equivalent to finding if a cycle exists in a directed graph**. <u>If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.</u>
2. [Topological Sort via DFS](https://class.coursera.org/algo-003/lecture/52) - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
3. Topological sort could also be done via [BFS](https://en.wikipedia.org/wiki/Topological_sorting#Algorithms).



**Method:**

```java
1. Construct data structure if necessary (see input)
   degree: in-degree, count of parent nodes (as HashMap in Topological sort)
   edges: neighbors, out-degree nodes (as input in Topological sort)
2. Add to queue those nodes who do not have a parent
3. process each node in the queue, count++, update the in-degree of its neighbor/children nodes (since this node is processed and deleted from the graph)
4. if the in-degree of neighbor nodes == 0, add it to queue
5. check if count == numCourses
```



```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // [0, 1] Take 0 you have to take 1 first
        // 1 -> 0
        
        List[] edges = new ArrayList[numCourses]; // neighbor, out-degree node
        // same as data structure used in topological sort
        
        int[] degree = new int[numCourses]; // in-degree
        // if in-degree = 0, no parent nodes
        
        // initialize edges
        for (int i = 0; i < numCourses; i++) {
            edges[i] = new ArrayList<Integer>();
        }
        
        // construct degree & edges
        for (int i = 0; i < prerequisites.length; i++) {
            degree[prerequisites[i][0]]++; 
            edges[prerequisites[i][1]].add(prerequisites[i][0]);
        }
        
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (degree[i] == 0) {
                q.offer(i);
            }
        }
        
        
        int count = 0;
        while (!q.isEmpty()) {
            int course = q.poll(); 
            count++;
            
            // remove connection in degree (NOT edges)
            // every loop -> process one node 
            // and access corresponding edge list
            for (int i = 0; i < edges[course].size(); i++) {
                int pointer = (int) edges[course].get(i); 
                // cause error without casting
                // incompatible types: Object cannot be converted to int
                // Look at declaration of edges: 
                // *** List[] edges = new ArrayList[numCourses]
                
                degree[pointer]--;
                if (degree[pointer] == 0) {
                    q.offer(pointer);
                }
            }
        }
        
        return count == numCourses;
    }
}
```





### Course Scheduler II

https://leetcode.com/problems/course-schedule-ii/description/

There are a total of *n* courses you have to take, labeled from `0` to `n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is `[0,1]`

```
4, [[1,0],[2,0],[3,1],[3,2]]
```

There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is `[0,1,2,3]`. Another correct ordering is`[0,2,1,3]`.



**Method**



```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // (1, 0) 
        // 0 -> 1
        
        List[] edges = new ArrayList[numCourses]; // out-degree nodes
        int[] degree = new int[numCourses];
        
        for (int i = 0; i < numCourses; i++) {
            edges[i] = new ArrayList<Integer>();
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            degree[prerequisites[i][0]]++;
            edges[prerequisites[i][1]].add(prerequisites[i][0]);
        }
        
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (degree[i] == 0) {
                q.offer(i);
            }
        }
        
        int[] order = new int[numCourses];
        int count = 0;
        
        while (!q.isEmpty()) {
            int course = q.poll();
            order[count++] = course;
            
            for (int i = 0 ; i < edges[course].size(); i++) {
                int pointer = (int) edges[course].get(i);
                degree[pointer]--;
                
                if (degree[pointer] == 0) {
                    q.offer(pointer);
                }
            }
        }
        
        if (count == numCourses) {
            return order;
        } else {
            return new int[0];
        }
    }
}
```

