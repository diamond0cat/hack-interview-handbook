
givne a new community with certain amount of store locations, input is 
a two dimension array:

   bookstore   restaurant   autoshop   market
1    30k            15k       5k        22k
2    7k            20k        3k        25k
3     5k            5k        20k       3k


constraint:you can not have the same type of business at adjacent location


dp:

1     30k               15k                   5k       22k

2      7k+22k          20k+30k           3k+30k       25k+30k


3      5k+(25k+30k)    5k+(25k+30k)      20k+(25k+30k)   3k+(20k+30k)       ==>取个max



```java
public int maximumRevenue(int[][] revenue) {

    int m = revenue.length;
    int m = reenue[0].length;

    int[][] dp = new int[m][n];

    

}



```