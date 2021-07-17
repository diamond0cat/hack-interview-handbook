

枚举两个坐标这种题目，想一下两个数的顺序有没有关系？？？
如果顺序没有关系，比如num[i] + nums[j] 跟nums[j] +nums[i]
我们可以加个条件： j < i 这样不影响答案

假设只有一种solution，或者只用返回任意一组解
相同的元素(下标相同)不能重复使用，数组中可能有重复的值，如果下标不同，看做不同的元素





### 朴素解法
- 由于我们每次要从数组中找两个数。

* 因此一个很简单的思路是：使用两重循环枚举下标 i 和 j ，分别代表要找的两个数。

* 然后判断 $nums[i] + nums[j] == target$ 是否成立。

* 另外为了防止得到重复的解，我们需要在第一层循环中让 i 从 0 开始，到 n - 2 结束（确保能取到下一位数作为 j ）；在第二层循环中让 j 从 i + 1 开始，到 n - 1 结束。
```java
class Solution {
    public int[] twoSum(int[] nums, int t) {
        int n = nums.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (t == nums[i] + nums[j]) return new int[]{i,j};
            }
        }
        return new int[]{};
    }
}
```
* 时间复杂度：两重循环，时间复杂度(n^2) 空间复杂度O(1)


method 1: 哈希
