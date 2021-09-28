- KMP的价值：  「匹配失败过程中产生的“信息”，可以用于之后的匹配流程」这种思想是如何帮助我们做到「线性复杂度」的
 
- KMP 之所以能够在 [公式]复杂度内完成查找，是因为其能在「非完全匹配」的过程中提取到有效信息进行复用，以减少「重复匹配」的消耗。
- 你应该清楚 KMP 为什么相比于朴素解法更快：
  - 因为 KMP 利用已匹配部分中相同的「前缀」和「后缀」来加速下一次的匹配。
  - 因为 KMP 的原串指针不会进行回溯（没有朴素匹配中回到下一个「发起点」的过程）。


- brute force:枚举开始位置和结束位置， 比较substring和target string是否相等， tc = O(n * m)

- kmp算法可以做到仅仅后移模式串，比较指针不用回溯

- kmp大致思路： 指针从下标从1开始比较方便，前面补上一个空格
  - next[i] : 所有P[1...i]的相等的前缀和后缀中长度的最大值，这里指的非平凡前缀和后缀，平凡前缀和后缀指的是本身

### 最重要是把握next数组的物理意义： next存的是一个最长的长度len，是指前len个字符， 长度为len的前缀和长度为len的后缀相等，所有前缀和后缀相等的长度里面，最大的一个； next[1] = 0,求得时候next从2开始，匹配的时候next从1开始

![picture 3](https://i.loli.net/2021/09/28/iKhwUdkgnSAPzpJ.png)  

![picture 4](https://i.loli.net/2021/09/28/iqr4nuCAKflB6mg.png)  

![picture 5](https://i.loli.net/2021/09/28/nDF8MHcsOeSy2kw.png)  


![picture 6](https://i.loli.net/2021/09/28/8sv64czOnhTVRUD.png)  


```java
class Solution {
public:
    int strStr(string s, string p) {
        if (p.empty()) return 0;
        int n = s.size(), m = p.size();
        s = ' ' + s, p = ' ' + p;

        vector<int> next(m + 1);
        for (int i = 2, j = 0; i <= m; i ++ ) {
            while (j && p[i] != p[j + 1]) j = next[j];
            if (p[i] == p[j + 1]) j ++ ;
            next[i] = j;
        }

        for (int i = 1, j = 0; i <= n; i ++ ) {
            while (j && s[i] != p[j + 1]) j = next[j];
            if (s[i] == p[j + 1]) j ++ ;
            if (j == m) return i - m;
        }

        return -1;
    }
};

```



![picture 2](https://i.loli.net/2021/09/28/HTRmv7DFebwXOf2.png)  
