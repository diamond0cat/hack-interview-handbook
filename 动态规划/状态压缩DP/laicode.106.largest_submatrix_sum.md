
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

- solution 3: dp: prefix sum in 2D  ==> O(n^4)

- for x1
  - for y1
    - for x2
      - for y2
      - // 枚举左上角和右下角，O（1）的时间把子矩阵的矩阵和求出来


![picture 2](https://i.loli.net/2021/10/14/rLqH1lPZGSReyKk.png)  


- solution 4: 如果还想优化，只能放弃一部分的枚举了
  
  - 关键是怎么枚举：
    - for top row
      - for bottom row
      - // O(n)的方法来搞定呢


```
 1  2 3 4 5
-1  1 2 1 2
 3  1 2 1 3

```
- top = 0, bottom = 1
![picture 3](https://i.loli.net/2021/10/14/XZ72LfitVmJkqBz.png)  

- top和bottom都定下来了，所以每列可以压缩一下，把每一列看成一个数就行了， top和bottom定了以后，完全可以把蓝色区域牌匾，我们只需要考虑每一列，而不用考虑每一列的每个格子，这样并不会丢掉任何信息， 这样一来，相当于在一维数组上求一个largest subarray sum

![picture 6](https://i.loli.net/2021/10/14/nsVpQJw6N5GAOXD.png)  


![picture 5](https://i.loli.net/2021/10/14/MaJVAUmLyo67nkI.png)  

- 这样一来，本来是一个二维的子矩阵，都可以一一对应成一个一维数组的subarray，这样只用枚举左边界y1和右边界y2,对应着在 0 3 5 5 7 这个数组上求largest subarray sum

![picture 7](https://i.loli.net/2021/10/14/B8x9Vsou3gDf416.png)  
