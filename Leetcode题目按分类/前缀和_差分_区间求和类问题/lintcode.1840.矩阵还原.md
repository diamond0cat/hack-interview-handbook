


```java
public class Solution {
    /**
     * @param n: the row of the matrix
     * @param m: the column of the matrix
     * @param after: the matrix
     * @return: restore the matrix
     */
    private int[][] prefixSum;
    public int[][] matrixRestoration(int n, int m, int[][] after) {
        // after is a prefix sum matrix
        this.prefixSum = after;
        // matrix[i][j] = sum[i][j] - getSum(i - 1, j) - getSum(i, j - 1) + getSum(i - 1, j - 1) 
        int[][] arr = new int[n][m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                arr[i][j] = after[i][j] - getSum(i -1, j) - getSum(i, j - 1) + getSum(i - 1, j  - 1);
            }
        }
        return arr;

    }
    private int getSum(int i, int j) {
        if (i >= 0 && j >= 0) return prefixSum[i][j];
        return 0;
    }
}


```