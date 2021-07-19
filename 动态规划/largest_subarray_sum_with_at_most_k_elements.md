
这题考的依然是拆分

拆分+组合

试一试能不能用dp做，先用brute force来分析



```java
动态规划的的四个解题步骤是：

定义子问题
写出子问题的递推关系
确定 DP 数组的计算顺序
空间优化（可选）

```

### 步骤一：定义子问题
![20210718173430](https://raw.githubusercontent.com/corykingsf/hack-system-design-pixel/main/pictures/20210718173430.png)
这个题用prefix-sum更好做一些



### 步骤二：写出子问题的递推关系


![20210718173623](https://raw.githubusercontent.com/corykingsf/hack-system-design-pixel/main/pictures/20210718173623.png)

ending at index i
