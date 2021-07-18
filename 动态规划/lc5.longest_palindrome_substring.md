


```java
class Solution {
    public String longestPalindrome(String s) {
        int n = s.length();
        String res = null;
        boolean[][] dp = new boolean[n][n];
        // dp(i, j) represents whether s(i...j) can form a palindromic substring, dp(i, j) is true when s(i) equals to s(j)
        // and s(i + 1... j - 1) is a palindromic substring
        int i, j;
        for (i = n - 1; i >= 0; i--) {
            for (j = i; j < n; j++) {
                dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);
            
            if (dp[i][j] && (res == null || j - i + 1 > res.length())) {
                res = s.substring(i, j + 1);
            }
            }
        }
        return res;
    }
}
```