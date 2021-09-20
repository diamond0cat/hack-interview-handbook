

![picture 18](https://i.loli.net/2021/09/16/VoCT8k6HiWt5GRL.png)  



brute froce:  枚举第一刀(第一刀可以切在任何地方)....第n刀


求所有可能的切法中最大的Product是多少

至少要切一刀


- 方法一： 暴力dfs,列出所有可能
  - 列出所有情况，找出乘积最大的那个解
    - 设F(n)为长度为n的绳子可以得到的最大乘积，对于每个F(n), 可以得到如下分解：

![picture 19](https://i.loli.net/2021/09/17/oAkN2niLQve9zOd.png)  

    - 从上图我们可以把求解F(n)的问题分解成求解F(n-1)的问题，以此类推，直到求解到F(2)时，F(2)=1,递推回去，问题就得到了解决，这就是分治的思想
    - 分治思想的解决方法往往是递归，注意到我们每次将一段绳子剪成两段时，剩下的部分也可以继续剪，也可以不剪，了因此我们得到了递归函数F(n)= max(i * (n-i), i*F(n-i))   i = 1, 2, ......n-2

    - time = O(n!)  space=O()

- 方法二：记忆化搜索(自顶向下)
    - 上面的方法重复计算了F(n),为了避免重复计算，可以使用Memoization

    - time = O(n!) space = O(n) //使用数组f
    - 
- 方法三：DP  (自底向上)
    - 从已知的F(2)逐步迭代到目标值F(n),这是一种自底向上的方法
    - 建立一维数组dp：  
      - 1米长的绳子invalid不能切: invalid
      - 2米：一种切法： dp[2]= 1
      - base case : dp[1]= dp[2] = 1,表示长度为2的绳子的最大乘积为1
      - 状态转移方程: dp[i] = max(dp[i],  max((i-j)*j, dp[i-j] * j))
      - time = O(n^2) space = O(n)


![picture 20](https://i.loli.net/2021/09/17/8z4lpkHfgV9jnuy.png)  


- 方法四： DP的空间优化  https://leetcode-cn.com/problems/jian-sheng-zi-lcof/solution/xiang-jie-bao-li-di-gui-ji-yi-hua-ji-zhu-dong-tai-/


