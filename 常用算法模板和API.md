快速排序模板
-

```java
public class Solution {
  public int[] quickSort(int[] array) {
      // Write your solution here
      if (array == null ||array.length <= 1) return array;
      quickSort(array, 0, array.length - 1);
      return array;
    }
    private void quickSort(int[] array, int left, int right) {
      if (left >= right) return;
      int pivotIndex = partition(array, left, right); // i <= pivotIndex ==> valu <= pivot, 
      quickSort(array, left, pivotIndex - 1);
      quickSort(array, pivotIndex + 1, right);
    }
      //所有<pivot的数放在pivot左边，所有>= pivot的数放在Pivot右边
    private int partition(int[] array, int left, int right) {
      int randomIndex = pickRandom(left, right);
      int pivot = array[randomIndex];
      swap(array, randomIndex, right);
      int leftIndex = left;
      int rightIndex = right- 1;
      while (leftIndex <= rightIndex) {
         if (array[leftIndex] <= pivot) {
           leftIndex++;
         } else if (array[rightIndex] > pivot) {
           rightIndex--;
         } else {
           swap(array, leftIndex, rightIndex);
           leftIndex++;
           rightIndex--;
         }
      }
      swap(array, leftIndex, right);
      return leftIndex;
    }
    private int pickRandom(int left, int right) {  // 2.....5    4
      return  left + (int)(Math.random() * (right - left + 1));
    }
    private void swap(int[] arr, int a, int b) {
      int tmp  = arr[a];
      arr[a] = arr[b];
      arr[b] = tmp;
    }
  
}

```




Rabin-karp (字符串哈希)是一种基于hash的高效的字符串搜索算法
- 

  - time = O(m + n)
  - 把字符串哈希当成一个筛选，如果match上hash，再做一次傻傻的比较，把字符串哈希当成一个screening筛选


![picture 2](https://i.loli.net/2021/09/08/GUgkD7lvy5cAFm4.png)  

- 滑动窗口往右滑的过程不停做乘法

- time = O(m+n) target string自己要算hash
- worst time: O(m*n)


- 选用的hash函数：
  - 把字符串看做一个b进制数(一个多项式), 计算它在(十进制下)对p取模的值
  - 举例： 取b =131, p = 2 ^ 64 （无符号64位整数的上界）， p也可以取个大质数, java和cpp中如果越界了，不是截断而是取模
    - 2147483647(equal to 231 − 1) + 1 =  -2147483648
    - 
  - 字符串foobar的hash值为: (a=1,b=2,f=6,o=15,r=18)
    - (6 * 131^5 + 15 * 131^4 + 15 * 131 ^3 + 2 * 131 ^ 2 + 1 * 131 + 18 ) mod 2 ^ 64
    - 选取b和p的值决定了hash函数的质量
    - 根据经验，b= 131, 13331 （1加上奇数个3然后1）等, p为大质数是，冲突概率极小
    - hash值相等时可以再比对一下两个字符串，避免hash碰撞问题
    - 取模运算具有分配律，可以对每项都取模，使得加起来的和更小


- java中把整数数据范围看成一个环
### -2147483648 -2147483647   ....... -1   0    1   ....  2147483647
- -2147483648 - 1 = 2147483647

- unsigned int下算术越界上溢相当于对2^32取模,好处是不用再手动模了

- 如何快速计算一个子串的hash值？
  - s = 'foobar'
  - 先计算6个前缀子串的hash值, O(n):
    - H[i] = Hash(s[0...i-1]) = (H[i-1] * b + s[i -1] ) mod p
    - 计算子串oba的hash值：
      - 相当于b进制下两个数做减法 (H[5] - H[2] * b^3)
      -    fooba
      -  - fo000
      -  =   oba
      -  Hash(s[l...r]) = (H[r+1] - H[l] * b ^ (r-l+1)) mod p ==> O(1)



```java

//时间复杂度： O(n), 计算哈希是复杂度O(L), 之后O(N- L)次循环，每次循环是常数复杂度

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


KMP模板
-

- next告诉我们：如果匹配失败了， 下一步调到哪里继续配

