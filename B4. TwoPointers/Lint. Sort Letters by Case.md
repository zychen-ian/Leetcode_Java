##Sort Letters by Case

Given a string which contains only letters. **Sort it by lower case first and upper case second.  (ONLY requirement)**

**Example**

For `"abAcD"`, a reasonable answer is `"acbAD"`

**Challenge**

Do it in one-pass and in-place.





**Remember**:

* Character.isCharacter(char)
* Character.isUpperCase(char)
* Character.isLowerCase(char)
* Character.isDigit(char)

```java
public class Solution {
    /** 
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] chars) {
        int i = 0, j = chars.length - 1;
		char tmp ;
		while ( i <= j) {
			while (i <= j && Character.isLowerCase(chars[i]) ) i++;
			while (i <= j && Character.isUpperCase(chars[j]) ) j--;
			if (i <= j) {
				tmp = chars[i];
				chars[i] = chars[j];
				chars[j] = tmp;
				i++; j--;
			}
		}
        //write your code here
		return ;
    }
}
```



* **Sort Uppercase first Lowercase second**
  * 'a' > 'A' > '0' (Please remember)
* **Sort uppercase & lower characters respectively**

```java
public class Solution {
    /*
     * @param chars: The letter array you should sort by Case
     * @return: nothing
     */
    public void sortLetters(char[] chars) {
        // write your code here
        if (chars == null || chars.length == 0) {
            return;
        }
        
        rainbowSort(chars, 0, chars.length - 1, 'a', 'z');
        rainbowSort(chars, 0, chars.length - 1, 'A', 'Z');
        
        
        
    }
    
    public void rainbowSort(char[] chars, //
                            int l, int r, //
                            char colorFrom, char colorTo) {
        
        if (colorFrom == colorTo) {
            return;
        }          
        
        if (l >= r) {
            return;
        }
        
        char colorMid = (char) (colorFrom + (colorTo - colorFrom) / 2);
        int left = l, right = r;
        
        while (left < right) {
            while (left < right && colorMid < chars[right]) {
                right--;
            }           
            
            while (left < right && colorMid >= chars[left]) {
                left++;
            }
            
            // swap
            if (left < right) {
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right] = temp;
                
                left++;
                right--;
            }
        }
        
        rainbowSort(chars, l, left, colorFrom, colorMid);
        rainbowSort(chars, left, r, (char) (colorMid + 1), colorTo);
    }
}
```

