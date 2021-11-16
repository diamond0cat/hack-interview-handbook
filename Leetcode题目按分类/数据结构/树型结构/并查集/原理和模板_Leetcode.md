连通性问题的通解
-

并查集是一种建立在「数组」上的树形结构，并且这棵树的特点是孩子结点指向父亲结点
-
「并查集」主要用于解决「动态连通性」问题，重点关注的是连接问题，并不关注路径问题；
-

并查集」是树，所以优化的策略依然是和树的高度较劲，优化思路有「按秩合并」与「路径压缩」。
-

### 什么题目用并查集?   具有传递性，比较容易想到使用并查集。





### 动态判断图的连通性

* 堆的作用：在数据动态变化的情况下用最优的时间拿出max/min

1. 并查集： 孩子指向父亲形成的一种树结构,用来解决连接问题
2. 


* 并查集用来解决connectivity problem
* 给出图中两点，判断两点是否可以经由一条路径连接

* 非常快的判断网络中节点间的连接状态
* 并查集也是集合这一概念在数据结构中的实现，可以高效求并集

### 基于size的优化和基于rank的优化



### 连接问题和路径问题

* 如果我们只想知道a， b两点的连接状态，我们通过求解路径问题来知道连接状态其实消耗了额外的性能


并查集支持的操作：

union(p,q)

isConnected(p,q)  --> find(p) == find(q)  //find返回的是元素的group的ID


并查集可以有不同的底层实现


并查集接口:


```java
public interface UF {
    int getSize();
    boolean isConnected(int p, int q);
    void unionElements(int p, int q);
}
```

```java
public interface IUnionFind {

    // 并查集的版本名称，由开发者指定
    String versionName();

    // p (0 到 N-1)所在的分量的标识符
    int find(int p);

    // 如果 p 和 q 存在于同一分量中则返回 true
    boolean isConnected(int p, int q);

    // 在 p 与 q 之间添加一条连接
    void union(int p, int q);

}
```

使用ID数组来存储每个元素所属的集合是谁
-


quick find下的find() 时间是O(1), union的时间是O(n)

并查集第1版(quick-find实现)
-

```java
public class UnionFind1 implements IUnionFind {

    private int[] id; // 分量 id

    private int count; // 连通分量的数量

    public UnionFind1(int n) {
        this.count = n;
        // 初始化分量 id 数组
        id = new int[n];
        for (int i = 0; i < n; i++) {
            id[i] = i;
        }
    }

    @Override
    public String versionName() {
        return "并查集的第 1 个版本，基于 id 数组，quick-find";
    }

    // 以常数时间复杂度，返回分量的标识符，与并查集的规模是无关的，这一步很快
    // 因此我们称这个版本的并查集是 quick-find
    @Override
    public int find(int p) {
        return id[p];
    }

    @Override
    public boolean isConnected(int p, int q) {
        return find(p) == find(q);
    }

    // 因为需要遍历数组中的全部元素，所以这个版本其实效率并不高
    @Override
    public void union(int p, int q) {
        int pid = find(p);
        int qid = find(q);

        // 如果 p 和 q 已经在相同的分量之中，则什么都不做
        if (pid == qid) {
            return;
        }

        // 将 p 的分量重新命名为 q 的名称
        for (int i = 0; i < id.length; i++) {
            if (find(i) == pid) {
                id[i] = qid;
            }
        }
        // 每次 union 以后，连通分量减 1
        count--;
    }
}
```


并查集第2版(基于parent的并查集,非最终版本). quick-union
-

```
这一版「并查集」代码是最基本的「并查集」，我们需要学习思想，核心思想是「代表元法」，以「树」的「根结点」作为代表元。
后续我们介绍这一版代码的两个优化：
1、按秩合并（有 2 个版本）
2、路径压缩（有 2 个版本）
介绍得多，只是为了方便大家建立知识结构，真正我们只会使用一个版本的「并查集」。我们放在介绍完了以后再说。
```

```java
public class UnionFind2 implements IUnionFind {

    private int[] parent; // 第 i 个元素存放它的父元素的索引

    private int count; // 连通分量的数量

    public UnionFind2(int n) {
        this.count = n;
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;   //初始化时每个元素的父亲都是自己
        }
    }
    public String versionName() {
        return "并查集的第 2 个版本，基于 parent 数组，quick-union";
    }
    public int find(int p) {
        // 跟随链接找到根结点
        while (parent[p] != p) { // 只要不是根结点,就继续找父亲，只要找到为止
            p = parent[p];
        }
        return p;
    }
    public boolean isConnected(int p, int q) {
        return find(p) == find(q);
    }

    // union两个节点，把其中一个节点的根节点指向另一个节点的根节点就可以了
    public void union(int p, int q) {
        int pRoot = find(p); // 将 p 归并与之相同的分量中
        int qRoot = find(q); // 将 q 归并与之相同的分量中

        // 如果 p 和 q 已经在相同的分量之中，则什么都不做
        if (pRoot == qRoot) {
            return;
        }
        // 如果 parent[qRoot] = pRoot; 也是可以的，即将其中一个结点指向另一个结点
        parent[pRoot] = qRoot;
        // 每次 union 以后，连通分量减 1
        count--;
    }
}
```

并查集第3版(quikc-union基于size的优化)
-

```
这一版「并查集」代码是最基本的「并查集」，我们需要学习思想，核心思想是「代表元法」，以「树」的「根结点」作为代表元。
后续我们介绍这一版代码的两个优化：
1、按秩合并（有 2 个版本）
2、路径压缩（有 2 个版本）
介绍得多，只是为了方便大家建立知识结构，真正我们只会使用一个版本的「并查集」。我们放在介绍完了以后再说。
我们发现 union(4, 9) 与 union(9, 4) 其实是一样的，也就是把谁的根指向谁的根，这一点从正确性上来说是无关紧要的，但是对于 find 的时间复杂度就会有影响。为此，我们做如下优化。
在合并之前做判断，具体做法是，计算每一个结点有多少个元素直接或者间接地以它为根，我们应该将集合元素少的那结点的根指向集合元素多的那个结点的根。这样，形成的树就会更高概率地形成一棵层数较低的树。
为此，我们再引入一个 size 数组，size[i] 的定义是：以第 i 个结点为根的集合的元素的个数。
在初始化的时候 size[i] = 1，find 和 isConnected 操作中我们都不须要去维护 size 这个数组，唯独在 unionElements 的时候，我们才要维护 size 数组的定义。
```

```java
// union-find 算法的实现（加权 quick-union 算法）
public class UnionFind3 implements IUnionFind {

    private int[] parent; // 第 i 个元素存放它的父元素的索引

    private int count; // 连通分量的数量

    private int[] size; // 以当前索引为根的树所包含的元素的总数

    public UnionFind3(int n) {
        this.count = n;
        parent = new int[n];
        size = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            // 初始化时，所有的元素只包含它自己，只有一个元素，所以 size[i] = 1
            size[i] = 1;
        }
    }
    public String versionName() {
        return "并查集的第 3 个版本，基于 parent 数组，quick-union，基于 size";
    }
    // 返回索引为 p 的元素的根结点的索引
    public int find(int p) {
        // 跟随链接找到根结点
        while (p != parent[p]) {
            p = parent[p];
        }
        return p;
    }
    public boolean isConnected(int p, int q) {
        int pRoot = find(p);
        int qRoot = find(q);
        return pRoot == qRoot;
    }
    public void union(int p, int q) {
        int pRoot = find(p);
        int qRoot = find(q);
        if (pRoot == qRoot) {
            return;
        }
        // 这一步是与第 2 版不同的地方，我们不是没有根据地把一个结点的根结点的父结点指向另一个结点的根结点
        // 而是将小树的根结点连接到大树的根结点
        if (size[pRoot] > size[qRoot]) {
            parent[qRoot] = pRoot;
            size[pRoot] += size[qRoot];
        } else {
            parent[pRoot] = qRoot;
            size[qRoot] += size[pRoot];
        }
        // 每次 union 以后，连通分量减 1
        count--;
    }
}
```
并查集第4版(quick-union基于rank的优化):为什么不叫height叫rank?


```java
public class UnionFind4 implements IUnionFind {

    private int[] parent;

    private int count;

    // 以下标为 i 的元素为根结点的树的深度（最深的那个深度）
    private int[] rank;

    public UnionFind4(int n) {
        this.count = n;
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            // 初始化时，所有的元素只包含它自己，只有一个元素，所以 rank[i] = 1
            rank[i] = 1;
        }
    }
    public String versionName() {
        return "并查集的第 4 个版本，基于 parent 数组，quick-union，基于 rank";
    }

    // 返回下标为 p 的元素的根结点
    public int find(int p) {
        while (p != parent[p]) {
            p = parent[p];
        }
        return p;
    }
    public boolean isConnected(int p, int q) {
        int pRoot = find(p);
        int qRoot = find(q);
        return pRoot == qRoot;
    }
    public void union(int p, int q) {
        int pRoot = find(p);
        int qRoot = find(q);
        if (pRoot == qRoot) {
            return;
        }
        // 这一步是与第 3 版不同的地方
        if (rank[pRoot] > rank[qRoot]) {
            parent[qRoot] = pRoot;
        } else if (rank[pRoot] < rank[qRoot]) {
            parent[pRoot] = qRoot;
        } else {   //rank[qRoot] == rank[pRoot]
            parent[qRoot] = pRoot;
            rank[pRoot]++;
        }
        // 每次 union 以后，连通分量减 1
        count--;
    }
}
```


并查集第5版quick-union基于路径压缩的非递归实现: 路径压缩（隔代压缩）
-

![picture 1](https://i.loli.net/2021/10/19/1kDoqLuRz7ciVJS.png)  


```java
public int find(int p) {
    // 在 find 的时候执行路径压缩
    while (p != parent[p]) {
        // 编写这句代码的时候可能会觉得有点绕，
        // 画一个示意图，就能很直观地写出正确的逻辑
        // 两步一跳完成路径压缩
        parent[p] = parent[parent[p]];
        p = parent[p];
    }
    return p;
}
```

```
这一版代码用得最多。因为好理解，且代码量较少。
只用理解这一句即可 parent[p] = parent[parent[p]];，可以称之为「隔代压缩」。
虽然压缩不彻底，但是多压缩几次也就能够达到完全压缩的效果，且不使用递归，占用「递归栈」空间。

什么是路径压缩 path Compression？以上我们都是针对于 union 操作的优化，其实我们在 find 的时候，就可以对一棵树进行整理，让它的高度变低，这一点是基于并查集的一个特性：只要它们是连在一起的，其实谁指向谁，并不重要，所以我们在接下来的讨论中看到的并查集的表示图，它们是等价的，即它们表示的都是同一个并查集。

```
![picture 2](https://i.loli.net/2021/10/18/mjxDwV6yPsYcvBq.png)  


并查集第5版quick-union基于路径压缩的递归实现:
-

![picture 2](https://i.loli.net/2021/10/19/e3GQWratLZFKVsJ.png)  

```java
/**
 * 返回索引为 p 的元素的根结点
 * 理解这个方法的关键点：我们就是要把这个结点的父结点指向根结点，
 * 既然父亲结点不是根结点，我们就继续拿父亲结点找根结点
 * 一致递归找下去，
 * 最后返回的时候，写 parent[p] 是可以的
 * 写 parent[parent[p]] 也是没有问题的
 *
 * @param p
 * @return
 */
public int find(int p) {
    // 在 find 的时候执行路径压缩
    assert p >= 0 && p < count;
    // 注意：这里是 if 不是 while，否则就变成循环
    if (p != parent[p]) {
        // 这一行代码的逻辑要想想清楚
        // 只要不是根结点
        // 就把父亲结点指向父亲结点的父亲结点
        parent[p] = find(parent[p]);
    }
    return parent[p];
}

### 并查集的时间复杂度分析: O(logh) ==> 严格意义上: O(log*n) --> iterative algorithm, log*m比logn还要快，近乎O(1)级别

![picture 3](https://i.loli.net/2021/10/19/wmLc54Ruobg1UTO.png)  


### 关于路径压缩的思考

- 写到这里，我们发现在路径压缩的过程中，我们之前引入的辅助合并的数组，不管是 rank 还是 size，它们的定义都不准确了，因为我们在路径压缩的过程中没有对它们的定义进行维护。这一点其实并不影响我们的算法的正确性，我们不去维护 rank 数组和 size 数组的定义，是因为第 1 点：难于实现，第 2 点： rank 数组还是 size 数组的当前实现仍然可以作为一个参考值，比起随机的做法要更有意义一些。

- 其实写到这里，数组 rank 还是数组 size 的意义都不太重要了，我们只须要在 find 的时候，做好路径压缩，把孩子结点指向父亲结点即可。


-  56 problems
|   | # | Title | Acceptance | Difficulty | Frequency |
| --- | --- | --- | --- | --- | --- |
|  | 128 | Longest Consecutive Sequence | 48.0% | Medium |  |
|  | 130 | Surrounded Regions | 31.6% | Medium |  |
|  | 200 | Number of Islands | 51.9% | Medium |  |
|  | 261 | Graph Valid Tree | 44.6% | Medium |  |
|  | 305 | Number of Islands II | 39.3% | Hard |  |
|  | 323 | Number of Connected Components in an Undirected Graph | 59.7% | Medium |  |
|  | 399 | Evaluate Division | 55.9% | Medium |  |
|  | 547 | Number of Provinces | 62.1% | Medium |  |
|  | 684 | Redundant Connection | 60.4% | Medium |  |
|  | 685 | Redundant Connection II | 33.4% | Hard |  |
|  | 694 | Number of Distinct Islands | 59.0% | Medium |  |
|  | 695 | Max Area of Island | 67.9% | Medium |  |
|  | 711 | Number of Distinct Islands II | 50.6% | Hard |  |
|  | 721 | Accounts Merge | 54.1% | Medium |  |
|  | 737 | Sentence Similarity II | 47.3% | Medium |  |
|  | 765 | Couples Holding Hands | 56.1% | Hard |  |
|  | 778 | Swim in Rising Water | 58.0% | Hard |  |
|  | 785 | Is Graph Bipartite? | 49.5% | Medium |  |
|  | 803 | Bricks Falling When Hit | 33.0% | Hard |  |
|  | 827 | Making A Large Island | 44.2% | Hard |  |
|  | 839 | Similar String Groups | 43.8% | Hard |  |
|  | 886 | Possible Bipartition | 46.3% | Medium |  |
|  | 924 | Minimize Malware Spread | 41.8% | Hard |  |
|  | 928 | Minimize Malware Spread II | 41.8% | Hard |  |
|  | 947 | Most Stones Removed with Same Row or Column | 56.2% | Medium |  |
|  | 952 | Largest Component Size by Common Factor | 37.1% | Hard |  |
|  | 959 | Regions Cut By Slashes | 68.2% | Medium |  |
|  | 990 | Satisfiability of Equality Equations | 48.8% | Medium |  |
|  | 1061 | Lexicographically Smallest Equivalent String | 67.6% | Medium |  |
|  | 1020 | Number of Enclaves | 60.6% | Medium |  |
|  | 1101 | The Earliest Moment When Everyone Become Friends | 64.7% | Medium |  |
|  | 1102 | Path With Maximum Minimum Value | 51.6% | Medium |  |
|  | 1135 | Connecting Cities With Minimum Cost | 60.2% | Medium |  |
|  | 1168 | Optimize Water Distribution in a Village | 62.6% | Hard |  |
|  | 1258 | Synonymous Sentences | 57.7% | Medium |  |
|  | 1627 | Graph Connectivity With Threshold | 43.3% | Hard |  |
|  | 1632 | Rank Transform of a Matrix | 40.6% | Hard |  |
|  | 1361 | Validate Binary Tree Nodes | 42.1% | Medium |  |
|  | 1202 | Smallest String With Swaps | 50.9% | Medium |  |
|  | 1254 | Number of Closed Islands | 62.6% | Medium |  |
|  | 1267 | Count Servers that Communicate | 57.9% | Medium |  |
|  | 1319 | Number of Operations to Make Network Connected | 56.2% | Medium |  |
|  | 1391 | Check if There is a Valid Path in a Grid | 46.3% | Medium |  |
|  | 1489 | Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree | 51.7% | Hard |  |
|  | 1559 | Detect Cycles in 2D Grid | 46.7% | Medium |  |
|  | 1569 | Number of Ways to Reorder Array to Get Same BST | 49.8% | Hard |  |
|  | 1579 | Remove Max Number of Edges to Keep Graph Fully Traversable | 48.9% | Hard |  |
|  | 1584 | Min Cost to Connect All Points | 59.3% | Medium |  |
|  | 1631 | Path With Minimum Effort | 50.9% | Medium |  |
|  | 1697 | Checking Existence of Edge Length Limited Paths | 48.5% | Hard |  |
|  | 1722 | Minimize Hamming Distance After Swap Operations | 46.6% | Medium |  |
|  | 1724 | Checking Existence of Edge Length Limited Paths II | 55.5% | Hard |  |
|  | 1905 | Count Sub Islands | 61.6% | Medium |  |
|  | 1970 | Last Day Where You Can Still Cross | 47.8% | Hard |  |
|  | 1998 | GCD Sort of an Array | 45.1% | Hard |  |
|  | 2003 | Smallest Missing Genetic Value in Each Subtree | 40.4% | Hard |  |sx 





