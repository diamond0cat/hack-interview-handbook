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
      if (random < 21) {  //0 到20
        return random % 7;  
      }
    }
  }
}

```


0---20
%7== 0  ==> 0, 7,14   //任何一个group都只有三个数
%7==1 =>  1, 8, 15
....
%7== 6 => 6, 