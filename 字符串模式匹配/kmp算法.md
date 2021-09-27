

- brute force:枚举开始位置和结束位置， 比较substring和target string是否相等， tc = O(n * m)

- kmp算法可以做到仅仅后移模式串，比较指针不用回溯

- kmp大致思路： 指针从下标从1开始比较方便，前面补上一个空格
  - next[i] : 所有P[1...i]的相等的前缀和后缀中长度的最大值，这里指的非平凡前缀和后缀，平凡前缀和后缀指的是本身


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