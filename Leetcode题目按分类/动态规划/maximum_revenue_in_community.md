


小偷偷钱问题
```
givne a new community with certain amount of store locations, input is 
a two dimension array:

   bookstore   restaurant   autoshop   market
1    30k            15k       5k        22k
2    35k            20k        3k        25k
3     40k            5k        20k       3k


constraint:you can not have the same type of business at adjacent location

dp:

1     30k                    15k                      5k       22k

2      35k+22k              20k+30k               3k+30k       25k+30k

 
3      40k+(25k+35k)        5k+57k                                        ==>取个max
       3号摊位开书店并且
      2号摊位不开书店的最大利润
```


dp[i][j] = Max()
```java
public int maximumRevenue(int[][] revenue) {

    int m = revenue.length;
    int m = reenue[0].length;

    int[][] dp = new int[m][n];

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            
            dp[i][j] = Math.max() + revenue[i][j];
        }
    }

}



```