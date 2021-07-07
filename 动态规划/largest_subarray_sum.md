

start from brute force




物理意义，开闭区间

dp[i] 表示[0, i] 这一段  (是否是闭区间按题目定)


try to find a valid induction rule:

第一步：dp[i] 表示[0, i]这一段的max subarray sum = max(array[i], dp[i -1] + array[i])

第二步：看最后一步:最后一步就是决定i-1在还是不在

     是否包含i-1:

     不包含i-1:  single element --> array[i]

     包含i-1：  dp[i - 1] + array[i]


推导base case //通过induction rule来推
dp[0]


优化： 通过哪个方面：
1.先考虑空间： 可以优化空间：这里的dp[i]只depend on dp[i - 1]


2. fill in order  : 如果是二维的情况，filling order不是唯一的

