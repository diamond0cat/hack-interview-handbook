

```java
public class Solution {
  public int[] largestSum(int[] array) {
    // Write your solution here
    // return [largest, maxLeft, maxRight]
    if (array == null || array.length < 1) {
      return new int[]{0, 0, 0};
    }
    int[] M = new int[array.length];
    int curLeft = 0, globalLeft = 0, globalRight = 0;
    M[0] = array[0];
     int globalMax = M[0];
    for (int i = 1; i < array.length; i++) {
      if (M[i - 1] < 0) {
        M[i] = array[i];
        curLeft = i;
      } else {
        M[i] = M[i - 1] + array[i];
      }
      if (M[i] > globalMax) {
          globalMax = M[i];
          globalLeft = curLeft;
          globalRight = i;
      }
    }
    return new int[]{globalMax, globalLeft, globalRight};
  }
}

```