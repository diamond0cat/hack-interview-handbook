

![picture 1](https://i.loli.net/2021/09/23/moaTA1DCZVEB6Qw.png)  


```java
public class Solution {
    /**
     * @param customers: the number of customers
     * @param grumpy: the owner's temper every day
     * @param X: X days
     * @return: calc the max satisfied customers
     */
    public int maxSatisfied(int[] customers, int[] grumpy, int X) {
        int n = grumpy.length;
        int satisfiedSum = 0;
        
        // 先统计原本就会给好评的人数
        for (int i = 0; i < n; i++) {
            if (grumpy[i] == 0) {
                satisfiedSum += customers[i];
            }
        }
        
        // 记录最多的可能会变好评的人数
        int maxBecomeSatisfied = 0;
        // 记录窗口中会变好评的人数
        int becomeSatisfied = 0;
        int left = 0;
        // 移动窗口的右端点
        for (int right = 0; right < n; right++) {
            if (grumpy[right] == 1) {
                becomeSatisfied += customers[right];
            }
            // 如果窗口中的个数过多，则移动窗口的左端点
            if (right - left + 1 > X) {
                if (grumpy[left] == 1) {
                    becomeSatisfied -= customers[left];
                }
                left++;
            }
            maxBecomeSatisfied = Math.max(maxBecomeSatisfied, becomeSatisfied);
        }
        return satisfiedSum + maxBecomeSatisfied;
    }
}
```
