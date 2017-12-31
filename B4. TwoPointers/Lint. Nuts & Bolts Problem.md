##Nuts & Bolts Problem

http://www.lintcode.com/en/problem/nuts-bolts-problem/

Given a set of *n* nuts of different sizes and *n* bolts of different sizes. There is a one-one mapping between nuts and bolts. Comparison of a nut to another nut or a bolt to another bolt is not allowed. It means nut can only be compared with bolt and bolt can only be compared with nut to see which one is bigger/smaller.

We will give you a compare function to compare nut with bolt.

**Example**

Given nuts = `['ab','bc','dd','gg']`, bolts = `['AB','GG', 'DD', 'BC']`.

Your code should find the matching bolts and nuts.

one of the possible return:

nuts = `['ab','bc','dd','gg']`, bolts = `['AB','BC','DD','GG']`.

we will tell you the match compare function. If we give you another compare functio

the possible return is the following:

nuts = `['ab','bc','dd','gg']`, bolts = `['BC','AA','DD','GG']`.

So you must use the compare function that we give to do the sorting.

`The order of the nuts or bolts does not matter. You just need to find the matching bolt for each nut.`





**Method**:

* 根据题目语境，螺丝钉之间很难**比较**/排序，螺母之间很难**比较**/排序
* Pivot: **nut** 
* Partition:  **bolts**
  * **[… < bolt]** bolt (fit with pivot nut) **[… > bolt]**
* Pivot: **bolt (fit with the above pivot nut) traverse to find $(O(n))$**
* Partition: **nuts**
  * **[… < nut]** nut (fit with pviot bolt) **[… > nut]**



=> 

![parition-2](../images/parition-2.png)







```java
public class Solution {
    /**
     * @param nuts: an array of integers
     * @param bolts: an array of integers
     * @param compare: a instance of Comparator
     * @return: nothing
     */
    public void sortNutsAndBolts(String[] nuts, String[] bolts, NBComparator compare) {
        if (nuts == null || nuts.length == 0) {
            return;
        }
        
        if (bolts == null || bolts.length == 0) {
            return;
        }
        
        if (nuts.length != bolts.length) {
            return;
        }

        qsort(nuts, bolts, compare, 0, nuts.length - 1);
    }

    private void qsort(String[] nuts, String[] bolts, NBComparator compare, 
                       int l, int u) {
        if (l >= u) return;
      
        // NUTS first or BOLTS first. Doesnt matter!!
        // find the partition index for nuts with bolts[l]
        int part_inx = partition(nuts, bolts[l], compare, l, u);
        // partition bolts with nuts[part_inx]
        partition(bolts, nuts[part_inx], compare, l, u);
        // qsort recursively
        qsort(nuts, bolts, compare, l, part_inx - 1);
        qsort(nuts, bolts, compare, part_inx + 1, u);
    }
    
    private int partition(String[] str, String pivot, NBComparator compare, 
                          int l, int u) {
        // preprocess: put the elem matching with pivot to the leftmost
        for (int i = l; i <= u; i++) {
            if (compare.cmp(str[i], pivot) == 0 || 
                compare.cmp(pivot, str[i]) == 0) {
                swap(str, i, l);
                break;
            }
        }
      
        // same with parition problem
        String now = str[l];
        int left = l; 
        int right = u;
        while (left < right) {
            while (left < right && 
            (compare.cmp(str[right], pivot) == -1 || 
            compare.cmp(pivot, str[right]) == 1)) { // easy mistake - grammar
                right--;
            }
            str[left] = str[right];
            
            while (left < right && 
             (compare.cmp(str[left], pivot) == 1 || 
             compare.cmp(pivot, str[left]) == -1)) { // easy mistake - grammar
                left++;
            }
            str[right] = str[left];
        }
        str[left] = now;

        return left;
    }

    private void swap(String[] str, int l, int r) {
        String temp = str[l];
        str[l] = str[r];
        str[r] = temp;
    }
}

```

