树状数组或二叉索引树（Binary Indexed Tree），又以其发明者命名为 Fenwick 树。其初衷是解决数据压缩里的累积频率的计算问题，现多用于高效计算数列的前缀和、区间和。

它可以O(logn) 的时间得到任意前缀和
![picture 6](https://i.loli.net/2021/10/26/nkXJydPpTbDeSCU.png)  



并同时支持在 O(\log n)O(logn) 时间内支持动态单点值的修改。空间复杂度 O(n)O(n)。



| 状态 | 题目 | 通过率 | 难度 | 出现频率 |
| --- | --- | --- | --- | --- |
|  | 218. 天际线问题 | 54.2% | 困难 |  |
|  | 307. 区域和检索 - 数组可修改 | 53.8% | 中等 |  |
|  | 308. 二维区域和检索 - 可变 | 61.1% | 困难 |  |
|  | 315. 计算右侧小于当前元素的个数 | 41.8% | 困难 |  |
|  | 327. 区间和的个数 | 42.1% | 困难 |  |
|  | 493. 翻转对 | 34.6% | 困难 |  |
|  | 2031. Count Subarrays With More Ones Than Zeros | 65.2% | 中等 |  |
|  | 673. 最长递增子序列的个数 | 43.6% | 中等 |  |
|  | 683. K 个关闭的灯泡 | 43.5% | 困难 |  |
|  | 1157. 子数组中占绝大多数的元素 | 32.1% | 困难 |  |
|  | 1395. 统计作战单位数 | 74.8% | 中等 |  |
|  | 1409. 查询带键的排列 | 80.6% | 中等 |  |
|  | 1505. 最多 K 次交换相邻数位后得到的最小整数 | 36.1% | 困难 |  |
|  | 1649. 通过指令创建有序数组 | 47.4% | 困难 |  |
|  | 1756. 设计最近使用（MRU）队列 | 79.9% | 中等 |  |
|  | 1964. 找出到每个位置为止最长的有效障碍赛跑路线 | 38.6% | 困难 |  |
|  | LCP 05. 发 LeetCoin | 20.0% | 困难 |  |
|  | 剑指 Offer 51. 数组中的逆序对 | 48.3% | 困难 |  |
|  | 面试题 10.10. 数字流的秩 | 62.3% | 中等 |  |



|   | # | Title | Acceptance | Difficulty | Frequency |
| --- | --- | --- | --- | --- | --- |
|  | 218 | The Skyline Problem | 37.8% | Hard |  |
|  | 307 | Range Sum Query - Mutable | 38.1% | Medium |  |
|  | 308 | Range Sum Query 2D - Mutable | 39.9% | Hard |  |
|  | 315 | Count of Smaller Numbers After Self | 42.0% | Hard |  |
|  | 327 | Count of Range Sum | 36.0% | Hard |  |
|  | 493 | Reverse Pairs | 28.8% | Hard |  |
|  | 2031 | Count Subarrays With More Ones Than Zeros | 55.4% | Medium |  |
|  | 673 | Number of Longest Increasing Subsequence | 39.6% | Medium |  |
|  | 683 | K Empty Slots | 36.5% | Hard |  |
|  | 1157 | Online Majority Element In Subarray | 41.7% | Hard |  |
|  | 1395 | Count Number of Teams | 70.9% | Medium |  |
|  | 1409 | Queries on a Permutation With Key | 82.5% | Medium |  |
|  | 1505 | Minimum Possible Integer After at Most K Adjacent Swaps On Digits | 36.8% | Hard |  |
|  | 1649 | Create Sorted Array through Instructions | 37.0% | Hard |  |
|  | 1756 | Design Most Recently Used Queue | 77.5% | Medium |  |
|  | 1964 | Find the Longest Valid Obstacle Course at Each Position | 43.5% | Hard |  |
