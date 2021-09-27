- 思路：降维：按行降维


```java
public class Solution {
  public int largest(int[][] matrix) {
    int m = matrix.length;
    if (m == 0) {
      return 0;
    }
    int n = matrix[0].length;
    if (n == 0) {
      return 0;
    }
    int[][] leftUp = leftUp(matrix, m, n);
    int[][] rightDown = rightDown(matrix, m, n);
    return merge(leftUp, rightDown, m, n);
  }
  private int merge(int[][] leftUp, int[][] rightDown, int m, int n) {
    int res = 0;
    for (int i = 0; i < m; i++) {
      for (int j = 0; j < n; j++) {
        leftUp[i][j] = Math.min(leftUp[i][j], rightDown[i][j]);
        res = Math.max(res, leftUp[i][j]);
      }
    }
    return res;
  }
  
  private int[][] leftUp(int[][] matrix, int m, int n) {
    int[][] left = new int[m][n];
    int[][] up = new int[m][n];
    for (int i = 0; i < m; i++) {
      for (int j = 0; j < n; j++) {
        if (matrix[i][j] == 1) {
          if (i == 0 && j == 0) {
            left[i][j] = 1;
            up[i][j] = 1;
          } else if (i == 0) {
            up[i][j] = 1;
            left[i][j] = left[i][j - 1] + 1;
          } else if (j == 0) {
            left[i][j] = 1;
            up[i][j] = up[i - 1][j] + 1;
          } else {
            up[i][j] = up[i - 1] [j] + 1;
            left[i][j] = left[i][j - 1] + 1;
          }
        }
      }
    }
    merge(left, up, m, n);
    return left;
  }  
  private int[][] rightDown(int[][] matrix, int m, int n) {
    int[][] right = new int[m][n];
    int[][] down = new int[m][n];
    for (int i = m - 1; i >= 0; i--) {
      for (int j = n - 1; j >= 0; j--) {
        if (matrix[i][j] == 1) {
          if (i == m - 1 && j == n - 1) {
            right[i][j] = 1;
            down[i][j] = 1;
          } else if (i == m - 1) {
            down[i][j] = 1;
            right[i][j] = right[i][j + 1] + 1;
          } else if (j == n - 1) {
            right[i][j] = 1;
            down[i][j] = down[i + 1][j] + 1;
          } else {
            right[i][j] = right[i][j + 1] + 1;
            down[i][j] = down[i + 1][j] + 1;
          }
        }
      }
    }
    merge(right, down, m, n);
    return right;
  }
}

```