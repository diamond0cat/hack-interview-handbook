分情况讨论：

a >0  b>0

a>0 b<0    取倒数

a<0 b>0    都变成正数再去算

a<0 b<0   


a==0 b==0

先把edge case写出来，体现能考虑到edge case




```java
class Solution {
    public double myPow(double x, int n) {
       // x == 0 n == 0
       if (x == 0 && n == 0) throw new IllegalArgumentException("invalid op");
      
        if (n == 0) return 1;
      
        if (n < 0) {
            return 1.0 / helper(x, -n);
        }
        return helper(x, n);
    }
    private double helper(double x, long n) {
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
