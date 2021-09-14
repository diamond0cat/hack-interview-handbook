

```java
Determine if the characters of a given string are all unique.

Assumptions

The only set of possible characters used in the string are 'a' - 'z', the 26 lower case letters.
The given string is not null.
Examples

the characters used in "abcd" are unique
the characters used in "aba" are not unique
```



```java
public class Solution {
  public boolean allUnique(String word) {
    // Write your solution here
    int occuredChars = 0;
    char[] arr = word.toCharArray();
    for (int i = 0; i < arr.length; i++) {
      int k = arr[i] - 'a';   // 字符转数字
      // check if occuredChars's kth bit is 1
      if (((occuredChars >> k) & 1) == 1) return false;  // contains duplicate,这里不再是数组操作，而是看某一个bit

    // set occuredChars's k-th bit to 1
      occuredChars |= (1 << k);
    }
    return true;
  }
}

```