## Data Stream Median

http://www.lintcode.com/en/problem/data-stream-median/

Numbers keep coming, return the median of numbers at every time a new number added.

**Clarification**

What's the definition of Median?
\- Median is the number that in the middle of a sorted array. If there are n numbers in a sorted array A, the median is `A[(n - 1) / 2]`. For example, if `A=[1,2,3]`, median is `2`. If `A=[1,19]`, median is `1`.

**list A, median, list B**

* A's size == B's size (Total: odd)
* A's size + 1 == B's size (Total: even. Median is the smaller one)

**Example**

For numbers coming list: `[1, 2, 3, 4, 5]`, return `[1, 1, 2, 2, 3]`.

For numbers coming list: `[4, 5, 1, 3, 2, 6, 0]`, return `[4, 4, 4, 3, 3, 3, 3]`.

For numbers coming list: `[2, 20, 100]`, return `[2, 2, 20]`.



Total run time in O(*nlogn*).

![data-stream-median-1](/Users/IanChan/Desktop/Interview/images/data-stream-median-1.png)





![data-stream-median-2](/Users/IanChan/Desktop/Interview/images/data-stream-median-2.png)

```java




```





##Sliding Window Median

https://leetcode.com/problems/sliding-window-median/

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 

`[2,3,4]` , the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.

For example,
Given *nums* = `[1,3,-1,-3,5,3,6,7]`, and *k* = 3.

```
Window position                Median
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7       -1
 1  3 [-1  -3  5] 3  6  7       -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6

```

Therefore, return the median sliding window as `[1,-1,-1,3,5,6]`.

**Note: **
You may assume `k` is always valid, ie: `k` is always smaller than input array's size for non-empty array.



* Sliding Window (e.g., [1, 3, -1])
  1. add a value (e.g, [1, 3, -1, -3]) - similar to **Data Stream Median** — $O(log_2n)$
  2. delete a value (e.g., [3, -1, -3])  — $O(log_2n)$
     1. Possibility 1: list A (left) - MaxHashHeap - remove $O(log_2n)$
     2. Possibility 2: median
        1. list A's size < list B's size: **min elem in list B shift to left**
        2. list A's size = list B's size: **max elem in list A shift to left**
     3. Possibility 3: list B (right) - MinHashHeap - remov  e $O(log_2n)$
  3. Total: $O(nlog_2n)$ same with **Data Stream Median**
  4. How to Handle duplicated elements
     1. Trick: use a pair to represent a node (value, index/position of an array)

```java



```



























