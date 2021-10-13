
![picture 1](https://i.loli.net/2021/10/14/Ud7ehzLHauskMIj.png)  
![picture 2](https://i.loli.net/2021/10/14/U71v39NwcCHZEQl.png)  

- 搞一个对每个列的prefix sum
![picture 3](https://i.loli.net/2021/10/14/gGlqemL53HdEIAZ.png)  

- O(n^5)
```java
public class Solution {
  public int largest(int[][] matrix) {
    // Write your solution here
    int row = matrix.length;
    int col = matrix[0].length;

    int result = Integer.MIN_VALUE;
    for (int i = 0; i < row; i++) {
      int[] cur = new int[col];
      for (int j = i; j < row; j++) {
          add(cur, matrix[j]);

          result = Math.max(result, max(cur));
      }
    }
    return result;
  }

  private void add(int[] cur, int[] add) {
    for (int i = 0; i < cur.length; i++) {
      cur[i] += add[i];
    }
  }

  private int max(int[] cur) {
    int result = cur[0];
    int tmp = cur[0];
    for (int i = 1; i < cur.length; i++) {
      tmp = Math.max(tmp + cur[i], cur[i]);
      result = Math.max(result, tmp);
    }
    return result;
  }
}

```