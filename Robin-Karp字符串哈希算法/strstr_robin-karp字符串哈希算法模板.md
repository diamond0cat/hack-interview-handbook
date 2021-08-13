如果我们可以对字符串进行哈希，那么我们也可以对树、图这些结构进行哈希

![20210811165622](https://i.loli.net/2021/08/12/7x1zq5Zd9IW6Oan.png)

java/cpp中，如果算数越界了，不是截断，是取模。可以自己试一下
做个试验：开个unsigned int 32位，算一下2^32 +1,其实等于1



2^32 + 1 等于1

取一个1，奇数个3，再加一个1，是一个hash的质量非常高的取法

为什么p取2^64 或者 2^32,因为无符号unsigned int 64的上界是2^64，如果算术溢出了，会怎么办？

语言里，python除外，java和cpp如果算术越界了，不是阶段，其实是取模

![20210811231838](https://i.loli.net/2021/08/12/okm7OiBb3LyDsQP.png)


![20210811232143](https://i.loli.net/2021/08/12/cOviIm1PxuCspSR.png)
java , cpp认为这些数形成一个环，  2147483647+1 = -2147483648

如果用unsigned int：
![20210811232456](https://i.loli.net/2021/08/12/z3DVI1e2SWjA6Lc.png)
返回0


![20210811233134](https://i.loli.net/2021/08/12/QnNWIJriPuREptb.png)

![20210812142612](https://i.loli.net/2021/08/13/uGajNVIcQg6rRlS.png)

```java
class Solution {
    public int strStr(String s, String t) {
        if (t.length() == 0) return 0;
        int n = s.length();
        int m = t.length();
        s = " " + s;
        t = " " + t;

        int p = (int)1e9 + 7; // 10^9+7 是一个质数
        long tHash = 0;
        for (int i = 1; i <= m; i++)
            tHash = (tHash * 131 + (t.charAt(i) - 'a' + 1)) % p;  //a必须映射为1，不能映射为0,否则ab与aab的值就会算出一个值
        // 模板：预处理前缀Hash
        long[] sHash = new long[n + 1];  //1到n一共n个
        sHash[0] = 0;
        long[] p131 = new long[n + 1]; // 131的次幂
        p131[0] = 1;
        for (int i = 1; i <= n; i++) {
            sHash[i] = (sHash[i - 1] * 131 + s.charAt(i) - 'a' + 1) % p;
            p131[i] = p131[i - 1] * 131 % p;
        }
        // hello
        // ll
        for (int i = m; i <= n; i++) { // 滑动窗结尾
            // s[i-m+1 ~ i] 与 t[1..m] 是否相等
            if (calcHash(sHash, p131, p, i - m + 1, i) == tHash &&
                s.substring(i - m + 1, i + 1).equals(t.substring(1))) {
                return i - m; // 下标变回0开始
            }
        }
        return -1;
    }

    // 模板：O(1)得到子串[l..r]的Hash值
    private long calcHash(long[] H, long[] p131, int p, int l, int r) {
        // hello 的子串ll的hash值
        //  hell
        // -he00
        // =  ll
        return ((H[r] - H[l - 1] * p131[r - l + 1]) % p + p) % p; //这里有负号，需要+p再模p,不取模这里会爆掉,这里其实不用专门存p131这个数组，直接把131的m次方算出来就可以
    }
}
```