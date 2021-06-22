

### 前缀和差分问题分类汇总


本文总结了力扣上 2000 题以内的关于前缀和的 44 道题，思路接近的题放到了一期。刷完这份题目列表，力扣范围内的前缀和问题可以说刷爆了

### 0 基础前缀和

303 [区域和检索-数组不可变](https://leetcode.com/problems/range-sum-query-immutable/)
简单前缀和, 注意数组下标

```java
class NumArray {
    int[] nums;
    int[] s;
    
    public NumArray(int[] nums) {
        this.nums = nums;  
        int len = nums.length;
        s = new int[len + 1];
        
        for (int i = 1; i <= len; i++) {
            s[i] = s[i - 1] + nums[i - 1];
        }
    }
    
    public int sumRange(int left, int right) {
        return s[right +1] - s[left];
    }
}
```

304.[Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/)

二维前缀和

```java
class NumMatrix {
    private int[][] sum;
    
    public NumMatrix(int[][] matrix) {
        sum = new int[matrix.length][matrix[0].length];
        
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                sum[i][j] = getSum(i - 1, j) + getSum(i, j - 1) - getSum(i - 1, j - 1) + matrix[i][j];
            }
        }
    }
    
    public int sumRegion(int row1, int col1, int row2, int col2) {
        return getSum(row2, col2) - getSum(row1 - 1, col2) - getSum(row2, col1 - 1) + getSum(row1 - 1, col1 -1);
    }
    private int getSum(int i, int j) {
        if (i >= 0 &&j >= 0) return sum[i][j];
        return 0;
    }
}
```

###  1 频数前缀和

