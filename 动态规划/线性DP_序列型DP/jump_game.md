


```java
//贪心的办法不好证明，不推荐
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        boolean[] dp = new boolean[n];
        
        dp[n - 1] = true;
        int lastPosition = n - 1;
        for (int i = n - 1; i >= 0; i--) {
            if (nums[i] + i >= lastPosition) {
                lastPosition = i;
            }
        }
        return lastPosition == 0;
    }
}
```