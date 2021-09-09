

把字符串哈希当成一个筛选，如果match上hash，再做一次傻傻的比较，把字符串哈希当成一个screening筛选


![picture 2](https://i.loli.net/2021/09/08/GUgkD7lvy5cAFm4.png)  
滑动窗口往右滑的过程不停做乘法

time = O(m+n) target string自己要算hash
worst time: O(m*n)





