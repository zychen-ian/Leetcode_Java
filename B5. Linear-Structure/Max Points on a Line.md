###Max Points on a Line

https://leetcode.com/problems/max-points-on-a-line/description/

http://www.lintcode.com/en/problem/max-points-on-a-line/#

Given *n* points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Example**

Given 4 points: `(1,2)`, `(3,6)`, `(0,0)`, `(1,3)`.

The maximum number is `3`.



用double表示的双精度小数在有的系统里不一定准确，为了更加精确无误的计算共线，我们应当避免除法，从而避免无线不循环小数的出现，那么怎么办呢，我们把除数和被除数都保存下来，不做除法，但是我们要让这两数分别除以它们的最大公约数，这样例如8和4，4和2，2和1，这三组商相同的数就都会存到一个映射里面，同样也能实现我们的目标，而求GCD的函数如果用递归来写那么一行就搞定了，叼不叼，这个方法能很好的避免除法的出现，算是牺牲了空间来保证精度吧





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
     * @param points: an array of point
     * @return: An integer
     */
    public int maxPoints(Point[] points) {
        // write your code here
        
        if (points == null || points.length == 0) {
            return 0;
        }
        
        int ans = 0; 
        // every point can be base point
        for (int i = 0; i < points.length; i++) {
            
            Map<String, Integer> slope = new HashMap<String, Integer>();
            int maxPoints = 0, overlap = 0, vertical = 0;
            
            for (int j = i + 1; j < points.length; j++) {
                
                if (points[i].x == points[j].x) { 
                    if (points[i].y == points[j].y) { // overlap
                        overlap++;
                    } else { // vertical
                        vertical++;
                    }
                    continue;
                }
                
                int dx = points[i].x - points[j].x;
                int dy = points[i].y - points[j].y;
                
                int tmp = gcd(dx, dy); // greatest common divisor
                dx /= tmp;
                dy /= tmp;
                
                String k = dy + "/" + dx; // 最简
                
                if (!slope.containsKey(k)) {
                    slope.put(k, 0);
                }
                slope.put(k, slope.get(k) + 1);
                maxPoints = Math.max(maxPoints, slope.get(k)); // regular update
            }
            
            // maxPoints is max of points which is aligned with points[i] but not vertical
            maxPoints = Math.max(maxPoints, vertical);
            // maxPoints is max of points which is aligned with points[i] but including vertical
            
            ans = Math.max(ans, maxPoints + overlap + 1); // + itself
            
        }
        
        return ans;
    }
    
    // !!! 
    int gcd(int a, int b) {
        
        if (b == 0) {
            return a;
        } else {
            return gcd(b, a % b);
        }
        
    }
}


```

