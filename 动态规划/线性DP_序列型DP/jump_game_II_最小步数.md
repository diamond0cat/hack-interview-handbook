
solution 1: 从右往左跳

```java
public class Solution {
  public int minJump(int[] array) {
    // Write your solution here
    // dp[i] represent the smallest steps 
    int n = array.length;
    int[] dp = new int[n];
    dp[n - 1] = 0;  // 已经站在终点，所以是0步
     
    for (int i = n - 2; i >= 0; i--) {
      if (array[i] + i >= n - 1) {
        dp[i] = 1;   //一步跳到终点
      } else {
        dp[i] = Integer.MAX_VALUE;
        for (int j = array[i]; j >= 1; j--) {
           if (dp[i +j] != Integer.MAX_VALUE) {
              dp[i] = Math.min(dp[i], dp[i + j] + 1);
           }
        } 
      }
    }

   if (dp[0] == Integer.MAX_VALUE) return -1;
    return dp[0];
  }
}

```

```java
public class Solution {
  public int minJump(int[] array) {
    // Write your solution here
    int length = array.length;
    // minJump record the min number of jumps from 0 to each of the indices.
    int[] minJump = new int[length];
    minJump[0] = 0;

    for (int i = 1; i < length; i++) {
      minJump[i] = -1;  // initialize as unreachable
      // 看i之前所有的index,如果能从0调到这个index,而且这个index能跳到i
      for (int j = i - 1; j >= 0; j--) { 
          if (j + array[j] >= i && minJump[j] != -1) {
            // 把历史上最小的存下来或者update
            if (minJump[i] == -1 || minJump[i] > minJump[j] + 1) {
              minJump[i] = minJump[j] + 1;
            }
          }
      }

    }
    return minJump[length - 1];
  }
}

```