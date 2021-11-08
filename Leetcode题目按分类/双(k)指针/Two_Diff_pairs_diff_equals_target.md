- 2-diff, how many pairs diff = target (< target, > target), where target > 0


  - v1. array is sorted - assume no duplicate
    - (1,2,3,4) target = 2, return 2
    - solution: sliding window
      - 分解所有的pair: i < j
        - 固定j:
          - for all j:
              - check if there is any i < j, such that array[i] + target == array[j]
      - 为什么这个方法不会漏解：  j -> move right,  is is guarantee not moving left(stay or move right)   



  - v2, array is sorted - assume no duplicate, 求array[j] - array[i] > target的所有pairs
    - for each j, find the right most i, array[j] - array[i] > target 最后一个满足要求的i,  写对代码的前提是把所有的case想清楚, 找对物理意义，一直保持循环不变量,所有的corner case都要讨论清楚

```java
int count = 0;
int left = 0;
int right = 1;

while (right < array.length>) {  // fore ach j.
  whiel (right + 1 < array.length && array[j] - array[i + 1] > target) {
    i++;
  }
  // we ned to handle the corner case where there is no applicable i for the current j.
  if (array[j] - array[i] > target) count += i + 1;
  right++;
}
return count;

```
      - 物理意义的把握：上面这个写法总要看当前index的后面一个，而且还有一个容易忽略的Cornercase容易忘掉，这个题找第一个不满足条件的index也可以：
      - find left most i, such that aray[j] - array[i] <= target,这个写法简单一些，因为不需要进行加1的check
  ```java


  ```