
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
    if (slow > 0 && charArr[slow - 1] == ' ') {
      slow--;
    }
    return new String(charArr, 0, slow);
  }
}
```