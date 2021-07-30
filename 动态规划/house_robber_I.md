
```java
 time = O(n^2)的版本
    public int rob(int[] nums) {
        int len = nums.length;
        if (len == 1) return nums[0];
        
        int[] dp = new int[len]; // dp[i]表示largest amount could steal at index i
        int max = Integer.MIN_VALUE;
        dp[0] = nums[0];
        dp[1] = nums[1];
        max = Math.max(dp[0], dp[1]);
        for (int i = 2; i < len; i++) {
            dp[i] = Integer.MIN_VALUE;
            for (int j = 0; j <i - 1; j++) {
                dp[i] = Math.max(dp[i], dp[j]);
            }
            dp[i] += nums[i];
            max = Math.max(max, dp[i]);
        }
        return max;
    }


public int rob(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    // 子问题：
    // f(k) = 偷 [0..k) 房间中的最大金额

    // f(0) = 0
    // f(1) = nums[0]
    // f(k) = max{ rob(k-1), nums[k-1] + rob(k-2) }

    int N = nums.length;
    int[] dp = new int[N+1];
    dp[0] = 0;
    dp[1] = nums[0];
    for (int k = 2; k <= N; k++) {
        dp[k] = Math.max(dp[k-1], nums[k-1] + dp[k-2]);
    }
    return dp[N];
}


//空间优化

public int rob(int[] nums) {
    int prev = 0;
    int curr = 0;

    // 每次循环，计算“偷到当前房子为止的最大金额”
    for (int i : nums) {
        // 循环开始时，curr 表示 dp[k-1]，prev 表示 dp[k-2]
        // dp[k] = max{ dp[k-1], dp[k-2] + i }
        int temp = Math.max(curr, prev + i);
        prev = curr;
        curr = temp;
        // 循环结束时，curr 表示 dp[k]，prev 表示 dp[k-1]
    }

    return curr;
}

```