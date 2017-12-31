###Spiral Matrix I

https://leetcode.com/problems/spiral-matrix/description/

Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

```

You should return `[1,2,3,6,9,8,7,4,5]`.

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<Integer>();
        if (matrix == null || matrix.length == 0) {
            return res;
        }
        
        if (matrix[0] == null || matrix[0].length == 0) {
            return res;
        }
        
        int row = matrix.length;
        int col = matrix[0].length;
        int count = 0;

        // row odd  5:  count: [0..2(mid)]
        // row even 4:  count: [0..1]
        while (count * 2 < row && count * 2 < col) { // && 
            // top row - whole row[0...end]
            for (int i = count; i < col - count; i++) {
                res.add(matrix[count][i]);
            }
            
            // last col - col[1...end]
            for (int i = count + 1; i < row - count; i++) {
                res.add(matrix[i][col - count - 1]);
            }
            
            // count of rows: odd && count is in the middle
            // * * * * 
            // count of cols: odd && count is in the middle
            //   * 
            //   *
            //   * 
            if (row - 2 * count == 1 || col - 2 * count == 1) { // ||
                break;
            }
            
            
            // down row - row[0...end - 1]
            for (int i = col - count - 2; i >= count; i--) {
                res.add(matrix[row - count - 1][i]);
            }
            
            // first col - col[1..end - 1]
            for (int i = row - count - 2; i >= count + 1; i--) {
                res.add(matrix[i][count]);
            }
            
            count++;
        }
        
        return res;
        
    }
}
```





###Spiral Matrix II

https://leetcode.com/problems/spiral-matrix-ii/description/

Given an integer *n*, generate a square matrix filled with elements from 1 to *n*2 in spiral order.

For example,
Given *n* = `3`,

```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```



```java
class Solution {
    public int[][] generateMatrix(int n) {
        if (n <= 0) {
            return new int[0][0];
        }
        
        int[][] matrix = new int[n][n];

        int count = 0;
        int val = 1;
        
        while (count * 2 < n) {
            
            for (int i = count; i < n - count; i++) {
                matrix[count][i] = val++;
            }
            
            for (int i = count + 1; i < n - count; i++) {
                matrix[i][n - count - 1] = val++;
            }
            
            if (n - count * 2 == 1) {
                break;
            }
            
            for (int i = n - count - 2; i >= count; i--) {
                matrix[n - count - 1][i] = val++;
            }
            
            for (int i = n - count - 2; i>= count + 1; i--) {
                matrix[i][count] = val++;
            }
            
            count++;
        }
        
        return matrix;
    }
}
```

