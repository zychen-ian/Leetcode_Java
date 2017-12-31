### High Five Scores

Given a list of Result objects which include the id and score of students. Each student will have at least five scores. Calculate the <u>average score of the highest five scores</u> of each student.



**Method**:

* Use hashmap to store each student's id and average score. (<u>returned result</u>)
* Use priorityqueue to ensure the highest five scores of each student. (Default: min-heap, so need to poll if size > 5)
* time:O(n), space:O(n)



```java
import java.util.*;

class Result{
    int id;
    int value;
    public Result(int id, int value){
        this.id = id;
        this.value = value;
    }
}
public class Solution {
    public static Map<Integer, Double> getHighFive(Result[] results){
        if (results == null || results.length == 0) {
            return null;
        }
        // Collect 5 highest scores for each stu (Map & MinHeap)
        Map<Integer, PriorityQueue<Integer>> map = new HashMap<>();
        for (Result result : results) {
            int id = result.id;
            int value = result.value;
            if (!map.containsKey(id)) {
                PriorityQueue<Integer> minheap = new PriorityQueue<>(6);
                minheap.add(value);
                map.put(id, minheap);
            } else {
                map.get(id).add(value);
                if (map.get(id).size() > 5) {
                    map.get(id).poll();
                }
            }
        }
        // Compute average score for each stu (Map)
        Map<Integer, Double> resultMap = new HashMap<>();
        for (Map.Entry<Integer, PriorityQueue<Integer>> entry : map.entrySet()) {
            PriorityQueue<Integer> pq = entry.getValue();
            double mark = 0;
            while (!pq.isEmpty()) {
                mark += pq.poll();
            }
            mark = mark / 5.0;
            resultMap.put(entry.getKey(), mark);
        }
        // Answer
        return resultMap;
    }

    public static void main(String[] args) {
        Result r1 = new Result(1, 1);
        Result r2 = new Result(1, 7);
        Result r3 = new Result(1, 7);
        Result r4 = new Result(1, 6);
        Result r5 = new Result(1, 6);
        Result r6 = new Result(1, 6);

        Result r7 = new Result(2, 6);
        Result r8 = new Result(2, 6);
        Result r9 = new Result(2, 7);
        Result r10 = new Result(2, 6);
        Result r11 = new Result(2, 6);
        Result[] arr = {r1, r2, r3, r4, r5, r6, r7, r8, r9, r10, r11};
        Map<Integer, Double> res = getHighFive(arr);

        System.out.println(res.get(1) + " " +res.get(2));
    }
}
```

