###Min Stack

http://www.lintcode.com/en/problem/min-stack/#

Implement a stack with min() function, which will return the smallest number in the stack.

It should support push, pop and min operation all in O(1) cost.

##### Notice

min operation will never be called if there is no number in the stack.

**Example**

```
push(1)
pop()   // return 1
push(2)
push(3)
min()   // return 2
push(1)
min()   // return 1
```



```java
public class MinStack {
    private Stack<Integer> stack = null;
    private Stack<Integer> minStack = null;
    
    // size of stack & minStack is always same
    
    /*
    * @param a: An integer
    */
    public MinStack() {
        // do intialization if necessary
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }

    /*
     * @param number: An integer
     * @return: nothing
     */
    public void push(int number) {
        // write your code here
        stack.push(number);
        
        if (minStack.isEmpty()) {
            minStack.push(number);
        } else {
            minStack.push(Math.min(number, minStack.peek()));
        }
    }

    /*
     * @return: An integer
     */
    public int pop() {
        // write your code here
        minStack.pop();
        return stack.pop();
    }

    /*
     * @return: An integer
     */
    public int min() {
        // write your code here
        return minStack.peek();
    }
}
```

