![20210821172207](https://i.loli.net/2021/08/22/WcZIu3s1jGAft6O.png)


寻找桥的算法： dfs, 遍历的过程记录不同的信息，根据记录的信息组合出逻辑，从而求出答案
寻找桥的算法更难，因为记录的信息更多元

怎么更新信息，怎么维护信息，怎么使用信息

order数组记录遍历的顺序
low数组记录对每个顶点来说，通过它从另外一条路能到达的最低的那个order值



 


![20210821233823](https://i.loli.net/2021/08/22/pLrK982Sncs4EIu.png)
![20210821235122](https://i.loli.net/2021/08/22/GUHXbrxvkO1zYRt.png)



![20210821235302](https://i.loli.net/2021/08/22/4u9ACHrJBj7Ikdv.png)

![20210821235820](https://i.loli.net/2021/08/22/5ozygJVaCRPWFTk.png)


树是将图中所有顶点连接起来所用边数最少的情况，

![20210822111337](https://i.loli.net/2021/08/23/6kyIoFMcHX4DTzP.png)


图的遍历树: bfs遍历树，dfs遍历树

dfs遍历树：前向边和后向边，前向边：遍历树上的边，后向边：不在遍历树上的边

图中的后向边可以只想自己的祖先节点，我们就是利用这个特性找到图中的桥
![20210822103210](https://i.loli.net/2021/08/23/2dw6zTQ7FvNUI3J.png)

寻找割点:

![20210822222208](https://i.loli.net/2021/08/23/xBGgOks86vamDCH.png)

![20210822222438](https://i.loli.net/2021/08/23/9vbOVqNEhPY1TQl.png)