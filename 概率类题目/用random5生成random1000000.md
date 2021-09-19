

```
Given a random generator RandomFive.random5(), the return value of RandomFive.random5() is 0 - 4 with equal probability. Use RandomFive.random5() to implement random1000().

同 random7 那道题, 我们需要产生一个比1000大的数, 那么在4个轴上选四个坐标, 最后创建出一个3000多的数.
每次call random5 5次，产生[0, 5^5 - 1 = 3124]，若>= 3000，重新产生，否则返回% 1000
舍弃尾巴, mod1000 就是所得.
```

```java
public class Solution {
	public int random1000() {
		int sample = -1;
		while (true) {
			sample = RandomFive.random5()*625+
				RandomFive.random5()*125+
				RandomFive.random5()*25+
				RandomFive.random5()*5+RandomFive.random5();
			if (sample<3000) {
				return sample%1000;
			}
		}
	}
}
```

```java
public class Solution {
  public int random1000() {
    // Write your solution here.
    // you can use RandomFive.random5() for generating
    // 0 - 4 with equal probability.
    while (true) {
      int num = 0;
      for (int i = 0; i < 5; i++) {
        num = num * 5 + RandomFive.random5();
      }
      if (num < 3000) {
        return num % 1000;
      }
    }
  }
}

//1000以5为底的对数:  4.292
```