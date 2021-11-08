

把字符串哈希当成一个筛选，如果match上hash，再做一次傻傻的比较，把字符串哈希当成一个screening筛选


![picture 2](https://i.loli.net/2021/09/08/GUgkD7lvy5cAFm4.png)  
滑动窗口往右滑的过程不停做乘法

time = O(m+n) target string自己要算hash
worst time: O(m*n)


- robin-karp算法：
  - 使用robin-karp解决字符串匹配问题的思路：
    - 1.计算长度为m的模式串t的hash值hash_pattern  O(m)
    - 2.计算长度为n的文本串s中每个长度为m的子串的hash值，共需要计算n-m+1次
    - 3.比较每个子串和模式串的hash值，如果hash值不同，必然不匹配
    - 4.如果hash值相同，还需要使用朴素算法再次判断
    - 在hash选取较好的情况， time = O(m+n)

### 注意这里a不能看成0, 考虑这个例子: aab 和 ab 这两个数值上没有区别了，所以这里字母不能映射为0


```java


class Solution {
    public int strStr(String s, String t) {
        if (t.length() == 0) return 0;
        int n = s.length();
        int m = t.length();
        s = " " + s;
        t = " " + t;
        int p = (int)1e9 + 7;  // 10^9+7是一个质数
        long tHash = 0;
        for (int i = 1; i <=m; i++) {
            tHash = (tHash * 131 + (t.charAt(i) - 'a' + 1)) % p;
        }
        // 模板：预处理前缀hash
        long[] sHash = new long[n + 1]; 
        sHash[0] = 0;
        long[] p131 = new long[n + 1]; // 131的次幂
        p131[0] = 1;
        
        for (int i = 1; i <= n; i++) {
            sHash[i] = (sHash[i - 1] *131 + s.charAt(i) - 'a' + 1) % p;
            p131[i] = p131[i - 1] *131 % p;  //预处理所有进制的若干次幂，后面可以直接用
        }
        
        /*
        hello
        ll
        
        */
        for (int i = m; i <= n; i++) {
            if (calHash(sHash, p131, p, i - m + 1, i) == tHash &&
               s.substring(i - m + 1, i + 1).equals(t.substring(1))) {
                return i - m; // 下标变回从0开始
            }
        }
        return -1;
    }

   // 模板：O(1)得到子串[l..r]的Hash值
    private long calHash(long[] H, long[] p131, int p, int l, int r) {
        // hello的子串ll的hash值: 前r个字符减掉 he00
        //  hell
        // -he00
        // =  ll
        return ((H[r] - H[l - 1] * p131[r - l + 1]) % p + p ) % p;  //131的长度次方
    }
    }
}
```
