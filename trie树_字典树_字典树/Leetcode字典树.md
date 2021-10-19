
- trie, 前缀树，字典树都是同一个东西

- trie是多叉树, 堆和线段树都是二叉树

- trie是一个专门为字典设计的数据结构，trie专门用来处理字符串

- trie的pros and cons

  - pros:
  - cons:
  - 
![picture 5](https://i.loli.net/2021/10/20/2RMJjbPlzoLCGm4.png)  



![picture 13](https://i.loli.net/2021/09/16/CWajEZ79fXTovmQ.png)  

### 注意： 我们应该把字母标记在edge上， 因为在下到下一层之前，就已经知道字母是什么了,才可能通过映射找到下一个节点，每个节点我们不存储char的信息是没有问题的，映射中有从char到node的映射


```
● Trie 本身携带的内容仅仅只是 isWord 这样一个布尔型变量，而沿着 next 指针一路走下来的路径，就能表示一个单词。
● 能匹配这件事情，是体现在边上的。
```

```java
public class Trie {
    private class Node {
        public boolean isWord;       // isWord 表示沿着根结点往下走，走到这个结点的时候是否是一个单词的结尾
        public TreeMap<Character, Node> next;   // 因为这里不涉及排序操作，用哈希表也是可以的
        public Node(boolean isWord) {
            this.isWord = isWord;
            next = new TreeMap<>();
        }
        public Node() {
            this(false);
        }
    }
    private Node root;
    private int size;

    public Trie() {
        root = new Node();
        size = 0;
    }

    public int getSize() {
        return size;
    }


    public void add(String word) {
        // root 是当前 Trie 对象的属性
        Node currNode = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (currNode.next.get(c) == null) {  //不存在才添加，否则这个block不执行
                currNode.next.put(c, new Node());
            }
            currNode = currNode.next.get(c);
        }
        // 如果已经添加过，才将 size++
        if (!currNode.isWord) {
            currNode.isWord = true;
            size++;
        }
    }
    // 下面这个方法查询整个单词在 Trie 中是否存在，所以在路径匹配完成以后，一定不要忘了判断匹配到的那个结点的  isWord 属性，如果它是一个单词的结尾，才返回 True
    public boolean contains(String word){ //整体逻辑和添加的过程是一致的，如果没有找到某一个字符，直接returnfalse
        Node currNode = root;
        Character currC;
        for (int i = 0; i < word.length(); i++) {
            currC = word.charAt(i);
            if(currNode.next.get(currC)==null){
                return false;
            }
            currNode = currNode.next.get(currC);
        }
        return currNode.isWord;
    }
}
```

leetcode上49道关于trie的题

| 状态 | 题目                                 | 通过率 | 难度 | 出现频率 | 完成度    |
| ---- | ------------------------------------ | ------ | ---- | -------- | --- |
|      | 139. 单词拆分                        | 51.4%  | 中等 |          |     |
|      | 208. 实现 Trie (前缀树)              | 71.6%  | 中等 |          |  r1   |
|      | 440. 字典序的第K小数字               | 38.0%  | 困难 |          |     |
|      | 692. 前K个高频单词                   | 57.9%  | 中等 |          |     |
|      | 421. 数组中两个数的最大异或值        | 62.2%  | 中等 |          |     |
|      | 386. 字典序排数                      | 74.8%  | 中等 |          |     |
|      | 1707. 与数组中元素的最大异或值       | 50.3%  | 困难 |          |     |
|      | 212. 单词搜索 II                     | 45.1%  | 困难 |          |     |
|      | 616. 给字符串添加加粗标签            | 46.1%  | 中等 |          |     |
|      | 336. 回文对                          | 40.1%  | 困难 |          |     |
|      | 820. 单词的压缩编码                  | 50.7%  | 中等 |          |     |
|      | 面试题 17.13. 恢复空格               | 55.3%  | 中等 |          |     |
|      | 140. 单词拆分 II                     | 48.6%  | 困难 |          |     |
|      | 面试题 17.15. 最长单词               | 40.3%  | 中等 |          |     |
|      | 211. 添加与搜索单词 - 数据结构设计   | 48.2%  | 中等 |          |     |
|      | 面试题 17.25. 单词矩阵               | 50.9%  | 困难 |          |     |
|      | 1803. 统计异或值在范围内的数对有多少 | 40.8%  | 困难 |          |     |
|      | 面试题 17.17. 多次搜索               | 44.2%  | 中等 |          |     |
|      | 792. 匹配子序列的单词数              | 45.2%  | 中等 |          |     |
|      | 758. 字符串中的加粗单词              | 45.9%  | 中等 |          |     |
|      | 1858. 包含所有前缀的最长单词         | 64.8%  | 中等 |          |     |
|      | 588. 设计内存文件系统                | 42.3%  | 困难 |          |     |
|      | 1948. 删除系统中的重复文件夹         | 51.3%  | 困难 |          |     |
|      | 642. 设计搜索自动补全系统            | 48.9%  | 困难 |          |     |
|      | 1804. 实现 Trie （前缀树） II        | 57.3%  | 中等 |          |     |
|      | 720. 词典中最长的单词                | 48.6%  | 简单 |          |     |
|      | 1233. 删除子文件夹                   | 48.2%  | 中等 |          |     |
|      | 1268. 搜索推荐系统                   | 58.3%  | 中等 |          |     |
|      | 648. 单词替换                        | 58.4%  | 中等 |          |     |
|      | 425. 单词方块                        | 61.2%  | 困难 |          |     |
|      | 472. 连接词                          | 40.3%  | 困难 |          |     |
|      | 527. 单词缩写                        | 57.7%  | 困难 |          |     |
|      | 676. 实现一个魔法字典                | 58.8%  | 中等 |          |     |
|      | 677. 键值映射                        | 61.7%  | 中等 |          |     |
|      | 745. 前缀和后缀搜索                  | 39.1%  | 困难 |          |     |
|      | 1065. 字符串的索引对                 | 53.9%  | 简单 |          |     |
|      | 1023. 驼峰式匹配                     | 56.6%  | 中等 |          |     |
|      | 1032. 字符流                         | 39.6%  | 困难 |          |     |
|      | 1166. 设计文件系统                   | 48.6%  | 中等 |          |     |
|      | 1316. 不同的循环子字符串             | 43.8%  | 困难 |          |     |
|      | 1178. 猜字谜                         | 46.2%  | 困难 |          |     |
|      | 1698. 字符串的不同子字符串个数       | 54.7%  | 中等 |          |     |
|      | 面试题 16.02. 单词频率               | 76.5%  | 中等 |          |     |
|      | 剑指 Offer II 062. 实现前缀树        | 73.1%  | 中等 |          |     |
|      | 剑指 Offer II 063. 替换单词          | 71.9%  | 中等 |          |     |
|      | 剑指 Offer II 064. 神奇的字典        | 61.4%  | 中等 |          |     |
|      | 剑指 Offer II 065. 最短的单词编码    | 61.9%  | 中等 |          |     |
|      | 剑指 Offer II 066. 单词之和          | 62.7%  | 中等 |          |     |
|      | 剑指 Offer II 067. 最大的异或        | 63.2%  | 中等 |          |     |
