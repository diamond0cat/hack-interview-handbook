
![picture 1](https://i.loli.net/2021/10/14/Ud7ehzLHauskMIj.png)  
![picture 2](https://i.loli.net/2021/10/14/U71v39NwcCHZEQl.png)  
- solution 1: brute force O(n^6)
    - there are O(n^4) submatrices
        - for for for for each submatrix, it takes O(n^2) to calculate its sum.
          - therefore total time = O(n^6)

- solution 2: DP1: prefix sum in 1D: 搞一个对每个列的prefix sum
![picture 3](https://i.loli.net/2021/10/14/gGlqemL53HdEIAZ.png)  


    - 物理意义： prefixSum[i][j] = a[0][j] + a[1][j] + a[2][j]+ ......+ a[i][j]
- pre-processing: O(n^2)
    - for i = 0; i < r; i++
      - for j = 0; j < c; j++
        - prefix[i][j] = prefix[i-1][j] + a[i][j]

// prefix[i-1][j] = a[0][j] + a[1][j] + ...+a[i - 1][j] +  a[i][j] = prefix[i][j]
                                                          

```
for x1
    for y1
        for x2
            for y2
                int sum = 0;
                for y = y1; y <= y2; y++:

                    // x1 == 0 小心处理越界
                    sum += prefixSum[x2][y] - prefixSum[x1 -1][y]
                global_max = max(global_max， sum);    
```
    - O(n^5)


- solution 3: dp: prefix sum in 2D  ==> O(n^4)


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