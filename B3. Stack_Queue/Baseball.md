###Baseball

输入是一个字符串数组，每一个值可能是一个整数，或者Z，或者X，或者+。整数代表现在拿的分，X代表当前成绩是前一个分数Double，+代表当前成绩是前两个的和，Z代表移除前一个成绩，然后要求的是最后的总成绩

Given a string array representing a throw ball blocks, each string is either a number, +, Z, X. Calculate total. 

* If number, cur score is number, and add it to total & stack. 
* If +, cur score is sum of last 2 scores, and add it to total & stack.  
* If X, cur score is double of last score, and add it to toal & stack.
* **If Z, remove last score from total & stack.**

<u>Use 0 for any missing last score</u>. 有些 corner cases 要考虑


​				
​			
​		
​	

```java
5 : sum = 5 // SK: 5
-2: sum = 5 - 2 = 3 // SK: -2, 5
4 : sum = 3 + 4 = 7
Z : sum = 7 - 4 = 3
X : sum = 3 + -2 * 2 = -1 (因为4被移除了，前一个成绩是-2)
9 : sum = -1 + 9 = 8
+ : sum = 8 + 9 - 4 = 13 (前两个成绩是9和-4)
+ : sum = 13 + 9 + 5 = 27 (前两个成绩是5 和 9)
```

```java
package sec7;

import java.util.Stack;

public class Baseball {
	
	public int baseball(String[] arr) {
        Stack<Integer> sk = new Stack<Integer>();
        int sum = 0;
        for (String str : arr) {
            if (str.equals("Z")) { // remove last score
                if (!sk.isEmpty()) {
                    int item = sk.pop();
                    sum -= item;
                }
            } else if (str.equals("X")) { // current score = 2 * last score
                int item = 0;
                if (!sk.isEmpty()) {
                    item = sk.peek() * 2;
                    sum += item;
                } 
                sk.push(item); 
            } else if (str.equals("+")) { // current score = last score + last 2nd score
                int item1 = 0, item2 = 0;
                if (!sk.isEmpty()) {
                    item1 = sk.pop();
                    if (!sk.isEmpty()) {
                        item2 = sk.pop();
                        sk.push(item2);
                    }
                    sk.push(item1);
                }
                int item = item1 + item2;
                sum += item;
                sk.push(item);
            } else {
                int item = Integer.valueOf(str);
                sum += item;
                sk.push(item);
            }
        }
        return sum;
    }
	
	public static void main(String args[]) {
		Baseball bb = new Baseball();
		String[] arr = {"5", "-2", "4", "Z", //
						"X", "9", "+", "+"};
		int sum = bb.baseball(arr);
		System.out.println(sum);
	}
}
```

