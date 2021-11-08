Remove adjacent, repeated characters in a given string, leaving only one character for each group of such characters.

Assumptions

Try to do it in place.
Examples

“aaaabbbc” is transferred to “abc”
Corner Cases

If the given string is null, returning null or an empty string are both valid.

```java
public class Solution {
  public String deDup(String input) {
    // Write your solution here

    int slow = 0, fast = 0;
    char[] arr = input.toCharArray();

    while (fast < arr.length) {
      if (slow == 0 || arr[slow - 1] != arr[fast]) {
        arr[slow]  = arr[fast];
        slow++;
        fast++;
      
      } else {
        fast++;
      }
    }
    return new String(arr, 0, slow);
  }
}


```