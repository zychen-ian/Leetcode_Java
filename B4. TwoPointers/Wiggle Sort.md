###Wiggle Sort I

http://www.lintcode.com/en/problem/wiggle-sort/#

Given an unsorted array `nums`, reorder it in-place such that

```
nums[0] <= nums[1] >= nums[2] <= nums[3]....
```

Example

Given `nums = [3, 5, 2, 1, 6, 4]`, one possible answer is `[1, 6, 2, 5, 3, 4]`.



* Space: in-place
* Time: $O(n)$

````java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: nothing
     */
    public void wiggleSort(int[] nums) {
        // 摆动排序
        
        for (int i = 1; i < nums.length; i++) {
            
            // 奇大偶小 (奇偶为index)
            if (i % 2 == 0 && nums[i] > nums[i - 1] ||
                i % 2 == 1 && nums[i] < nums[i - 1]) {
                    swap(nums, i, i-1);
                }
            
        }
                
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
````

- Space: in-place
- Time: $O(nlog_2n)$

```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: nothing
     */
    public void wiggleSort(int[] nums) {
        // 摆动排序
        Arrays.sort(nums);
        
        for (int i = 1; i < nums.length; i++) {
            if (i % 2 == 0) {
                swap(nums, i, i-1);
            }
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```





###Wiggle Sort II

http://www.lintcode.com/en/problem/wiggle-sort-ii/

Given an unsorted array `nums`, reorder it such that

```
nums[0] < nums[1] > nums[2] < nums[3]....
```

**Example**

Given `nums = [1, 5, 1, 1, 6, 4]`, one possible answer is `[1, 4, 1, 5, 1, 6]`.

Given `nums = [1, 3, 2, 2, 3, 1]`, one possible answer is `[2, 3, 1, 3, 1, 2]`.



这道题其实就是要找一个中间值，比中间值小的插入到偶数位上，比中间值大的插入到奇数位上。

1. 用quick select寻找中间值（即能平分nums中所有元素的元素的值）

2. 将ans的值全部设为中间值，遍历数组nums，将遇到的数和中间值比较，间隔地插入ans中

3. 若原数组长度为偶数，则为小->大->小。。。->大的形式，小的数从后往前(len - 2)寻找位置插入，大的数从前往后(1)寻找位置插入

   若原数组长度为奇数，则为大->小->大。。。->小的形式，小的数从前往后(0)寻找位置插入，大的数从后往前(len - 2)寻找位置插入



https://www.hrwhisper.me/leetcode-wiggle-sort-ii/

用快排的思想查找中位数，然后再合并两边。

最坏复杂度O(n^2)，平均复杂度O(n)。

* wiggleSort
* quickSortToFindMedium (better to separate findMid & partition)
  * **findMedium** 
    * This template (similar to QuickSort) is VERY important
    * You can find value of any desired position, like mid and rank is (nums.length - 1) / 2 (inspired by **median**)
  * partition
  * swap

```java
class Solution {
    public void wiggleSort(int[] nums) {
        // O(n) time and/or in-place with O(1) extra space?
        
        int[] tem = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++) {
            tem[i] = nums[i];
        }
        
        // mid: value of mid of nums (NOT index)
        // rank: index (nums.length - 1) / 2
        //       kth   (nums.length - 1) / 2 + 1 
        //             --- 215. Kth Largest Element in an Array.md
        int mid = findMedium(tem, 0, nums.length - 1, (nums.length - 1) / 2);
                
        // input: 111111111 -> 111111111 unchanged
        int[] ans = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            ans[i] = mid;
        }
        
        // two pointers
        int l, r;
        if (nums.length % 2 == 0) { // even count
            // 0 1 2 3 (TOTAL: 4)
            l = nums.length - 2; // last EVEN index -> first EVEN by loop
            r = 1; // first ODD index -> last ODD by loop
            
            for (int i = 0; i < nums.length; i++) {
                if (nums[i] < mid) { // smaller
                    ans[l] = nums[i]; // put to EVEN index
                    l -= 2;
                } else if (nums[i] > mid) { // larger
                    ans[r] = nums[i]; // put to ODD index
                    r += 2;
                }
            }
        } else { // odd count
            l = 0; // first EVEN index -> last EVEN by loop
            r = nums.length - 2; // last ODD index -> first ODD by loop
            
            for (int i = 0; i < nums.length; i++) {
                if (nums[i] < mid) { // smaller
                    ans[l] = nums[i];
                    l += 2;
                } else if (nums[i] > mid) {
                    ans[r] = nums[i];
                    r -= 2;
                }
            }
        }
        
        for (int i = 0; i < nums.length; i++) {
            nums[i] = ans[i];
        }
    }
    
    // rank is always absolute index in the original array
    public int findMedium(int[] nums, int l, int r, int rank) {
        System.out.println("fm");
        
        if (l >= r) {
            return nums[l]; // or nums[l]
        }
        
        int idx = partition(nums, l, r);
        if (idx == rank) {
            return nums[idx];
        } else if (idx < rank) { // right
            return findMedium(nums, idx + 1, r, rank); 
        } else { // left
            return findMedium(nums, l, idx - 1, rank);
        }
    }
    
    public int partition(int[] nums, int l, int r) {
        System.out.println("pt");
        
        int left = l, right = r;
        int now = nums[left]; // pivot?
        while (left < right) {
            while (left < right && nums[right] >= now) {
                right--;
            }
            nums[left] = nums[right];
            
            while (left < right && nums[left] <= now) {
                left++;
            }
            nums[right] = nums[left];
        }
        
        // left == right
        nums[left] = now;
        
        return left;
        
        // if (left - 1 == rank) { // mid
        //     return now; 
        // } else if (left - 1 < rank) { // left to mid
        //     return partition(nums, left + 1, r, rank - (left + 1 - l));
        // } else { // right to mid
        //     return partition(nums, l, right - 1, rank);           
        // }
    }
    
    public void swap(int[] nums, int a, int b) {
        int tmp = nums[a];
        nums[a] = nums[b];
        nums[b] = tmp;
    }
}
```





