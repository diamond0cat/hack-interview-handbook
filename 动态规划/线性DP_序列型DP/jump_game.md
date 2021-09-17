



```java
// 从右往左跳
public class Solution {
  public boolean canJump(int[] array) {
    // Write your solution here
    // from right to left
    // dp[i] represent if we could jump from i to array[len-1]

    int len = array.length;
    boolean[] dp = new boolean[len];

    dp[len - 1] = true;

    for (int i = len - 2; i >= 0; i--) {
        if (i + array[i] >= len - 1)  {dp[i] = true; continue;}
        for (int j = array[i]; j >= 1; j--) {
          if (dp[i +j]) {
            dp[i] = true;
            break;
          }
        }
    }

    return dp[0];
  }
}
```

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