##Two Sum

https://leetcode.com/problems/two-sum/description/

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```



**Method**:

* HashSet
  * Time: ${O(n)}$
  * Space: ${O(n)}$
* Sort & Two Pointers
  * Time: ${O(nlog_2 n)}$
  * Space: ${O(1)}$ - QuickSort

```java
public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
         numbers=[2, 7, 11, 15],  target=9
         return [1, 2]
     */
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> map = new HashMap<>();

        for (int i = 0; i < numbers.length; i++) {
            if (map.get(numbers[i]) != null) {
                int[] result = {map.get(numbers[i]) + 1, i + 1};
                return result;
            }
            map.put(target - numbers[i], i);
        }
        
        int[] result = {}; // tech communication
        return result;
    }
}

```



##Two Sum II - Input array is sorted

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Input:** numbers={2, 7, 11, 15}, target=9
**Output:** index1=1, index2=2



```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        if (numbers == null || numbers.length == 0) {
            return new int[]{0, 0}; // grammar
        }
        
        int left = 0;
        int right = numbers.length - 1;
        
        while (left < right) {
            int sum = numbers[left] + numbers[right];
            
            if (sum == target) {
                return new int[]{left + 1, right + 1}; // not actual index (index + 1)
            } else if (sum > target) {
                right--;
            } else {
                left++;
            }
        }
            
        return new int[]{0, 0};
    }
}

```





##Two Sum II - Larger than Target; # of Pairs

https://aaronice.gitbooks.io/lintcode/content/two_pointers/two_sum_ii.html

Given an array of integers, find how many pairs in the array such that their sum is **bigger than** a specific target number. Please return the number of pairs.

**Example**

Given numbers = `[2, 7, 11, 15]`, target = 24. Return 1. (11 + 15 is the only pair)

**Challenge**

Do it in O(1) extra space and O(nlogn) time.

**Method**

* Sort
* Two Pointers 
  * A[i] + A[j] > target: j--
  * A[i] + A[j] <= target: i++
  * until i == j 
* Time: ${O(nlog_2n + n)}$
* Space: ${O(1)}$



```java
public class Solution{
  public int twoSum2(int[] nums, int target) {
      if (nums == null || nums.length == 0) {
          return 0;
      }
    
      // !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! - Used in Valid Triangle Number
      Arrays.sort(nums);
      int left = 0, right = nums.length - 1;
      int ans = 0;
      while (left < right) {
          if (nums[left] + nums[right] > target) {
              ans += right - left;
              right--;
          } else {
              left++;
          }
      }
      return ans;
  }
}
```



##Three Sum

https://leetcode.com/problems/3sum/description/

Given an array *S* of *n* integers, are there elements *a*, *b*, *c* in *S* such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must **not contain duplicate triplets.**

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



* **NOT** duplicate triplets
* ​

```java
public class Solution {
    /**
     * @param nums : Give an array numbers of n integer
     * @return : Find all unique triplets in the array which gives the sum of zero.
     */
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> results = new ArrayList<>(); // !!! This works
        
        if (nums == null || nums.length < 3) { // nums.length < 3
            return results;
        }
        
        // DONT FORGET SORT...
        Arrays.sort(nums); // SORT and break down to 2SUM - INPUT IS SORTED ARRAY

        for (int i = 0; i < nums.length - 2; i++) { // DONT MISS -2
            // skip duplicate triples with the same first numebr
            if (i > 0 && nums[i] == nums[i - 1]) { // if NOT while!!!
                continue;
            }

            int left = i + 1, right = nums.length - 1;
            int target = 0 - nums[i]; // sumTarget - nums[i]
            
            twoSum(nums, left, right, target, results);
        }
        
        return results;
    }
    
    public void twoSum(int[] nums,
                       int left,
                       int right,
                       int target,
                       List<List<Integer>> results) {
        while (left < right) {
            if (nums[left] + nums[right] == target) {
                ArrayList<Integer> triple = new ArrayList<>();
                triple.add(-target);
                triple.add(nums[left]);
                triple.add(nums[right]);
                results.add(triple);
              
                // First to do
                left++;
                right--;
              
                // skip duplicate pairs with the same left
                while (left < right && nums[left] == nums[left - 1]) { // while not if!
                    left++;
                }
                // skip duplicate pairs with the same right
                while (left < right && nums[right] == nums[right + 1]) {
                    right--;
                }
            } else if (nums[left] + nums[right] < target) {
                left++;
            } else {
                right--;
            }
        }
    }
}
```





##Three Sum Cloest

https://leetcode.com/problems/3sum-closest/description/

Given an array *S* of *n* integers, find three integers in *S* such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```



* Exactly One Solution

```java
public class Solution {
    /**
     * @param numbers: Give an array numbers of n integer
     * @param target : An integer
     * @return : return the sum of the three integers, the sum closest target.
     */
    public int threeSumClosest(int[] numbers, int target) {
        if (numbers == null || numbers.length < 3) {
            return -1;
        }
        
        Arrays.sort(numbers);
        int bestSum = numbers[0] + numbers[1] + numbers[2]; // GOOD WAY for setting
      												 // initial state for comparisons
        for (int i = 0; i < numbers.length; i++) {
            int start = i + 1, end = numbers.length - 1;
            while (start < end) {
                int sum = numbers[i] + numbers[start] + numbers[end];
                if (Math.abs(target - sum) < Math.abs(target - bestSum)) {
                    bestSum = sum;
                }
                if (sum < target) {
                    start++;
                } else {
                    end--;
                }
            }
        }
        
        return bestSum;
    }
}
```



```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) {
            return 0; // tech commu
        }
        
        // Cloest
        // Math.abs(sum - target) -> smallest
        Arrays.sort(nums);
        
        int cloest = nums[0] + nums[1] + nums[2]; // GOOD WAY!!!
        
        for (int i = 0; i < nums.length - 2; i++)    {
            
            int twoSumTarget = target - nums[i];
            int left = i + 1, right = nums.length - 1;
            
            int sum = twoSumCloest(nums, twoSumTarget, left, right) + nums[i];
            
            if (Math.abs(target - sum) < Math.abs(target - cloest)) {
                cloest = sum;
            }
        }
                
        return cloest;
    }
    
    public int twoSumCloest(int[] nums, int target, int left, int right) {
        int cloest = nums[left] + nums[left + 1]; // GOOD WAY!!!
        
        while (left < right) {
            int sum = nums[left] +  nums[right];
          
            // check cloest
            if (Math.abs(target - sum) < Math.abs(target - cloest)) {
                cloest = sum;
            } 
            
            // move
            if (sum > target) {
                right--;
            } else {
                left++;
            }
            
        }
        
        return cloest;
    }
}

```



##Two Sum Cloest









##Four Sum

https://leetcode.com/problems/4sum/description/

Given an array *S* of *n* integers, are there elements *a*, *b*, *c*, and *d* in *S* such that *a* + *b* + *c* + *d* = target? Find all unique quadruplets in the array which gives the sum of target.

**Note:** The solution set must not contain duplicate quadruplets.





* NOT contain duplicate quadruplets.

```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```



```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null || nums.length < 4) {
            return results;
        }
        
        Arrays.sort(nums);
        
        for (int i = 0; i < nums.length - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) { // remove duplicates
                continue;
            }
            
            int threeSumTarget = target - nums[i];
            
            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) { // remove duplicates
                    continue;
                }
                
                int twoSumTarget = threeSumTarget - nums[j];
                
                int left = j + 1;
                int right = nums.length - 1;
                
                twoSum(nums, twoSumTarget, i, j, left, right, results);
            }
        }
        return results;        
    }
    
    public void twoSum(int[] nums, int target, int i, int j, //
                      int left, int right, //
                      List<List<Integer>> results) {
        
        while (left < right) {
            int sum = nums[left] + nums[right];
            
            if (sum == target) {
                List<Integer> result = new ArrayList<Integer>();
                result.add(nums[i]);
                result.add(nums[j]);
                result.add(nums[left]);
                result.add(nums[right]);
                
                results.add(result);
                
                right--;
                left++;
                
                // remove duplicates
                while (left < right && nums[right] == nums[right + 1]) {
                    right--;
                }
                // remove duplicates
                while (left < right && nums[left] == nums[left - 1]) {
                    left++;
                }
                
            } else if (sum > target) {
                right--;    
            } else {
                left++;
            }
        }
    }
}
```



* nine-chapter

```java
public class Solution {
	public List<List<Integer>> fourSum(int[] num, int target) {
		List<List<Integer>> rst = new ArrayList<List<Integer>>();
		Arrays.sort(num);

		for (int i = 0; i < num.length - 3; i++) {
			if (i != 0 && num[i] == num[i - 1]) {
				continue;
			}

			for (int j = i + 1; j < num.length - 2; j++) {
				if (j != i + 1 && num[j] == num[j - 1])
					continue;

				int left = j + 1;
				int right = num.length - 1;
				while (left < right) {
					int sum = num[i] + num[j] + num[left] + num[right];
					if (sum < target) {
						left++;
					} else if (sum > target) {
						right--;
					} else {
						ArrayList<Integer> tmp = new ArrayList<Integer>();
						tmp.add(num[i]);
						tmp.add(num[j]);
						tmp.add(num[left]);
						tmp.add(num[right]);
						rst.add(tmp);
						left++;
						right--;
						while (left < right && num[left] == num[left - 1]) {
							left++;
						}
						while (left < right && num[right] == num[right + 1]) {
							right--;
						}
					}
				}
			}
		}

		return rst;
	}
}
```









