###K Closest Points (matrix)

http://www.lintcode.com/en/problem/k-closest-points/#

Given some `points` and a point `origin` in two dimensional space, find `k` points out of the some points which are nearest to `origin`.
Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.



Example

Given points = `[[4,6],[4,7],[4,4],[2,5],[1,1]]`, origin = `[0, 0]`, k = `3`
return `[[1,1],[2,5],[4,4]]`



**Method**

```java
1. Use PriorityQueue as MaxHeap to store points
   For comparator, first distance, second x, last y 
   (default is minHeap for priorityQueue)
2. Traverse each point, add it to priority queue, if size > k, poll a point
3. Construct a result array storing point in increasing order. PriorityQueue is max heap, so need to create array reversely. from end to start.
```



```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */


public class Solution {
    /*
     * @param points: a list of points
     * @param origin: a point
     * @param k: An integer
     * @return: the k closest points
     */
     
    private Point global_origin = null; 
    public Point[] kClosest(Point[] points, Point origin, int k) {
        
        global_origin = origin;
        
        // max heap 
        // argument k: initial capacity
        // PriorityQueue(int initialCapacity, Comparator<? super E> comparator)
        PriorityQueue<Point> pq = new PriorityQueue<Point>(k, new Comparator<Point> () {
            @Override
            public int compare(Point p1, Point p2) { 
                // multiple comparator
                // - first distance
                // - second x
                // - last y
                
                // max heap - reverse order 
                // so p2 - p1
                int diff = getDistance(p2, global_origin) - getDistance(p1, global_origin);
                
                // max heap - reverse order
                if (diff == 0) {
                    diff = p2.x - p1.x;
                }
                if (diff == 0) {
                    diff = p2.y - p1.y;
                }
                
                return diff;
            }
        });
        
        for (Point p : points) {
            pq.offer(p);
            if (pq.size() > k) {
                pq.poll();
            } 
        }
        
        Point[] res = new Point[k];
        while (k > 0) {
            res[--k] = pq.poll();
        }
                
        return res;
        
    }
     
    private int getDistance(Point a, Point b) {
        return (a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y);
    }
}
```



##K closest numbers in sorted array (Binary Search)

https://leetcode.com/problems/find-k-closest-elements/description/

Given a sorted array, two integers `k` and `x`, find the `k` closest elements to `x` in the array. <u>The result should also be sorted in ascending orde</u>r. If there is a tie, the smaller elements are always preferred.

**Example 1:**

```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

**Example 2:**

```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]

```

**Note:**

1. The value k is positive and will always be smaller than the length of the sorted array.
2. Length of the given array is positive and will not exceed 104
3. Absolute value of elements in the array and x will not exceed 104

The *arr* parameter had been changed to an **array of integers** (instead of a list of integers). **Please reload the code definition to get the latest changes**.



**Lintcode Version**

Given a target number, a non-negative integer k and an integer array A sorted in ascending order, find the k closest numbers to target in A, <u>sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.</u>

Example

Given A = [1, 2, 3], target = 2 and k = 3, return [2, 1, 3].

Given A = [1, 4, 6, 8], target = 3 and k = 3, return [4, 1, 6].



* Leetcode: result sorted just in ascending order
* Lintcode: result sorted in ascending order by the diff bet. number and target. If diff same, sort by number

```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        // sorted array
        // result: subarray of arr
        
        List<Integer> res = new ArrayList<Integer>();
        
        if (arr == null || arr.length == 0) {
            return res;
        }
        
        if (k > arr.length) { // arr too short
            return res;
        }
        
        // binary tree find the target (1st elem)
        int index = firstIndex(arr, x); // 0 ~ arr.length
        
        int start = index - 1; 
        int end = index;
        for (int i = 0; i < k; i++) { // k elem
            if (start < 0) { // end == 0, if  index == 0
                end++;
                // res.add(arr[end++]);  Lintcode version
            } else if (end >= arr.length) { // start == arr.length - 1, 
                                            // if index == arr.length
                start--;
                // res.add(arr[start--]); Lintcode version
            } else {
                // smaller elem
                if (x - arr[start] <= arr[end] - x) {
                    start--;
                    // res.add(arr[start--]); Lintcode version
                } else {
                    end++;
                    // res.add(arr[end++]); Lintcode version
                }
            }
        }
        
        // subarray arr[start + 1...end - 1]
        // like substring in String
        return res.subList(start + 1, end);
    }
    
    // target is not always in the arr for all possible input
    private int firstIndex(int[] arr, int target) {
        int start = 0, end = arr.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            
            if (arr[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (arr[start] >= target) {
            return start;
        } else if (arr[end] >= target) {
            return end;
        } 
        
        return end + 1; // or arr.length; // same
    }
}
```

