



```java
public class Solution {
  public long reverseBits(long n) {
    // Write your solution here
    // 32 bit integer
    int i = 0, j = 31;
    while (i < j) {
      n = reverseBit(n, i, j);   //这里翻转的是primitive type,所以这里一定要把交换完的值通过返回值弄出来
      i++;
      j--;
    }
    return n;
  }
  private long reverseBit(long x, int i, int j) {  //swap两个bit
    long left = ((x >> j) & 1L);   //把第i个bit扣出来
    long right = ((x >> i) & 1L);   //把第j个bit扣出来
    if (left != right) {
      x = x ^ (1L << i);  //第i位取反  （任何一个位异或0等于自己，任何一个位异或1等于取反）
      x = x ^ (1L << j);   //第j位取反
    }
    return x;
  }
}

```