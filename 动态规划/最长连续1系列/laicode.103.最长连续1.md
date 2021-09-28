


```java
public class Solution {
  public int longest(int[] array) {
    // Write your solution here
    if (array == null || array.length < 1) {
      return 0;
    }
    int[] M = new int[array.length];
    M[0] = array[0] == 1 ? 1 : 0;
    int globalMax = M[0];
    for (int i = 1; i < array.length; i++) {
      if (array[i] == 0) {
        M[i] = 0;
      } else {
        M[i] = M[i - 1] + 1;
        globalMax = Math.max(globalMax, M[i]);
      }
    }
    return globalMax;
  }
}

```