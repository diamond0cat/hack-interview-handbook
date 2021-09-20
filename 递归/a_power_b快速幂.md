- 分情况讨论：  a^b

![picture 15](https://i.loli.net/2021/09/15/htoMINukAVqDrca.png)  



先把edge case写出来，体现能考虑到edge case
```java

class Solution {
    public double myPow(double x, int n) { // x分兩種情況： x==0 和x!=0
        // case 1:x ==0
        if (x == 0) {
            if (n <= 0) return 0.0;         // x == 0 , n <= 0 invalid
            else return 0;  // x == 0 n > 0
        }

        //case 2: x != 0 
        if (n <0)  return 1.0 / helper(x, -n);
        if (n == 0) return 1.0;
        return helper(x, n);

    }
    private double helper(double x, int n) {
        if (n == 0) return 1;
        if (n == 1) return x;

        double half = helper(x, n / 2);

        if (n % 2 == 0) return half * half;
        else return half * half *x;
    }
}

```
