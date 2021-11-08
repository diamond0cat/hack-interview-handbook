

```java
public class Solution {
  public int longest(int[] array) {
    // Write your solution here
    if (array == null || array.length == 0) return 0;
    int n = array.length;
    int[] f = new int[n];  // f[i] represent length of longest consecutive 1s ending at i

    f[0] = array[0] == 1 ? 1 : 0;
    int globalMax = f[0];

    for (int i = 1; i < n; i++) {
      if (array[i] == 0) f[i] = 0;
      else  {
        f[i] = f[i - 1] + 1;
        globalMax = Math.max(globalMax, f[i]);
      }
    }
    return globalMax;

  }
}

```