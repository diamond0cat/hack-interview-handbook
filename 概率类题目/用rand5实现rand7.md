rand()随机等概率的返回一个0~32767 当中的任何一个数

nextInt()都是在rand()的基础上实现出来的，用一个范围定死了的随机生成器来做出一个范围可变的随机生成器
keep calling random7() untilt he return value is between 0 and 4


0,1,2,3,4,5,6
只要是5，6就再试一次



```java

public class Solution {
  public int random7() {
    // you can use RandomFive.random5() for generating
    // 0 - 4 with equal probability.
    while (true) {
      int random = 5 * RandomFive.random5() + RandomFive.random5();
      if (random < 21) {  //0 到20,所以只浪费了21,22,23,24四个数
        return random % 7;  
      }
    }
  }
}

```
只管0~6可以但是慢:
![picture 9](https://i.loli.net/2021/09/20/cETtlx2jMG1C5Qd.png)  



high * 5 + low ==> random25() 而且一定是随机等概率的

可以取7的倍数: 0~20一共21个数： 0~6， 7~13， 14~20
![picture 8](https://i.loli.net/2021/09/20/V8n7sBHcXmpOwhy.png)  




0---20
%7== 0  ==> 0, 7,14   //任何一个group都只有三个数
%7==1 =>  1, 8, 15
....
%7== 6 => 6, 