

```java

Given an array, find the subarray (containing at least k numbers) which has the largest sum. 
Examples: 
 

Input : arr[] = {-4, -2, 1, -3} 
            k = 2
Output : -1
The sub array is {-2, 1}

Input : arr[] = {1, 1, 1, 1, 1, 1} 
            k = 2
Output : 6 
The sub array is {1, 1, 1, 1, 1, 1}
Asked in : Facebook 
```


method 1:DP

dp state:

induction rule:


```java
public‌ ‌class‌ ‌Solution‌ ‌{‌ ‌
 ‌
   ‌public‌ ‌int‌ ‌largestSubarraySum(int[]‌ ‌a,‌ ‌int‌ ‌k)‌ ‌{‌ ‌
       ‌int‌ ‌n‌ ‌=‌ ‌a.length,‌ ‌dp‌ ‌=‌ ‌0;‌ ‌
       ‌for‌ ‌(int‌ ‌i‌ ‌=‌ ‌0;‌ ‌i‌ ‌<‌ ‌k;‌ ‌i++)‌ ‌{‌ ‌
           ‌dp‌ ‌+=‌ ‌a[i];‌ ‌   //前k个元素加起来，因为要求at least k elements
       ‌}‌ ‌
       ‌int‌ ‌sumk‌ ‌=‌ ‌dp,‌ ‌max‌ ‌=‌ ‌dp;‌ ‌
       ‌for‌ ‌(int‌ ‌i‌ ‌=‌ ‌k;‌ ‌i‌ ‌<‌ ‌n;‌ ‌i++)‌ ‌{‌ ‌
           ‌sumk‌ ‌=‌ ‌sumk‌ ‌-‌ ‌a[i‌ ‌-‌ ‌k]‌ ‌+‌ ‌a[i];‌ ‌//case1:subarray with exactly k elements ending at index i, size为k的sliding window
           ‌dp‌ ‌=‌ ‌Math.max(sumk,‌ ‌dp‌ ‌+‌ ‌a[i]);‌ ‌//case1:subarrays with at least (K+1) elements ending at index, dp[i-1]+array[i]=at lease (K+1) elements ending at index i
           ‌max‌ ‌=‌ ‌Math.max(dp,‌ ‌max);‌ ‌
       ‌}‌ ‌
       ‌return‌ ‌max;‌ ‌
   ‌}‌ ‌
}‌ ‌
 ‌
Time‌ ‌O(n)‌ ‌
Space‌ ‌O(1)‌ ‌


method 2:sliding window


```