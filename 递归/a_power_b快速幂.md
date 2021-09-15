- 分情况讨论：  a^b
  - a>0   b>0    正常算
  - a>0   b<0    取倒数
  - a<0   b>0    都变成正数再去算
  - a<0   b<0  
  - a==0  b==0  invalid
  - a==0 b < 0  invalid
  - a==0 b > 0  return 0


先把edge case写出来，体现能考虑到edge case

![picture 15](https://i.loli.net/2021/09/15/htoMINukAVqDrca.png)  



```java
class Solution {
    public double myPow(double x, int n) {  //invalid的和一些corner case在main function里解决
       // x == 0 n == 0
       if (x == 0 && n == 0) throw new IllegalArgumentException("invalid op");
      
        if (n == 0) return 1;
      
        if (n < 0) {
            return 1.0 / helper(x, -n);
        }
        return helper(x, n);
    }
    private double helper(double x, long n) {  //Ok的情况在这里解决了
        if (n == 0) return 1;
        if (n == 1) return x;
      
        double half = helper(x, n/2);
      
        if (n %2 ==0) {
            return half * half;
        }
        return half * half * x;
    }
}
```
