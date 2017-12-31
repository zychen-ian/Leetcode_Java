###Movie Network

```java
public class Movie {
    int movieId;
    float rating;
    List<Movie> similarMovies;
    // getters
}
```



给一部电影，要求返回跟这部电影相关的，排名最高的 N 部电影，其中不包括输入的那部电影!!

输出不需要排序。如果不够 N 部，就有多少输出多少部。



**Method**:

* BFS
  * queue
* minHeap
  * if minHeap.size() == k && pq.peak() < movie.rate   —>  pq.poll(); pq.offer(movie);
  * if minHeap.size() <  k  —>   pq.offer(movie)

```java
public static List<Movie> getNearest(Movie movie, int numSimilar)
```







​				
​			
​		
​	

​		
​		
​	
​	
​		
​			
​				
​					
​						public static List<Movie> getNearest(Movie movie, int numSimilar)。


​				
​			
​		
​	