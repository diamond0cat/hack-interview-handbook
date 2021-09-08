
Given a string, remove all leading/trailing/duplicated empty spaces.

Assumptions:

The given string is not null.
Examples:

“  a” --> “a”
“   I     love MTV ” --> “I love MTV”

```java
public class Solution {
  public String removeSpaces(String input) {
    char[] charArr = input.toCharArray();
    int slow = 0;
    for (int fast = 0; fast < charArr.length; fast++) {
     if (charArr[fast] == ' ' && (slow == 0 || charArr[slow - 1] == ' ')) {
       continue;
     }
     charArr[slow++] = charArr[fast];
    }
    if (slow > 0 && charArr[slow - 1] == ' ') { //post-processing: 如果slow-1等于空格,slow--，把![picture 5](https://i.loli.net/2021/09/08/V1rXY9Z4ycSpJ2L.png)  

      slow--;
    }
    return new String(charArr, 0, slow);
  }
}
```
![picture 6](https://i.loli.net/2021/09/08/V1rXY9Z4ycSpJ2L.png)  
