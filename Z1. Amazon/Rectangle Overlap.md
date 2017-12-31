###Rectangle Overlap

http://www.jiuzhang.com/solution/rectangle-overlap/



```java
/**
 * Definition for a point.
 * class Point {
 *     public int x, y;
 *     public Point() { x = 0; y = 0; }
 *     public Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    /**
     * @param l1 top-left coordinate of first rectangle
     * @param r1 bottom-right coordinate of first rectangle
     * @param l2 top-left coordinate of second rectangle
     * @param r2 bottom-right coordinate of second rectangle
     * @return true if they are overlap or false
     */
    public boolean doOverlap(Point l1, Point r1, Point l2, Point r2) {
		// l: top-left
        // r: bottom-right
        
        // pivot: rect1
      
        // left-right
        // rect2 (space) rect1   or   rect1 (space) rect2
        if (l1.x > r2.x || l2.x > r1.x)
            return false;
        
        // top-bottom
        //  rect2      rect1
        // (space) or (space)
        //  rect1      rect2
        if (l1.y < r2.y || l2.y < r1.y)
            return false;
   
        // including cases like left && top, or right && bottom
      
        return true;
    }
}
```



