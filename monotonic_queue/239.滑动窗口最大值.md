##  找冗余

1 3 [-1, -3, 5] 3 6 7 
// 时间： expire_time(-1)  <expire_time(-3)<expire_time(5)
// 值大小  
// 求max

只要5在，-1和-3都不可能是max这个解
expire_time和值大小都是5最优


### 冗余：
- 一个j和一个i,如果i < j,同时nums[i] <= nums[j]，i是冗余

1， [3，  -1,  -3]  -5，  3， 6，7   //当前3是最好

1，  3,     [-1,  -3 , -5]， 3， 6，7    //当前-1最好

如果一个值比较大，但是它出界的比较早，那么当它出界以后，那么他后面的会变成新的max
只要发生了递增，5进来了，前面的元素先出界还没有5好，所以是冗余

维护一个递减序列，窗口移动
只要递增，前一个就是冗余了
值大小有顺序，时间也有顺序




```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
         // 双端队列，存下标(代表时间)
        Deque<Integer> q = new ArrayDeque<>();
        int len = nums.length;
        int[] res = new int[len - k +1];
        
        
        for (int i = 0; i < nums.length; i++) {
            // 保证队头合法性
            while (!q.isEmpty() && q.peekFirst() <= i - k) q.pollFirst();
            // 维护队列单调性，插入新的选项
            while (!q.isEmpty() && nums[q.peekLast()] <= nums[i]) q.pollLast();
            
            q.offerLast(i);
            
            //取队头更新答案
            if (i >= k - 1) res[i - (k - 1)] = nums[q.peekFirst()];
            
        }
        return res;
    }
}

/*1 3 [-1 -3 5] 3 6 7
时间：expire_time(-1) < expire_time(-3) < expire_time(5)
值大小：-1 < -3 < 5
求max

冗余：一个下标i一个下标j，如果i<j，并且nums[i]<=nums[j]，i是冗余
去除冗余：维护下标（时间）递增、nums递减（>=）的队列
队头最优，随着下标增长，队头expire后，后面的开始逐渐变成最优*/

```