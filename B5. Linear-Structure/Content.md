###Content - Array

* Binary Search [Link](../BinarySearch-SortedArray/Content - Binary Search & Sorted Array.md) 
* Two Pointers [Link](../TwoPointers/Content.md)
* Dynamic Programming [Link](../DynamicProgramming/Content.md)
* Greedy
  * [Maximum/Minimum Subarray I & II](53. Maximum Subarray.md)
  * [Maximum Subarray Difference](Maximum Subarray Difference.md)
  * [Continuous Subarray Sum I & II](Continuous Subarray Sum.md)
* Data Structures
  * Stack
* Else
  * [674. Longest Continuous Increasing Subsequence](674. Longest Continuous Increasing Subsequence.md)

  * [56. Merge Intervals](56. Merge Intervals.md)

  * [57. Insert Interval](57. Insert Interval.md)

  * [283. Move Zeroes & 27. Remove Element](283. Move Zeroes.md)

  * [41. First Missing Positive](41. First Missing Positive.md)

  * [128. Longest Consecutive Sequence](128. Longest Consecutive Sequence.md)

    ​
* Matrix
  * [Spiral Matrix I & II](Spiral Matrix.md)
  * [Maximum Difference in Arrays](Maximum Difference in Arrays.md)





* Notes:

  * Edge Case Check

  ```java
  if (A == null || A.length == 0) { // array: 1-dimensional matrix
      return 0;
  }
  ```

  ```java
  if (matrix == null || matrix.length == 0) { // matrix: 2-dimensional matrix
      return res;
  }

  if (matrix[0] == null || matrix[0].length == 0) {
      return res;
  }
  ```

  ```java
  if (s == null || s.length() == 0) { // string (like 1-dimensional matrix)
      return 0;
  }
  ```

  ```java
  if (nums == null || nums.size() == 0) { // List
      return 0;
  }
  ```

  * **APIs** - ArrayList

  ```java
  ArrayList al = new ArrayList();

  al.add("C");     // al: C
  al.add("A");     // al: C, A
  al.add(1, "A2"); // a1: C, A2, A
  al.set(3, "A3"); // Throws IndexOutOfBoundsException if the specified index is out of range (index < 0 || index >= size()).
                   // Replaces the element at the specified position in this list with the specified element.
  al.remove(2);    // al: C, A2
  ```

  ```java
  return new int[]{-1, -1};
  ```

  * List< String > to Array String[]

  ```java
  List<String> list = new ArrayList<String>();
  //add some stuff
  list.add("android");
  list.add("apple");
  String[] stringArray = list.toArray(new String[0]);
  // argument: new String[0]
  // you have to pass an array as an argument, which will be filled with the data from the list, and returned. 
  ```

  * Initialize 2d array with **known row size** but **unknown col size**

  ```java
  public IntMatrix(int[][] array) {
      matrix = new int[array.length][]; // !!!!!
      for (int i = 0; i < array.length; i++) {
          matrix[i] = new int[array[i].length];  // !!!!
          for(int j=0; j < array[i].length; j++) {
              matrix[i][j] = array[i][j];
          }
      }
  }
  ```

  ​



###Content - HashMap

* Principles & Concepts
  * [Hash Function](Hash Function.md)


* Map/Set helps reduce time complexity
  * [Subarray Sum Equals K](560. Subarray Sum Equals K.md)
  * [Subarray Sum](Subarray Sum.md)
  * [Maximum Size Subarray Sum Equals k](560. Subarray Sum Equals K.md)
* Else
  * [Longest Palindrome](Longest Palindrome.md)
  * [Happy Number](Happy Number.md)
  * [Strings Homomorphism](Strings Homomorphism.md)
  * [Substring Anagrams/Find All Anagrams in a String](Substring Anagrams.md)
  * [Anagrams/Group Anagrams](Anagrams.md)
  * [First Unique Number In Stream](First Unique Number In Stream.md)
  * [Majority Number III](Majority Number III.md)
  * [Max Points on a Line](Max Points on a Line.md)





