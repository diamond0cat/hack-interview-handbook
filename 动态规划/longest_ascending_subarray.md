

一维dp


```java
    public int cuttingRope(int n) {
        int[] dp = new int[n +1];
        dp[0] = 0;
        dp[1] = 1;

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




```

注‌：‌这‌道‌题‌也‌可‌以‌从‌ ‌Sliding‌ ‌window‌ ‌的‌角‌度‌来‌思‌考‌ ‌(essentially‌ ‌it‌ ‌is‌ ‌similar‌ ‌
to‌ ‌DP’s‌ ‌principle)‌ ‌
public‌ ‌class‌ ‌‌LongestAscendingSubArray‌‌ ‌{‌ ‌
    public‌ ‌int‌ ‌longest(int[]‌ ‌nums)‌ ‌{‌ ‌
        //‌ ‌invalid‌ ‌input‌ ‌
        if‌ ‌(nums‌ ‌==‌ ‌null)‌ ‌{‌ ‌
            return‌ ‌-1;‌ ‌
        }‌ ‌
        if‌ ‌(nums.length‌ ‌==‌ ‌0)‌ ‌{‌ ‌
            return‌ ‌0;‌ ‌
        }‌ ‌
        int‌ ‌result‌ ‌=‌ ‌1;‌ ‌
        for‌ ‌(int‌ ‌i‌ ‌=‌ ‌0,‌ ‌left‌ ‌=‌ ‌0;‌ ‌i‌ ‌<‌ ‌nums.length;‌ ‌i++)‌ ‌{‌ ‌
            //‌ ‌if‌ ‌ascending,‌ ‌maintain‌ ‌the‌ ‌result‌ ‌
            if‌ ‌(i‌ ‌==‌ ‌0‌ ‌||‌ ‌nums[i]‌ ‌>‌ ‌nums[i‌ ‌-‌ ‌1])‌ ‌{‌ ‌
               result‌ ‌=‌ ‌Math.max(result,‌ ‌i‌ ‌-‌ ‌left‌ ‌+‌ ‌1);‌ ‌
            }‌ ‌else‌ ‌{‌ ‌
               left‌ ‌=‌ ‌i;‌ ‌
            }‌ 
        }‌ ‌
        return‌ ‌result;‌ ‌
    }‌ ‌
}‌ ‌
```