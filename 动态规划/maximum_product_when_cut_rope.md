

```java
    public int cuttingRope(int n) {
        int[] dp = new int[n +1];
        dp[0] = 0;
        dp[1] = 0;

        for (int i = 2; i <= n; i++) {
            int curMax = 0;

            for (int j = 1; j < i; j++) {
                curMax = Math.max(curMax, Math.max(j, dp[j]) * (i - j));
            }
            dp[i] = curMax;
        }
        return dp[n];
    }
```